# Chapter 11 – Securing Kafka – Test | CCDAK Preparation Material

---

## Question 1
Which four security protocols does Kafka support?
A) PLAINTEXT, SSL, SASL_PLAINTEXT, SASL_SSL
B) HTTP, HTTPS, TCP, SSL
C) TLS, SASL, KERBEROS, OAUTH
D) PLAINTEXT, ENCRYPTED, AUTHENTICATED, SECURE

---

## Question 2
What is the main difference between authentication and authorization?
A) Authentication verifies identity while authorization determines what operations are allowed
B) Authentication is for clients while authorization is for brokers
C) Authentication uses SSL while authorization uses SASL
D) Authentication is optional while authorization is mandatory

---

## Question 3
Which security protocol provides encryption but no authentication?
A) PLAINTEXT
B) SSL without client authentication
C) SASL_PLAINTEXT
D) SASL_SSL

---

## Question 4
What does TLS stand for and what was its predecessor called?
A) Transport Layer Security, predecessor was Secure Sockets Layer (SSL)
B) Total Layer Security, predecessor was SSL
C) Transmission Layer Security, predecessor was HTTPS
D) Trusted Layer Service, predecessor was TCP

---

## Question 5
Which configuration determines the listener used for inter-broker communication?
A) broker.listener.name
B) inter.broker.listener.name
C) broker.security.protocol
D) internal.listener.name

---

## Question 6
What is the principal used for unauthenticated connections in Kafka?
A) User:Guest
B) User:Anonymous
C) User:ANONYMOUS
D) User:Unknown

---

## Question 7
Which SSL configuration option enables required client authentication?
A) ssl.client.auth=true
B) ssl.client.auth=required
C) ssl.client.authentication=enabled
D) ssl.require.client.auth=true

---

## Question 8
What is hostname verification used for in SSL?
A) To improve performance
B) To protect against man-in-the-middle attacks
C) To enable load balancing
D) To configure DNS resolution

---

## Question 9
Which SASL mechanism is used for Kerberos authentication?
A) SASL/KERBEROS
B) SASL/GSSAPI
C) SASL/KRB5
D) SASL/KERB

---

## Question 10
What does SASL stand for?
A) Secure Authentication and Security Layer
B) Simple Authentication and Security Layer
C) Standard Authentication Security Layer
D) Secure Access Security Layer

---

## Question 11
Which SASL mechanisms are supported by Kafka out of the box?
A) GSSAPI, PLAIN, SCRAM-SHA-256, SCRAM-SHA-512, OAUTHBEARER
B) GSSAPI, PLAIN, MD5, SHA1
C) KERBEROS, LDAP, OAUTH, JWT
D) DIGEST-MD5, EXTERNAL, ANONYMOUS

---

## Question 12
What is the default iteration count for SCRAM in Kafka?
A) 1,024
B) 2,048
C) 4,096
D) 8,192

---

## Question 13
Where are SCRAM user credentials stored in Kafka?
A) In broker configuration files
B) In ZooKeeper
C) In a separate database
D) In LDAP

---

## Question 14
Which configuration option is used to specify JAAS configuration in Kafka?
A) jaas.config
B) sasl.jaas.config
C) security.jaas.config
D) auth.jaas.config

---

## Question 15
What is the purpose of keytab files in Kerberos authentication?
A) Store encryption keys
B) Store mapping of principals to their long-term keys
C) Store broker configuration
D) Store ACL definitions

---

## Question 16
Which SSL store contains the private key and certificate?
A) Trust store
B) Key store
C) Certificate store
D) Credential store

---

## Question 17
What type of file format is PKCS12?
A) A text file format
B) A binary key store format
C) An XML configuration format
D) A certificate signing request format

---

## Question 18
Can SSL key stores and trust stores be updated dynamically without broker restart?
A) No, always requires restart
B) Yes, using Admin API or kafka-configs tool
C) Only key stores can be updated
D) Only trust stores can be updated

