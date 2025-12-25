# Chapter 11 – Securing Kafka – Solutions and Explanations

> **Answer Key with Detailed Explanations** | CCDAK Preparation Material

---

## Question 1
**Correct Answer: A**

**Explanation:**
Kafka supports four security protocols: PLAINTEXT (no security), SSL (TLS with optional client authentication), SASL_PLAINTEXT (SASL authentication without encryption), and SASL_SSL (SASL authentication with SSL encryption). These protocols combine transport layer (PLAINTEXT or SSL) with optional authentication layer (SSL or SASL).

---

## Question 2
**Correct Answer: A**

**Explanation:**
Authentication establishes your identity (who you are) while authorization determines what operations you are allowed to perform (what you can do). Authentication occurs first when a connection is established, and the resulting KafkaPrincipal is then used for authorization checks on each request.

---

## Question 3
**Correct Answer: B**

**Explanation:**
SSL without client authentication provides encryption of data in transit but doesn't authenticate the client. The broker authenticates to the client using its certificate, but the client principal is User:ANONYMOUS since no client certificate is verified.

---

## Question 4
**Correct Answer: A**

**Explanation:**
TLS stands for Transport Layer Security, and its predecessor was called Secure Sockets Layer (SSL). Although TLS has replaced SSL, the protocol is still commonly referred to by its old name SSL. Kafka enables TLSv1.2 and TLSv1.3 by default.

---

## Question 5
**Correct Answer: B**

**Explanation:**
The `inter.broker.listener.name` configuration determines which listener is used for inter-broker communication. Brokers need both server-side and client-side configuration for this listener since they establish connections to other brokers.

---

## Question 6
**Correct Answer: C**

**Explanation:**
The principal `User:ANONYMOUS` (all uppercase) is used for unauthenticated connections, including clients on PLAINTEXT listeners and unauthenticated clients on SSL listeners without client authentication enabled.

---

## Question 7
**Correct Answer: B**

**Explanation:**
The configuration `ssl.client.auth=required` enables required client authentication using SSL. When set to `requested`, client authentication is optional, and clients without key stores will be assigned User:ANONYMOUS.

---

## Question 8
**Correct Answer: B**

**Explanation:**
Hostname verification protects against man-in-the-middle attacks by verifying that the hostname in the server certificate matches the host the client is connecting to. This is enabled by default and should not be disabled in production.

---

## Question 9
**Correct Answer: B**

**Explanation:**
SASL/GSSAPI is the SASL mechanism used for Kerberos authentication. GSSAPI (Generic Security Service Application Program Interface) is a framework that supports Kerberos V5 mechanism for secure authentication.

---

## Question 10
**Correct Answer: B**

**Explanation:**
SASL stands for Simple Authentication and Security Layer. It's a framework for providing authentication using different mechanisms in connection-oriented protocols. Kafka supports GSSAPI, PLAIN, SCRAM-SHA-256, SCRAM-SHA-512, and OAUTHBEARER mechanisms.

---

## Question 11
**Correct Answer: A**

**Explanation:**
Kafka supports five SASL mechanisms out of the box: GSSAPI (Kerberos), PLAIN (username/password), SCRAM-SHA-256 and SCRAM-SHA-512 (salted challenge-response), and OAUTHBEARER (OAuth 2.0 bearer tokens). Each can be customized with callbacks for integration with external systems.

---

## Question 12
**Correct Answer: C**

**Explanation:**
The default iteration count for SCRAM in Kafka is 4,096. This high iteration count combined with unique random salts for each stored key helps limit the impact of brute-force attacks even if ZooKeeper security is compromised.

---

## Question 13
**Correct Answer: B**

**Explanation:**
SCRAM user credentials are stored in ZooKeeper. Brokers load SCRAM metadata into an in-memory cache during startup and keep it updated using ZooKeeper watchers. This built-in provider works without additional password servers but requires secure ZooKeeper.

---

## Question 14
**Correct Answer: B**

