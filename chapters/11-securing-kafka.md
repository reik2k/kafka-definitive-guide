# Chapter 11: Securing Kafka

## Table of Contents

1. [Locking Down Kafka](#locking-down-kafka)
2. [Security Protocols](#security-protocols)
   - [TLS/SSL](#tlsssl)
3. [Authentication](#authentication)
   - [SSL](#ssl)
   - [SASL](#sasl)
   - [Delegation Tokens](#delegation-tokens)
   - [Reauthentication](#reauthentication)
   - [Security Updates Without Downtime](#security-updates-without-downtime)
4. [Encryption](#encryption)
   - [End-to-End Encryption](#end-to-end-encryption)
5. [Authorization](#authorization)
   - [AclAuthorizer](#aclauthorizer)
   - [Customizing Authorization](#customizing-authorization)
6. [Auditing](#auditing)
7. [Securing ZooKeeper](#securing-zookeeper)
   - [SASL](#sasl-1)
   - [SSL](#ssl-1)
   - [Authorization](#authorization-1)
8. [Securing the Platform](#securing-the-platform)
   - [Password Protection](#password-protection)
9. [Summary](#summary)

----

## Introduction

Kafka is used for a variety of use cases ranging from website activity tracking and metrics pipelines to patient record management and online payments. Each use case has different requirements in terms of security, performance, reliability, and availability. Kafka supports several standard security technologies with a range of configuration options to tailor security to each use case.

Like performance and reliability, security is an aspect of the system that must be addressed for the system as a whole. The security of a system is only as strong as the weakest link. The customizable security features in Kafka enable integration with existing security infrastructure to build a consistent security model.

In this chapter, we will discuss the security features in Kafka and see how they address different aspects of security. Throughout the chapter, we will share best practices, potential threats, and techniques to mitigate these threats. We will also review additional measures that can be adopted to secure ZooKeeper and the rest of the platform.

## Locking Down Kafka

Kafka uses a range of security procedures to establish and maintain confidentiality, integrity, and availability of data:

- **Authentication** establishes your identity and determines who you are
- **Authorization** determines what you are allowed to do
- **Encryption** protects your data from eavesdropping and tampering
- **Auditing** tracks what you have done or have attempted to do
- **Quotas** control how much resources you can utilize

A secure deployment must guarantee:

**Client authenticity:** When Alice establishes a client connection to the broker, the broker should authenticate the client to ensure that the message is really coming from Alice.

**Server authenticity:** Before sending a message to the leader broker, Alice's client should verify that the connection is to the real broker.

**Data privacy:** All connections where the message flows, as well as all disks where messages are stored, should be encrypted or physically secured.

**Data integrity:** Message digests should be included for data transmitted over insecure networks to detect tampering.

**Access control:** Before writing the message to the log, the leader broker should verify that Alice is authorized to write to the topic.

**Auditability:** An audit trail that shows all operations performed should be logged.

**Availability:** Brokers should apply quotas and limits to avoid overwhelming the broker with denial-of-service attacks.

## Security Protocols

Kafka brokers are configured with listeners on one or more endpoints and accept client connections on these listeners. Each listener can be configured with its own security settings. Kafka supports four security protocols:

**PLAINTEXT:** No authentication or encryption. Suitable only for use within private networks.

**SSL:** SSL transport layer with optional SSL client authentication. Suitable for use in insecure networks since client and server authentication as well as encryption are supported.

**SASL_PLAINTEXT:** PLAINTEXT transport layer with SASL client authentication. Does not support encryption, suitable only for use within private networks.

**SASL_SSL:** SSL transport layer with SASL authentication. Suitable for use in insecure networks with client and server authentication and encryption.

### TLS/SSL

TLS is one of the most widely used cryptographic protocols on the public internet. Application protocols like HTTP, SMTP, and FTP rely on TLS to provide privacy and integrity of data in transit. Session keys generated during the TLS handshake enable symmetric encryption with higher performance for subsequent data transfer.

## Authentication

Authentication is the process of establishing the identity of the client and server. When Alice's client connects to the leader broker, server authentication enables the client to establish that the server is the actual broker. Client authentication verifies Alice's identity.

### SSL

When Kafka is configured with SSL or SASL_SSL as the security protocol for a listener, TLS is used as the secure transport layer. The server's digital certificate is verified by the client to establish the identity of the server. If client authentication is enabled, the server also verifies the client's digital certificate.

**Key Configuration Requirements:**
- Brokers require a key store containing the broker's private key and certificate
- Clients require a trust store containing the broker certificate or CA certificate
- Broker certificates should contain the broker hostname as a Subject Alternative Name (SAN)
- Hostname verification is enabled by default to prevent man-in-the-middle attacks

### SASL

Kafka protocol supports authentication using SASL (Simple Authentication and Security Layer) and has built-in support for several commonly used SASL mechanisms:

**SASL/GSSAPI:** Kerberos authentication that can be used to integrate with Kerberos servers like Active Directory or OpenLDAP.

**SASL/PLAIN:** Username/password authentication typically used with a custom server-side callback to verify passwords from an external password store.

**SASL/SCRAM-SHA-256 and SCRAM-SHA-512:** Username/password authentication available out of the box with Kafka without the need for additional password stores.

**SASL/OAUTHBEARER:** Authentication using OAuth bearer tokens that is typically used with custom callbacks to acquire and validate tokens granted by standard OAuth servers.

### Delegation Tokens

Delegation tokens are shared secrets between Kafka brokers and clients that provide a lightweight configuration mechanism without the requirement to distribute SSL key stores or Kerberos keytabs. Client authentication with delegation tokens is performed using SASL/SCRAM with the token identifier as username and HMAC as the password.

### Reauthentication

Kafka brokers perform client authentication when a connection is established by the client. Some security mechanisms like Kerberos and OAuth use credentials with a limited lifetime. Kafka brokers support reauthentication for connections authenticated using SASL using the configuration option `connections.max.reauth.ms`.

### Security Updates Without Downtime

Kafka deployments need regular maintenance to rotate secrets, apply security fixes, and update to the latest security protocols. Many of these maintenance tasks are performed using rolling updates or dynamic config updates without restarting brokers.

## Encryption

Encryption is used to preserve data privacy and data integrity. Kafka listeners using SSL and SASL_SSL security protocols use TLS as the transport layer, providing secure encrypted channels that protect data transmitted over an insecure network.

### End-to-End Encryption

Serializers and deserializers can be integrated with an encryption library to perform encryption of the message during serialization, and decryption during deserialization. Message encryption is typically performed using symmetric encryption algorithms like AES. A shared encryption key stored in a key management system (KMS) enables producers to encrypt the message and consumers to decrypt the message. Brokers do not require access to the encryption key.

## Authorization

Authorization is the process that determines what operations you are allowed to perform on which resources. Kafka brokers manage access control using a customizable authorizer.

### AclAuthorizer

Kafka has a built-in authorizer, `AclAuthorizer`, that can be enabled by configuring:

```
authorizer.class.name=kafka.security.authorizer.AclAuthorizer
```

`AclAuthorizer` supports fine-grained access control for Kafka resources using access control lists (ACLs). ACLs are stored in ZooKeeper and cached in memory by every broker. Each ACL binding consists of:

- Resource type: Cluster|Topic|Group|TransactionalId|DelegationToken
- Pattern type: Literal|Prefixed
- Resource name: Name of the resource or prefix, or the wildcard `*`
- Operation: Describe|Create|Delete|Alter|Read|Write|DescribeConfigs|AlterConfigs
- Permission type: Allow|Deny (Deny has higher precedence)
- Principal: Kafka principal represented as <principalType>:<principalName>
- Host: Source IP address or `*` if all hosts are authorized

### Customizing Authorization

Authorization can be customized in Kafka to implement additional restrictions or add new types of access control, like role-based access control. Custom authorizers can extend the built-in Kafka authorizer and integrate with external systems like LDAP for group-based or role-based access control.

## Auditing

Kafka brokers can be configured to generate comprehensive log4j logs for auditing and debugging. The logger instances `kafka.authorizer.logger` for authorization logging and `kafka.request.logger` for request logging can be configured independently.

Authorizers generate INFO-level log entries for every attempted operation for which access was denied, and log entries at the DEBUG level for every operation for which access was granted.

## Securing ZooKeeper

ZooKeeper stores Kafka metadata that is critical for maintaining the availability of Kafka clusters. ZooKeeper supports authentication using SASL/GSSAPI for Kerberos authentication and SASL/DIGEST-MD5 for username/password authentication. ZooKeeper also added TLS support in 3.5.0.

### SASL

SASL configuration for ZooKeeper is provided using the Java system property `java.security.auth.login.config`. The property must be set to a JAAS configuration file that contains a login section for the ZooKeeper server and client.

### SSL

SSL may be enabled on any ZooKeeper endpoint. To configure SSL on a ZooKeeper server, a key store with the hostname of the server should be configured. If client authentication is enabled, a trust store to validate client certificates is also required.

### Authorization

Authorization can be enabled for ZooKeeper nodes by setting ACLs for the path. When brokers are configured with `zookeeper.set.acl=true`, the broker sets ACLs for ZooKeeper nodes when creating the node.

## Securing the Platform

In addition to protecting data in Kafka and metadata in ZooKeeper, extra steps must be taken to ensure that the platform is secure. Key stores, trust stores, and Kerberos keytab files that contain credentials must be protected using filesystem permissions.

### Password Protection

Customizable configuration providers can be configured for Kafka brokers and clients to retrieve passwords from a secure third-party password store. Passwords may also be stored in encrypted form in configuration files with custom configuration providers that perform decryption.

## Summary

The frequency and scale of data breaches have been increasing over the last decade as cyberattacks have become increasingly sophisticated. In this chapter, we explored the vast array of options available to guarantee the confidentiality, integrity, and availability of data stored in Kafka.

Kafka security features address:

**Client authenticity:** SASL or SSL with client authentication verifies connection authenticity. Reauthentication limits exposure.

**Server authenticity:** SSL with hostname validation or SASL mechanisms with mutual authentication verify server identity.

**Data privacy:** SSL encrypts data in transit. Disk encryption protects data at rest. End-to-end encryption provides fine-grained control.

**Data integrity:** SSL detects tampering over insecure networks. Digital signatures verify integrity with end-to-end encryption.

**Access control:** Customizable authorizer with ACLs enables fine-grained access control.

**Auditability:** Authorizer logs and request logs track operations for auditing.

**Availability:** Quotas and connection management protect against denial-of-service attacks. Secured ZooKeeper ensures broker availability.

----

## External Resources and Links

This chapter referenced the following external resources:

- [RFC-4752 (SASL/GSSAPI)](https://oreil.ly/wxTZt) - SASL mechanism for Kerberos authentication
- [RFC-4616 (SASL/PLAIN)](https://oreil.ly/wZrxB) - Simple username/password authentication mechanism
- [RFC-5802 (SASL/SCRAM)](https://oreil.ly/dXe3y) - Salted Challenge Response Authentication Mechanism
- [RFC-7628 (SASL/OAUTHBEARER)](https://oreil.ly/sPBfv) - OAUTHBEARER SASL mechanism for OAuth 2.0

----

*This chapter is part of "Kafka: The Definitive Guide, 2nd Edition" by Gwen Shapira, Todd Palino, Rajini Sivaram, and Krit Petty, published by O'Reilly Media, Inc.*