---

## Question 19
What is the purpose of the Subject Alternative Name (SAN) in SSL certificates?
A) To encrypt data
B) To enable hostname verification
C) To store passwords
D) To define ACLs

---

## Question 20
Which broker configuration delays response on authentication failures?
A) auth.delay.ms
B) connection.failed.authentication.delay.ms
C) security.auth.delay.ms
D) sasl.authentication.delay.ms

---

## Question 21
What does SCRAM stand for?
A) Secure Challenge Response Authentication Method
B) Salted Challenge Response Authentication Mechanism
C) Simple Challenge Response Authentication Mode
D) Standard Cryptographic Response Authentication Mechanism

---

## Question 22
Which built-in authorizer class should be configured for ACL-based authorization?
A) SimpleAclAuthorizer
B) AclAuthorizer
C) StandardAuthorizer
D) KafkaAuthorizer

---

## Question 23
Where are ACLs stored when using AclAuthorizer?
A) In broker memory only
B) In ZooKeeper
C) In configuration files
D) In a database

---

## Question 24
Which ACL operation is implicitly granted if Read permission is granted?
A) Write
B) Describe
C) Alter
D) Delete

---

## Question 25
What is the separator character used for the super.users configuration?
A) Comma
B) Semicolon
C) Colon
D) Pipe

---

## Question 26
Which ACL resource type is used for transactional producers?
A) Topic
B) Group
C) TransactionalId
D) Producer

---

## Question 27
What does the ClusterAction ACL operation allow?
A) Creating topics
B) Inter-broker requests including controller and replication
C) Managing consumer groups
D) Altering configurations

---

## Question 28
Which configuration enables reauthentication for SASL connections?
A) sasl.reauth.enabled
B) connections.max.reauth.ms
C) sasl.session.timeout.ms
D) authentication.renewal.ms

---

## Question 29
What is the purpose of delegation tokens?
A) To delegate administrative permissions
B) Shared secrets between brokers and clients for lightweight authentication
C) To encrypt messages
D) To manage ACLs

---

## Question 30
Which SASL mechanism do delegation tokens use for authentication?
A) GSSAPI
B) PLAIN
C) SCRAM
D) OAUTHBEARER

---

## Question 31
Why should SASL/PLAIN only be used with SSL?
A) For better performance
B) Because it transmits clear-text passwords
C) To comply with standards
D) To enable compression

---

## Question 32
Which logger is used for authorization logging in Kafka?
A) kafka.security.logger
B) kafka.authorizer.logger
C) kafka.acl.logger
D) kafka.auth.logger

---

## Question 33
What is the typical SSL performance overhead?
A) 5-10%
B) 10-15%
C) 20-30%
D) 40-50%

---

## Question 34
Which TLS protocol versions does Kafka enable by default?
A) TLSv1.0 and TLSv1.1
B) TLSv1.1 and TLSv1.2
C) TLSv1.2 and TLSv1.3
D) All TLS versions

---

## Question 35
What is end-to-end encryption in Kafka?
A) Encryption between brokers
B) Encryption at the serializer level so brokers never see unencrypted data
C) Encryption of configuration files
D) Encryption using ZooKeeper

---

## Question 36
Where are encrypted messages decrypted in end-to-end encryption?
A) At the broker
B) At the deserializer in consumers
C) In ZooKeeper
D) At the network layer

---

## Question 37
Which Kafka versions support ZooKeeper SSL?
A) 0.10.0 and later
B) 0.11.0 and later
C) 2.0.0 and later
D) 3.5.0 and later for ZooKeeper, configurable in Kafka

---

## Question 38
What SASL mechanism does ZooKeeper support for authentication?
A) GSSAPI and DIGEST-MD5
B) PLAIN and SCRAM
C) OAUTHBEARER only
D) EXTERNAL only

---

## Question 39
What is the purpose of the kafka-acls tool?
A) To create topics
B) To manage ACLs using the configured authorizer
C) To encrypt data
D) To monitor performance