**Explanation:**
The `sasl.jaas.config` configuration option is used to specify JAAS configuration in Kafka. It's recommended over the java.security.auth.login.config system property because it supports password protection and separate configuration for each SASL mechanism.

---

## Question 15
**Correct Answer: B**

**Explanation:**
Keytab files store the mapping of Kerberos principals to their long-term keys in encrypted form. Brokers and clients use keytabs for automatic authentication without requiring manual password entry. Access to keytab files must be restricted with filesystem permissions.

---

## Question 16
**Correct Answer: B**

**Explanation:**
The key store contains the private key and certificate. The trust store contains certificates of trusted certificate authorities (CAs). Brokers need a key store with their certificate, and clients need a trust store with the broker CA certificate.

---

## Question 17
**Correct Answer: B**

**Explanation:**
PKCS12 is a binary key store format used to store private keys and certificates. It's the recommended format for SSL stores in Kafka. The keytool utility can generate and manage PKCS12 key stores and trust stores.

---

## Question 18
**Correct Answer: B**

**Explanation:**
SSL key stores and trust stores can be dynamically updated without broker restart using the Admin API or kafka-configs tool. The broker can be configured to monitor file changes or the configuration can point to a new versioned file.

---

## Question 19
**Correct Answer: B**

**Explanation:**
The Subject Alternative Name (SAN) extension in SSL certificates stores the hostname and enables hostname verification. Clients verify that the server hostname matches the SAN or Common Name in the certificate to prevent man-in-the-middle attacks.

---

## Question 20
**Correct Answer: B**

**Explanation:**
The `connection.failed.authentication.delay.ms` configuration delays the response on authentication failures to reduce the rate at which failed authentications are retried by clients. This helps protect against denial-of-service attacks on TLS listeners.

---

## Question 21
**Correct Answer: B**

**Explanation:**
SCRAM stands for Salted Challenge Response Authentication Mechanism. It applies a one-way cryptographic hash function on passwords combined with random salt to avoid transmitting clear-text passwords and to store passwords securely.

---

## Question 22
**Correct Answer: B**

**Explanation:**
`AclAuthorizer` is the built-in authorizer class for ACL-based authorization in Kafka 2.3+. It replaced the deprecated SimpleAclAuthorizer. The authorizer is configured using `authorizer.class.name=kafka.security.authorizer.AclAuthorizer`.

---

## Question 23
**Correct Answer: B**

**Explanation:**
ACLs are stored in ZooKeeper and cached in memory by brokers for high-performance lookups. The cache is loaded during broker startup and kept up-to-date using ZooKeeper watchers for any ACL changes.

---

## Question 24
**Correct Answer: B**

**Explanation:**
Describe permission is implicitly granted if Read, Write, Alter, or Delete permission is granted. Similarly, DescribeConfigs permission is implicitly granted if AlterConfigs permission is granted. This simplifies ACL management.

---

## Question 25
**Correct Answer: B**

**Explanation:**
The `super.users` configuration uses semicolon as the separator (not comma like most Kafka configurations). This is because user principals like distinguished names from SSL certificates often contain commas.

---

## Question 26
**Correct Answer: C**

**Explanation:**
TransactionalId is the ACL resource type used for transactional producers. Producers need TransactionalId:Write permission to use transactions. This resource type was introduced to provide fine-grained control over transactional operations.

---

## Question 27
**Correct Answer: B**

**Explanation:**
ClusterAction ACL operation allows inter-broker requests including controller requests and follower fetch requests for replication. This permission should only be granted to brokers, never to client applications.

---

## Question 28
**Correct Answer: B**

**Explanation:**
The `connections.max.reauth.ms` configuration enables reauthentication for SASL connections. When set to a positive value, brokers determine session lifetime and terminate connections that don't reauthenticate within the interval.

---

## Question 29
**Correct Answer: B**

**Explanation:**
Delegation tokens are shared secrets between Kafka brokers and clients that provide lightweight authentication. They reduce load on authentication servers like Kerberos KDC and simplify security configuration for frameworks like Kafka Connect workers.

---

## Question 30
**Correct Answer: C**

