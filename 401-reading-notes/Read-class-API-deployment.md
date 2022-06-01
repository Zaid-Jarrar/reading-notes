# Reading 34 - API Deployment

## Django Settings Best Practices

### Managing Django Setting Issues

**Different environments** - each environment has its own specific settings; need approach that allows you to maintain Django setting configurations.

**sensitive data** - DB passwords and tokens cannot be stored in VCS.

**Django settings are a python code** - provides flexibility, settings.py can have very tricky logic.

**Sharing setting between team members** - must have a general approach to eliminate human error when dealing with settings.

### Setting Configuration: Different Approaches

`settings_local.py` - oldest method. It extends all environment-specific settings in the settings_local.py (ignored by VCS)

settings.py file:

```python
ALLOWED_HOSTS = ['example.com']
DEBUG = False
```

settings_local.py

```python
ALLOWED_HOSTS = ['localhost']
DEBUG = True
```

Pros:
secrets not in VCS.

Cons:
-settings_local.py is not in VCS, so you can lose some of your Django environment settings.

-The Django settings file is a Python code, so settings_local.py can have some non-obvious logic.

-You need to have settings_local.example (in VCS) to share the default configurations for developers.

### 12 Factors

**12 factors** - collection of recommendations on how to build distributed web-apps that will be easy to deploy and scale in the cloud.

1.Codebase
2.Dependencies
3.Config
4.Backing services
5.Build, release, run
6.Processes
7.Port binding
8.Concurrency
9.Disposability
10.Dev/prod parity
11.Logs
12.Admin processes

-each are ways to implement a specific aspect of the project.

-significance to Configuration
-store configuration in environment.

### django-environ

-store settings in environment variable.

### Naming Conventions

-give meaningful names to settings

-always use the prefix with the project name for custom settings.

-write description for your settings in comments.

### Django Settings: Best Practices

-keep settings in environment variable

-write default values for production configuration.

-don't hardcode sensitive settings and don't put in VCS.

-split settings in groups: Django, third-party, object

-follow naming conventions for custom settings.

## How does SSH work?

### What is SSH?

**ssh** - security shell protocol. It is a remote admin protocol that allows users to access, control, and modify their remote servers over the internet.

-replaced un-encrypted Telnet and user cryptographic techniques to ensure relations to and from remote server happens in an encrypted manner.

### How does it work?

first --> `ssh{user}@{host}`

`ssh` - opens an encrypted secure shell connection

`{user}` - account you want to access

`{host}` - refers to the computer you want to access.

### Understanding Different Encryption Techniques

SSH - secure transfer between hot and and client.

*Three* different encryption techniques used by SSH:

1. **Symmetric Encryption**

2. **Asymmetrical encryption**

3. **Hashing**

#### Symmetric Encryption

**Symmetric Encryption** - form of encryption where a secret key is used for encryption and decryption of a message by client and host.

-anyone with key can decrypt message.

-aka *shared key*, encrypt entire communication and client and server get secret key using method.

**key exchange algorithm** - create a symmetric key. This key is never transmitted between client and host.

#### Asymmetrical Encryption

**Asymmetrical Encryption** - form of encryption that uses two separate keys for encryption and decryption.

public + private key = public-private key pair.

*public* key - can be used by anyone to encrypt a message; can only be decrypted by those who possess private key.

-used during key exchange algorithm of symmetric encryption.

#### Hashing

**one-way hashing** - are never to be decrypted; generate unique value of fixed length for each input.
-hard to reverse; hard to generate input from hash.

-verify authenticity of messages using hash-based message authentication code (**HMAC**)

**HMAC** - ensures the command received is not damaged.

### How SSH Work With Encryption Techniques

-authentication through client-server model of two remote systems and encrypted data that passes.

-establish SSH connection by:
1.TCP handshake with server
2.ensure secure symmetric connection
3.verify identity on server matches previous records.
4.present user credentials to connect.

### Session Encryption Negotiation

**Diffie-Hellman Key Exchange Algorithm** - algorithm that allows both client and server to arrive at a shared encryption key.

1. Client and server agree on a large seed value (prime number).

2. Both parties agree on encryption mechanism to generate set of values by manipulating seed value in a specific way.

3. Both generate another prime number separately. This is a *private* key.

4. Private key used to compute *public key*

5. Original prime number, private key, and public key are used by both parties to create final shared key.

6. Now can symmetrically encrypt entire SSH session.