---

## Question 40
Which ACL permission allows a consumer to read from a topic?
A) Topic:Read
B) Topic:Consume
C) Topic:Fetch
D) Topic:Get

---

## Question 41
What does IdempotentWrite ACL operation allow?
A) Writing without acknowledgment
B) Idempotent produce for nontransactional producers
C) Writing to multiple topics
D) Transactional writes

---

## Question 42
Which configuration option customizes the principal builder?
A) security.principal.builder
B) principal.builder.class
C) auth.principal.class
D) sasl.principal.builder

---

## Question 43
What is the purpose of ssl.principal.mapping.rules?
A) To map SSL ciphers
B) To customize the principal extracted from client certificates
C) To configure SSL protocols
D) To define trust relationships

---

## Question 44
Which configuration allows everyone access if no ACL is found?
A) allow.everyone.default=true
B) allow.everyone.if.no.acl.found=true
C) acl.default.allow=true
D) security.allow.all=true

---

## Question 45
What is the master key used for in delegation tokens?
A) Encrypting messages
B) Generating and validating delegation tokens
C) Signing certificates
D) Encrypting configurations

---

## Question 46
Which authentication protocol requires a secure DNS service?
A) PLAIN
B) SCRAM
C) GSSAPI (Kerberos)
D) OAUTHBEARER

---

## Question 47
What is OAuth 2.0 bearer token lifetime used for?
A) To define ACL expiration
B) To limit credential exposure with short-lived tokens
C) To configure session timeout
D) To set connection limits

---

## Question 48
Which tool generates encrypted passwords for SASL/PLAIN?
A) openssl
B) htpasswd
C) gpg
D) keytool

---

## Question 49
What is the purpose of config providers in Kafka?
A) To provide broker configuration
B) To retrieve passwords from secure external stores
C) To configure security protocols
D) To manage ACLs

---

## Question 50
Which ACL operation is required for consumers using group management?
A) Topic:Read
B) Group:Read
C) Group:Join
D) Consumer:Read

---

## Question 51
What is the purpose of the Common Name (CN) in SSL certificates?
A) To encrypt data
B) To identify the entity owning the certificate
C) To store passwords
D) To define ACLs

---

## Question 52
Which configuration option sets the ZooKeeper authentication provider?
A) zookeeper.auth.provider
B) authProvider.sasl
C) zk.authentication.provider
D) security.zookeeper.auth

---

## Question 53
What happens if a user is compromised and you cannot restart brokers immediately?
A) Wait for connection timeout
B) Use Deny ACLs to prevent operations
C) Disable the broker
D) Clear ZooKeeper data

---

## Question 54
Which ACL pattern type matches all resources with a specific prefix?
A) Wildcard
B) Prefixed
C) Literal
D) Regex

---

## Question 55
What is disk encryption used for in Kafka security?
A) To encrypt messages in transit
B) To protect data at rest even if disk is stolen
C) To authenticate clients
D) To authorize operations

---

## Question 56
Which configuration must all brokers share for delegation tokens?
A) broker.id
B) delegation.token.master.key
C) security.inter.broker.protocol
D) sasl.enabled.mechanisms

---

## Question 57
What is the purpose of the kafka-delegation-tokens tool?
A) To create topics
B) To create, renew, and expire delegation tokens
C) To manage ACLs
D) To configure security

---

## Question 58
Which permission type has higher precedence in ACLs?
A) Allow
B) Deny
C) Both have equal precedence
D) Depends on order

---

## Question 59
What is the purpose of quotas in Kafka security?
A) To authenticate users
B) To control resource utilization and prevent DoS attacks
C) To encrypt data
D) To authorize operations

---

## Question 60
Which SASL mechanism uses unsecured JSON Web Tokens by default?
A) GSSAPI
B) PLAIN
C) SCRAM
D) OAUTHBEARER

---