**Explanation:**
Delegation tokens use SASL/SCRAM for authentication. The token identifier is used as the username and the HMAC is used as the password. At least one SCRAM mechanism must be enabled on brokers to support delegation token authentication.

---

## Question 31
**Correct Answer: B**

**Explanation:**
SASL/PLAIN should only be used with SSL (SASL_SSL) because it transmits clear-text passwords over the wire during authentication. Without SSL encryption, eavesdroppers can capture passwords. Combined with SSL, SASL/PLAIN provides secure username/password authentication.

---

## Question 32
**Correct Answer: B**

**Explanation:**
The `kafka.authorizer.logger` is used for authorization logging. It generates INFO-level logs for denied operations and DEBUG-level logs for granted operations. This logger can be configured independently for audit logging requirements.

---

## Question 33
**Correct Answer: C**

**Explanation:**
SSL introduces a 20-30% performance overhead due to CPU usage for encryption and because zero-copy transfer is not supported for SSL channels. The overhead depends on traffic patterns and hardware. Newer Java versions have improved SSL performance.

---

## Question 34
**Correct Answer: C**

**Explanation:**
Kafka enables TLSv1.2 and TLSv1.3 by default. Older protocols like TLSv1.0 and TLSv1.1 are disabled due to known vulnerabilities. Strong security requires using current TLS protocols and appropriate cipher suites.

---

## Question 35
**Correct Answer: B**

**Explanation:**
End-to-end encryption encrypts messages at the serializer level in producers and decrypts at the deserializer level in consumers. Brokers never see unencrypted data, providing protection even from platform administrators with physical disk access.

---

## Question 36
**Correct Answer: B**

**Explanation:**
In end-to-end encryption, encrypted messages are decrypted at the deserializer in consumers. The deserializer integrates with an encryption library and retrieves the encryption key from a Key Management System (KMS) to decrypt messages.

---

## Question 37
**Correct Answer: D**

**Explanation:**
ZooKeeper added TLS support in version 3.5.0. Kafka can be configured to use SSL for ZooKeeper connections by setting `zookeeper.ssl.client.enable=true` and providing appropriate key stores and trust stores.

---

## Question 38
**Correct Answer: A**

**Explanation:**
ZooKeeper supports SASL authentication using GSSAPI (Kerberos) and DIGEST-MD5 mechanisms. DIGEST-MD5 should only be used with TLS encryption due to known vulnerabilities and is not recommended for production.

---

## Question 39
**Correct Answer: B**

**Explanation:**
The kafka-acls tool manages ACLs using the authorizer configured in brokers. It can add, remove, and list ACLs. ACLs can be created directly in ZooKeeper or through brokers using the Admin API.

---

## Question 40
**Correct Answer: A**

**Explanation:**
Topic:Read ACL permission allows consumers to read from a topic using the Fetch operation. Consumers also need Group:Read permission for consumer group management and offset management.

---

## Question 41
**Correct Answer: B**

**Explanation:**
Cluster:IdempotentWrite ACL operation is required for nontransactional idempotent producers. This permission allows producers to use idempotent produce with InitProducerId and Produce requests. Transactional producers don't need this permission.

---

## Question 42
**Correct Answer: B**

**Explanation:**
The `principal.builder.class` configuration customizes the principal builder for brokers. This allows custom extraction and transformation of the KafkaPrincipal from authentication credentials, enabling integration with existing security infrastructure.

---

## Question 43
**Correct Answer: B**

**Explanation:**
The `ssl.principal.mapping.rules` configuration customizes how the principal is extracted from SSL client certificates. By default, the distinguished name (DN) is used, but mapping rules can transform it to a simpler principal format.

---

## Question 44
**Correct Answer: B**

**Explanation:**
The `allow.everyone.if.no.acl.found=true` configuration grants access to all users for resources without ACLs. This is useful during development but not recommended for production as it may grant unintended access.

---

## Question 45
**Correct Answer: B**

**Explanation:**
The delegation token master key (`delegation.token.master.key`) is used by all brokers to generate and validate delegation tokens. All brokers must share the same master key, which should be protected using encryption or external secure storage.

---

## Question 46
**Correct Answer: C**

**Explanation:**
GSSAPI (Kerberos) requires a secure DNS service for server authentication and hostname lookup during authentication. Insecure DNS can be exploited for man-in-the-middle attacks, so DNS security is critical for Kerberos deployments.

---

## Question 47
**Correct Answer: B**

**Explanation:**
OAuth 2.0 bearer tokens have limited lifetime to reduce credential exposure if tokens are compromised. Short-lived tokens combined with reauthentication limit the time an existing connection can use a token after revocation.

---

## Question 48
**Correct Answer: B**

**Explanation:**
The `htpasswd` tool from Apache can be used to generate encrypted passwords for SASL/PLAIN. Custom server callbacks can integrate with htpasswd files or other secure password databases for production deployments.

---

## Question 49
**Correct Answer: B**

**Explanation:**
Config providers retrieve passwords from secure external stores or decrypt passwords from configuration files. This avoids storing clear-text passwords in configuration files. Custom providers can integrate with enterprise key management systems.

---

## Question 50
**Correct Answer: B**

**Explanation:**
Group:Read ACL operation is required for consumers using group management (JoinGroup, SyncGroup, Heartbeat) or Kafka-based offset management (OffsetCommit). It's also required for transactional producers committing offsets.

---

## Question 51
**Correct Answer: B**

**Explanation:**
The Common Name (CN) in SSL certificates identifies the entity owning the certificate. It can be used along with Subject Alternative Name for hostname verification. The DN containing the CN is used as the default KafkaPrincipal.

---

## Question 52
**Correct Answer: B**

**Explanation:**
The `authProvider.sasl` configuration sets the ZooKeeper SASL authentication provider. For example: `authProvider.sasl=org.apache.zookeeper.server.auth.SASLAuthenticationProvider` enables SASL authentication on ZooKeeper servers.

---

## Question 53
**Correct Answer: B**

**Explanation:**
If a user is compromised and brokers cannot be restarted immediately, Deny ACLs can be used to prevent all operations by that principal. ACL changes are applied quickly across brokers, providing the fastest way to disable access.

---

## Question 54
**Correct Answer: B**

**Explanation:**
The Prefixed ACL pattern type matches all resources with a specific prefix. For example, a Prefixed ACL for topic "customer" matches "customerOrders", "customerProfile", etc. Literal pattern matches exact resource names.

---

## Question 55
**Correct Answer: B**

**Explanation:**
Disk encryption (whole disk or volume encryption) protects data at rest by ensuring sensitive data cannot be retrieved even if physical disks are stolen. This complements TLS encryption for data in transit.

---

## Question 56
**Correct Answer: B**

**Explanation:**
All brokers must share the same `delegation.token.master.key` configuration for generating and validating delegation tokens. The key can only be rotated by restarting all brokers, and existing tokens must be deleted before rotation.

---

## Question 57
**Correct Answer: B**

**Explanation:**
The kafka-delegation-tokens tool creates, renews, and expires delegation tokens. Tokens can be created for authenticated users and distributed to applications for lightweight authentication without distributing SSL keystores or Kerberos keytabs.

---

## Question 58
**Correct Answer: B**

**Explanation:**
Deny ACLs have higher precedence than Allow ACLs. AclAuthorizer denies access if any Deny ACL matches the action, even if Allow ACLs also match. This ensures explicit denials cannot be overridden.

---

## Question 59
**Correct Answer: B**

**Explanation:**
Quotas control resource utilization to ensure fair allocation among users and prevent denial-of-service attacks. Connection quotas and limits protect broker availability by preventing some users from overwhelming brokers with excessive connections or requests.

---

## Question 60
**Correct Answer: D**

**Explanation:**
The OAUTHBEARER SASL mechanism uses unsecured JSON Web Tokens (JWTs) by default in the built-in implementation. This is not suitable for production. Custom callbacks must be used to integrate with standard OAuth servers for secure authentication.

---