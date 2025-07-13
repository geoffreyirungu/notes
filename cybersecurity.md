# Cybersecurity

## What is Confidentiality, Integrity and Authenticity in Cyber Security
* **Confidentiality:** Ensures that data or message is kept secret from unauthorized parties.
* **Integrity:** Ensures that the data or message has not been altered or tampered with during transmission or storage.
* **Authenticity:** Ensures data and transactions are genuine and come from a verified source.

## What is a nonce(number used once)
In cryptography, a nonce (short for "number used once") is a unique, random, or pseudo-random number used just once in cryptographic communication to prevent replay attacks. 

## Encryption
Encryption is the process of converting plain data (plaintext) into an unreadable format (ciphertext) using an algorithm and an encryption key. 
The purpose is to protect the confidentiality of the data, so only authorized parties with the decryption key can access the original information.
**Types of encryption**
* **Symmetric encryption:** The same key is used for encryption and decryption. It is faster than asymmetric encryption and relies on the secure exchange of the secret key.
Example algorithms: Advanced Encryption Standard(AES), Data Encryption Standard(DES)
* **Asymmetric/public-key encryption:** Uses a key pair (public key to encrypt, private key to decrypt). It is generally slower than symmetric encryption due to the complexity of the algorithms but eliminates the need for a secure key exchange channel. 
Example algorithms: Rivest Shamir Adleman(RSA), Elliptic Curve Cryptography(ECC)

Illustration:

	Plaintext (Readable)  ----encrypt with shared/public key---->  Ciphertext (Unreadable)
	HELLO WORLD                                  XU2H8#@!34JD

	Ciphertext  ----decrypt with shared/private key---->  Plaintext
	XU2H8#@!34JD                               HELLO WORLD

**Hybrid Encryption**
Hybrid encryption in cryptography combines symmetric and asymmetric encryption to offer efficient and secure data transmission. 
It uses symmetric encryption for fast data processing and asymmetric encryption for secure key exchange, leveraging the strengths of both methods. 
**How Hybrid Encryption Works:**
* **Symmetric key generation:** the sender generates a random symmetric key.
* **Data Encryption:** the sender then uses the symmetric key to encrypt the actual message/data. 
* **Symmetric Key encryption:** the sender encrypts the symmetric key using the recipient's public key.
* **Transmission:** the sender sends both the encrypted data/message and the encrypted symmetric key.
* **Symmetric key decryption:** the recipient decrypts the symmetric key with their private key.
* **Data decryption:** the recipient uses the decrypted symmetric key to decrypt the data.

** Probabilistic/Randomized Encryption and Deterministic Encryption**
**Probabilistic encryption** is the use of randomness in an encryption algorithm, so that when encrypting the same message several times with the same key will, in general, yield different ciphertexts.
This randomness helps protect against certain attacks, such as chosen-ciphertext attacks, where an attacker might try to manipulate the ciphertext to gain information about the plaintext. 
**Note:** A chosen ciphertext attack allows an adversary to select a piece of ciphertext and attempt to reveal its corresponding decrypted plaintext.
The term "probabilistic encryption" is typically used in reference to public key encryption algorithms; 
however various symmetric key encryption algorithms achieve a similar property (e.g., block ciphers when used in a chaining mode such as CBC), and stream ciphers such as Freestyle which are inherently random. 

**Deterministic encryption** is a type of encryption where a given plaintext input always produces the same ciphertext output, given the same key.
This means that the encrypted data is predictable and reversible, making it suitable for search and comparison operations on encrypted data.
While deterministic encryption is useful for certain operations, it's crucial to consider its security implications, especially for sensitive data. 
It's vulnerable to pattern analysis. If an attacker sees the same ciphertext multiple times, they know it's the same plaintext.


**Authenticated Encryption (AE) and Authenticated Encryption with Associated Data(AEAD)**
**Authenticated encryption(AE)** is a type of encryption that ensures both the confidentiality of the data and its authenticity.
**Confidentiality:**
* Just like regular encryption, authenticated encryption ensures that the data is secret and cannot be understood by unauthorized parties.
* The data is converted into an unreadable format (ciphertext) using a secret key, preventing anyone without the key from deciphering it. 
**Authenticity:**
* It generates a message authentication code (MAC), a unique tag (also known as an authentication tag), based on the ciphertext and a secret key. 
* This tag is included in the transmitted data.
* The receiver uses the same key to calculate a MAC of the received ciphertext. 
* If the generated tag matches the received tag, the receiver knows that the data hasn't been altered in transit and that it was sent by a party who knows the secret key. 

That being said AE ensures confidentiality, integrity and authenticity of the data.
Examples of encryption modes/modes of operation that provide AE are Galois/Counter Mode (GCM), Counter with Cipher Block Chaining-Message Authentication Code (CCM).

**AEAD (Authenticated Encryption with Associated Data)** extends AE by allowing additional data (e.g., headers) to be authenticated with the encrypted message, without being encrypted itself(the associated data).
**Use Cases:** Network packets where headers are unencrypted but still need authentication, or tying encrypted data to specific user accounts. 
**Note:** AEAD produces different ciphertexts even with the same plaintext and key (due to random initialization vectors, a type of nonce).

**Deterministic AEAD**
Deterministic AEAD (DAEAD) is a variant of AEAD where encrypting the same plaintext with the same key and associated data will always produce the same ciphertext.
It is deterministic(The same plaintext + same key + same associated data will always produce the same ciphertext) since it does not use randomness(does not require a nonce).
**Use Cases of DAEAD**
* searching and comparing on encrypted data, as the ciphertext can be used as a unique identifier for the plaintext.
* Deduplication: Same values should produce the same ciphertext, enabling you to spot duplicates.
* Tokenization: You want to replace Personally Identifiable Information(PII) like email or phone number with consistent tokens.

**Tokenization**, when applied to data security, is the process of replacing sensitive data with a non-sensitive equivalent known as a token.

| Feature                      | AEAD                       | Deterministic AEAD (DAEAD)      |
| ---------------------------- | -------------------------- | ------------------------------- |
| Same input → same output?    | ❌ No                       | ✅ Yes                           |
| Secure against pattern leaks | ✅ Yes                      | ❌ No (reveals duplicate values) |
| Can be used for search?      | ❌ No                       | ✅ Yes                           |
| Supports associated data?    | ✅ Yes                      | ✅ Yes                           |
| Use case                     | General-purpose encryption | Searchable/tokenized encryption |


| Algorithm          | Full Name                                          | Type  | Deterministic? | Standardized?           | Notes                                           |
| ------------------ | -------------------------------------------------- | ----- | -------------- | ----------------------- | ----------------------------------------------- |
| **AES-GCM**        | Advanced Encryption Standard – Galois/Counter Mode | AEAD  | ❌ No           | ✅ Yes (NIST SP 800-38D) | Most common AEAD, but randomized                |
| **AES-CTR + HMAC** | AES in Counter Mode with HMAC for authentication   | AEAD  | ❌ No           | ❌ No (custom)           | Can be made deterministic if built carefully    |
| **AES-SIV**        | AES with Synthetic IV                              | DAEAD | ✅ Yes          | ✅ Yes (RFC 5297)        | Tink uses this under the hood                   |
| **XSalsa20-SIV**   | Extended Salsa20 with Synthetic IV                 | DAEAD | ✅ Yes          | ❌ No                    | Less common; more in research/prototypes        |
| **ChaCha20-SIV**   | ChaCha20 with Synthetic IV                         | DAEAD | ✅ Yes          | ❌ No                    | Custom use in modern, high-performance settings |


	
**Symmetric encryption**
Symmetric encryption algorithms are categorized into two main types: **block ciphers and stream ciphers**. 
**1. Block Ciphers**
Block ciphers divide the data into fixed-size blocks (like 64, 128, or 256 bits) and encrypt each block independently.
The algorithm operates on each block, using the shared secret key to transform the data. 
**Modes of Operation:**
Block ciphers are often used with different modes of operation, such as Electronic codebook (ECB), Cipher Block Chaining (CBC), Counter (CTR) mode and Galois/Counter Mode (GCM), to enhance security and prevent patterns in the encrypted data. 
**Why modes of operations are needed:**
* To encrypt data longer than one block securely.
* To provide additional security features like authentication/authenticity and integrity
**Padding:**
Padding in block ciphers is a process where extra data (padding) is added before encryption, ensuring that the final data length is a multiple of the block size of the cipher.
This is necessary because most block cipher modes of operation, like CBC, require the input to be an exact multiple of the block size. 
GCM does not require padding. 
**Common Algorithms:**
Examples of block ciphers include Advanced Encryption Standard (AES),widely used block cipher that encrypts data in 128-bit blocks, Data Encryption Standard (DES), and Blowfish. 
**Advantages:** Can provide strong encryption for large amounts of data. 
**Disadvantages:** Can be less efficient for real-time data streams. 

**DES**
* **Key size:** 56 bits
* **Block size:** 64 bits
* **Status:** Considered insecure and obsolete today due to vulnerability to brute-force attacks.
AES is far more widely used today due to its stronger security, better performance, and adoption as the encryption standard by NIST(National Institute of Standards and Technology). 
DES is considered outdated and insecure, and is generally avoided except in legacy systems.

**AES**
* **Key sizes:** 128, 192, or 256 bits
* **Block size:** 128 bits
* **Status:** Considered highly secure and is the current standard for symmetric encryption.
* Most widely used symmetric encryption algorithm today.

**AES Modes**
**Electronic Codebook (ECB) mode (⚠️ Not Recommended)**
ECB is the simplest mode
**How it works:**
* Each block of plaintext is encrypted independently with the same key.
* No chaining or randomness.

However, it is generally not recommended due to its vulnerability to pattern recognition attacks.
🚫 ECB is not secure for messages longer than 1 block.
**CBC (Cipher Block Chaining)**
**How it works:**
* Each plaintext block is XORed with the previous ciphertext block before encryption.
* Requires an Initialization Vector (IV).
IV Must be unique and unpredictable for each message.
🔄 Process:
	C0 = Encrypt(P0 XOR IV)
	C1 = Encrypt(P1 XOR C0)
	C2 = Encrypt(P2 XOR C1)
	...

Libraries like OpenSSL often use AES-CBC by default.
**✅ Security:**
* Much more secure than ECB.
* Still vulnerable to some attacks unless combined with authentication (see GCM).
**CFB (Cipher Feedback)**
**How it works:**
* Turns a block cipher into a stream cipher.
* Encrypts the previous ciphertext (or IV) and XORs it with plaintext.
🔄 Process:
	C0 = Encrypt(IV) XOR P0
	C1 = Encrypt(C0) XOR P1
	...

✅ Used for encrypting small units like bytes or characters.

**OFB (Output Feedback)**
**How it works:**
* Also stream-like.
* Encrypts the IV repeatedly to generate a keystream.
🔄 Process:
	O0 = Encrypt(IV)
	O1 = Encrypt(O0)
	...

	C0 = P0 XOR O0
	C1 = P1 XOR O1
	
✅ Prevents error propagation, but needs a secure IV.
**CTR (Counter Mode)**
**How it works:**
* Converts a block cipher into a stream cipher.
* Encrypts a counter value (incremented per block) and XORs it with plaintext.
🔄 Process:
	C0 = Encrypt(nonce + 0) XOR P0
	C1 = Encrypt(nonce + 1) XOR P1
	...
✅ High performance and parallelizable.
🔁 Used in many modern protocols like TLS, IPsec.

**GCM (Galois/Counter Mode)**
Adds authentication to encryption.
**How it works:**
* Uses CTR mode for encryption.
* Adds GMAC for authentication (integrity + authenticity). 
This ensures that the data is not only kept secret but also that it hasn't been tampered with during transit or storage.
✅ Preferred in most modern applications (HTTPS, secure messaging, etc).
**Nonce and Tag length in AES-GCM:**
AES-GCM uses nonce(or initialization vector) to ensure secure encryption process and a tag length which determines the size/length of the authentication tag.
Nonce is typically a random number generated for each encryption operation, often 96 bits (12 bytes) in length. 
The tag length can be adjusted based on the specific application's security requirements.
Common tag lengths in GCM include 128 bits (16 bytes, default), 120 bits, 112 bits, 104 bits, 96 bits, 64 bits, and 32 bits.
A longer tag length provides stronger security, but it also increases the overhead of the encryption process. 
**AAD (Additional Authenticated Data) in AES-GCM**
This is optional Additional data that must be authenticated but kept plaintext (e.g., headers).
**Widely Used:** AES-GCM is a widely adopted and trusted authenticated encryption scheme.  

**AES Modes Summary Table**
| Mode        | Security     | Parallelizable | Needs IV? | Authenticated? | Notes                           |
| ----------- | ------------ | -------------- | --------- | -------------- | ------------------------------- |
| **ECB**     | ❌ Weak       | ✅             | ❌        | ❌             | Don’t use unless for testing.   |
| **CBC**     | ✅ Good       | ❌             | ✅        | ❌             | Needs padding.                  |
| **CFB/OFB** | ✅ Good       | ❌             | ✅        | ❌             | Stream-friendly.                |
| **CTR**     | ✅ Very good  | ✅             | ✅        | ❌             | Fast, no padding.               |
| **GCM**     | ✅✅ Excellent| ✅             | ✅        | ✅             | Best choice for most use cases. |

**Parallelizable** means that an algorithm or task can be split into independent parts and processed at the same time, usually across multiple CPU cores or threads.
In cryptography, this refers to the ability to encrypt or decrypt multiple blocks of data simultaneously rather than one after another (sequentially).
**Some of applications of AES:**
* Wireless Security: AES is a core component of WPA2 and WPA3 protocols, securing Wi-Fi networks. 
* File and Disk Encryption: AES is used in software like BitLocker and FileVault to encrypt files and entire disks, protecting data at rest. 
* Secure Communications: AES secures online communications (HTTPS), VPNs, and messaging apps like WhatsApp and Signal. 
* Data Storage: AES encrypts data on hard drives, USB drives, and in cloud storage services like Dropbox. 
* Database Encryption: AES protects sensitive data in databases, ensuring confidentiality. 
* Password Management: AES encrypts stored passwords, enhancing security. 


**Why Hash a Secret Key in AES Encryption?**
**Code snippet example:**

	MessageDigest sha256 = MessageDigest.getInstance(SHA_CRYPT);
	byte[] keyBytes = sha256.digest(aesSecret.getBytes(StandardCharsets.UTF_8));
	SecretKeySpec aesKey = new SecretKeySpec(keyBytes, AES_ALGORITHM);

| Why Hash a Secret Key?                                               						|   |
| ----------------------------------------------------------------------------------------- | - |
| ✔️ Ensures correct key length (e.g., 256 bits for AES-256) and format requirements        |   |
| ✔️ Normalizes arbitrary strings into valid cryptographic keys        						|   |
| ✔️ Adds randomness and reduces predictability                        						|   |
| 🚫 Not hashing could cause key size errors or weak security          						|   |
| 🔐 Better yet: use a **KDF** (e.g., PBKDF2) instead of plain hashing 						|   |

**KDF (Key Derivation Function) is stronger than hashing**
In cryptography, a Key Derivation Function (KDF) is a function that takes an input secret (like a password or a master key) and transforms it into a cryptographically strong key suitable for use in other cryptographic operations (like encryption or authentication).
**Short definition** A KDF is a cryptographic algorithm that generates secure keys from a primary secret like a password or master key.
**KDF uses:**
* **Cryptographic Key Derivation:** KDFs are used to create keys suitable for use with symmetric encryption algorithms like AES.
* **Password Storage:** KDFs are crucial for securely storing passwords in databases. Hashing and storing passwords (with salt) in authentication systems.
* **Key expansion:** Derives multiple cryptographically strong keys from a single high-entropy shared secret (used in protocols like TLS, Signal, etc).
* **Key Stretching:** KDFs are often used to "stretch" passwords, making them more resistant to brute-force attacks. This is done by making the KDF computationally expensive(Add salt + multiple iterations). 
* **Key Agreement Protocols:** KDFs are used in protocols like Diffie-Hellman to derive a shared secret key between two parties.
* **Deterministic key generation:** Generates repeatable keys for the same password+salt, often in secure backups or vaults.

**Common KDFs**
| KDF        | Description                              | Strengths                                  |
| ---------- | ---------------------------------------- | ------------------------------------------ |
| **PBKDF2** | Password-Based Key Derivation Function 2 | Widely used, adjustable iterations         |
| **bcrypt** | Adds computational cost + salt           | Very slow = strong against brute-force     |
| **scrypt** | Adds memory hardness                     | Good for defense against ASICs/GPU attacks |
| **HKDF**   | HMAC-based KDF, used in TLS/Signal       | For key expansion from a shared secret     |


**2. Stream Ciphers**
Stream ciphers encrypt data one bit or byte at a time.
**Keystream generation:** They use a keystream, a pseudorandom sequence generated from a secret key, to encrypt and decrypt the plaintext.
**Encryption process:** This keystream is then combined with the plaintext using a simple operation, like XOR, to produce ciphertext. 
**Decryption process:** The same keystream and the same XOR operation are used to decrypt the ciphertext and recover the original plaintext. 
**Common/widely used ciphers:**
* Rivest Cipher 4 (RC4): used in some legacy systems, but newer protocols often avoid it since it is now considered less secure due to known vulnerabilities.  
* Salsa20: considered a modern alternative to RC4.  
* ChaCha20: another modern alternative to RC4
**Advantages:** Efficient for real-time data processing(like voice and video transmission) due to their speed and simplicity and can handle variable-length data.
**Disadvantages:** Can be more vulnerable to certain attacks if the keystream is not properly generated. 

## Hashing
Hashing is a process that converts data of any size into a fixed-length, string of characters which appears random.
The resulting string is called a hash or hash value or digest.
Hashing is a one-way process, meaning you can't derive the original data from the hash. 
Even minor changes to the input data result in a significantly different hash value (avalanche effect).

Illustration:

	Input: password123
	Hash:  ef92b778bafe771e89245b89ecbcff69a4c18f42cc83a1a2a9b9d7e75857a52a

	Input: password124
	Hash:  3d7f5bf5bb6d96a2f19c08d81ca7a0efaaeb80e3ff9f32d1e56212e2b6ccff62
	
Common hashing algorithms include Secure Hash Algorithm(SHA) eg. SHA512 and Bcrypt

**Uses of Hashing in Cybersecurity**
* **Storing passwords securely:** Instead of storing passwords directly, websites often store the hash of the password possibly with a salt(salting). 
* **Digital Signatures:** Hashing is used to verify the authenticity and integrity of digital documents and software.
* **Verify data integrity:** Hashing can be used to verify that a file or message has not been altered during transmission or storage. 

## Salting
Salting is adding a random string of characters, called a salt, to a password before hashing it.
This makes it significantly more difficult for attackers to crack passwords, using precomputed hash attacks (rainbow tables), even if they have access to a database of hashed passwords.
**Rainbow table:** is a precomputed table for caching the outputs of a cryptographic hash function, usually for cracking password hashes. It is used in rainbow table attacks.
Salting ensures that even if two users use the same password, their hashed passwords will be different due to the unique salt added to each. 

Example:

	Password: password123
	Salt: randomSalt123
	Hash: SHA-256(password123randomSalt123)

## What is a Signature/digital signature in Cybersecurity?
A digital signature is a cryptographic technique that proves two key things about a digital message or document:
1. **Authenticity:** The message really comes from the claimed sender.
2. **Integrity:** The message hasn’t been altered or tampered with since it was signed.

It’s created by hashing the data and then encrypting the hash(sign) with a private key.
In short a signature guarantees who sent the message and that it hasn’t been altered.
Below is how digital signature works:
* The sender uses their private key (in asymmetric cryptography) or a secret key (in symmetric schemes) to create a signature over the message.
* This signature is a unique string generated by applying a cryptographic algorithm with the private/secret key on the message’s content/data.
* Anyone with the corresponding public key (or shared secret) can decrypt the signature and verify it and confirm that:
	* The message hasn’t changed.
	* It was signed by the holder of the private key.

Illustration:

	Data ----> Hash ----> Encrypt Hash with Private Key ---> Digital Signature

	Receiver:
	Data + Signature ----> Hash Data & Decrypt Signature with Public Key
	Compare both hashes -> If equal, signature is valid.
	
	
**HMAC (Hash-based Message Authentication Code)** is a cryptographic tool used to verify the integrity and authenticity of a message.
It uses a cryptographic hash function on the message, combined with a secret key, to generate a unique message authentication code (MAC). 
This MAC is then attached to the message and sent to the recipient, who can use the same secret key to verify the message's origin and ensure that it hasn't been tampered with. 

**Ed25519** is a digital signature algorithm that uses the **Curve25519 elliptic curve** and the **Edwards-curve Digital Signature Algorithm (EdDSA)** to create secure digital signatures.
**PS256** is a digital signature algorithm based on RSA. **RSASSA-PSS (RSA Signature Scheme with Appendix – Probabilistic Signature Scheme) using SHA-256**
**ES256** is a digital signature algorithm based on elliptic curve cryptography (ECC). ***Elliptic Curve Digital Signature Algorithm (ECDSA) using the P-256 curve and SHA-256*
Also referred to as: ECDSA(P-256, SHA-256)
	
Common Symmetric Signature algorithms(Both sign and verify with the same secret key):

| Algorithm | Name           | Hash Function Used | Key Type |
| --------- | -------------- | ------------------ | -------- |
| `HS256`   | HMAC + SHA-256 | SHA-256            | Secret   |
| `HS384`   | HMAC + SHA-384 | SHA-384            | Secret   |
| `HS512`   | HMAC + SHA-512 | SHA-512            | Secret   |

Common Asymmetric signature algorithms(Sign with private key, verify with public key):

| Algorithm | Name                 | Type          | Hash Used | Notes                                           |
| --------- | -------------------- | ------------- | --------- | ----------------------------------------------- |
| `RS256`   | RSA + SHA-256        | RSA           | SHA-256   | Common for OAuth2                               |
| `RS512`   | RSA + SHA-512        | RSA           | SHA-512   | Stronger hash                                   |
| `PS256`   | RSASSA-PSS + SHA-256 | RSA (PSS)     | SHA-256   | More secure variant of RSA                      |
| `PS512`   | RSASSA-PSS + SHA-512 | RSA (PSS)     | SHA-512   | Very strong security                            |
| `ES256`   | ECDSA + SHA-256      | EC (Elliptic) | SHA-256   | Compact, fast, modern                           |
| `Ed25519` | EdDSA + Ed25519      | EC (EdDSA)    | SHA-512   | Very fast, secure, widely used modern signature |



## Google Tink
Google Tink is a multi-language, cross-platform , open source cryptographic library developed by Google.
It provides secure and easy-to-use APIs for various cryptographic operations.
Tink's goal is to simplify the use of cryptography while minimizing the risk of common pitfalls.
Tink supports essential cryptographic operations(also known as primitives):
* Symmetric and Asymmetric Encryption
* Digital Signatures
* MAC (Message Authentication Codes)
* AEAD (Authenticated Encryption with Associated Data)
* Hybrid Encryption
* Streaming Encryption
* PRF (Pseudo-Random Function)
* Key Rotation and Management

## Authentication
Authentication is the process of verifying the identity of a user, device, or system before granting access.

**Types of authentication**
* **Password based authentication:** This is the most common method, where users provide a username and password to verify their identity. 
* **Multi-factor authentication (MFA):** requires users to provide multiple verification factors(two or more independent ways to verify a user), in addition to a password, to access a system or account. These factors are typically things the user knows (like a PIN or password), something they have (like a phone or token), or something they are (like a biometric scan). 
MFA adds an extra layer of security, making it harder for unauthorized individuals to gain access, even if they have compromised one factor. 
* **Biometric authentication:** This uses unique physical characteristics like fingerprints, facial recognition, or voice recognition to verify identity. 
* **Certificate-based authentication:** This method uses digital certificates to verify identity, similar to how a driver's license is used in the physical world.
* **Token-based authentication:** enables users to enter their credentials once and receive a unique encrypted string of random characters(the token) in exchange. The token is used to access protected systems instead of entering your credentials all over again.
The digital token proves that you already have access permission. Use cases of token-based authentication include RESTful APIs that are used by multiple frameworks and clients.

## Authorization
Authorization is the process of verifying and granting a user or system the permission to access specific resources or perform specific actions.
(**Short definition:** Determining what an authenticated user is allowed to do — access control. E.g., user can view files but not delete them.)
It builds upon authentication, which verifies the user's identity, and determines what resources they are allowed to interact with and what actions they can take. 

**Key concepts in authorization**
* **Authentication vs. Authorization:** Authentication verifies who a user is, while authorization determines what they are allowed to do. 
* **Permissions:** Authorization is based on user permissions, which define what a user can access and what they can do with that access. 
* **Access control:** Authorization implements access control mechanisms to restrict access to sensitive resources and enforce security policies. 
**Access control:** is the process of restricting access to resources, like data, applications, or networks, ensuring only authorized individuals or systems can view or use them.
**Access Control Models:** Common types of access control/authorization methods include Role-Based Access Control (RBAC), Mandatory Access Control (MAC), and Discretionary Access Control (DAC). 
* **Authentication and Authorization in the AAA Model:** Authentication, authorization, and accounting (AAA) work together to manage user access and activity within a system, with authentication occurring first, followed by authorization and then accounting (tracking activity).

## Man-in-the-Middle (MITM) Attack
A man-in-the-middle(MITM) attack, or on-path attack, is a cyberattack where the attacker secretly relays(forwards) and possibly alters the communications between two parties who believe that they are directly communicating with each other, where in actuality the attacker has inserted themselves between the two parties.
(**Short definition:** is where an attacker secretly intercepts/eavesdrops on communication between two parties, possibly altering it.)

Some ways of preventing MITM attacks:
* Use encryption (TLS/SSL)
* Use certificates to verify identity

## Side-Channel Attack
A side-channel attack is a type of cyberattack that attempts to extract secret information (like passwords, cryptographic keys, etc.) by observing physical or behavioral characteristics of a system rather than exploiting bugs in the code or algorithm itself.

It’s like learning someone’s ATM PIN by watching their hand movements and not by hacking the ATM software.

**Types of Side-Channel Attacks**

| Type                      | Description                                                   |
| ------------------------- | ------------------------------------------------------------- |
| **Timing attacks**        | Observing how long operations take to infer data              |
| **Power analysis**        | Measuring power consumption to guess internal operations      |
| **Electromagnetic leaks** | Monitoring EM signals from the device to infer data           |
| **Acoustic analysis**     | Listening to CPU noise or keystrokes to derive sensitive info |
| **Cache attacks**         | Exploiting CPU cache behavior (flush, hit/miss times)         |

**A timing side-channel attack** is a type of side-channel cyber attack that exploits differences in execution time of cryptographic operations to infer sensitive information about the system or the data being processed. 

### Example: Timing/Timing side-channel Attack on String Comparison

Imagine you have code like this:

	public boolean isPasswordCorrect(String inputPassword) {
		String actualPassword = "SuperSecret";
		return inputPassword.equals(actualPassword);
	}

Let’s assume under the hood, equals() checks one character at a time and returns false as soon as it finds a mismatch.

**Attack Strategy**
An attacker can send thousands of guesses, measure how long the system takes to respond, and infer:
* If the response takes longer, it means more characters matched.
* They can guess the password one character at a time.

This is a timing side-channel attack.

**Realistic Code Demonstration (vulnerable version)**

	public boolean isEqual(String a, String b) {
		if (a.length() != b.length()) return false;
		for (int i = 0; i < a.length(); i++) {
			if (a.charAt(i) != b.charAt(i)) return false;
		}
		return true;
	}

* This returns immediately on mismatch.
* If an attacker times how long it takes to return false, they can guess how many characters matched before it failed.

**Secure (Constant-Time) Version**

	public boolean isEqualSecure(String a, String b) {
		if (a.length() != b.length()) return false;
		int result = 0;
		for (int i = 0; i < a.length(); i++) {
			result |= a.charAt(i) ^ b.charAt(i);
		}
		return result == 0;
	}

* It checks all characters regardless of mismatch, making timing attacks much harder.
* This is called constant-time comparison.




## TLS/SSL
SSL (Secure Sockets Layer), and its more modern and secure replacement, TLS (Transport Layer Security), ensure secure communication over the internet or a computer network.
They encrypt data, authenticate the identity of servers, and verify the integrity of the data being transmitted. 
**What SSL/TLS provides:**
* **Encryption(confidentiality):** SSL/TLS encrypts data, making it unreadable to anyone who intercepts it without the proper key. 
This is crucial for protecting sensitive information like passwords, credit card details, and personal messages. 
* **Authentication(Authenticity):** SSL/TLS certificates, issued by trusted Certificate Authorities (CAs), verify the identity of the server. 
This ensures that users are actually connecting to the legitimate website or application, preventing phishing and other security risks. 
* **Integrity:** SSL/TLS ensures that the data transmitted remains unchanged during transit. 
This prevents hackers from modifying the data in transit and then passing it on to the user, a technique known as a man-in-the-middle attack. 

SSL is an older protocol, while TLS is its more modern, secure successor.
While the term "SSL" is often used colloquially, most modern systems now use TLS.

SSL/TLS is the foundation of HTTPS (Hypertext Transfer Protocol Secure), the protocol that secures web connections.
When you see "https://" in a web address, it indicates that the connection is secured by SSL/TLS.

SSL/TLS uses a "handshake" process to establish a secure connection. 
During this handshake, the client and server exchange cryptographic keys to create a shared secret key for encrypting the data.

**Uses of SSL/TLS:** SSL/TLS is widely used for securing web browsing(HTTPS), email communication, and other applications that require secure data transmission. 

## JWT

### What is JWT?
JSON Web Token (JWT) is an open standard that defines a compact(small & efficient) and self-contained(carrys all the information/claims) way for securely transmitting information between parties as a JSON object. 
This JSON object is the JWT Claims Set. A claim is represented as a name-value pair that contains a Claim Name and a Claim Value. The JSON object can contain zero or more claims.

A JWT is represented as a sequence of URL-safe(can be included in the url without extra encoding) parts separated by period (’.’) characters. Each part contains a base64url-encoded value.
The number of parts in the JWT is dependent upon the type of token: 3 for JWS and 5 for JWE.

### Types of JWT

#### JSON Web Signature(JWS)
JWS is the most common type of JWT, which is signed(a signature has been applied to the header and payload) to ensure integrity and authenticity.
The information(JSON object) can be verified and trusted because it is digitally signed.
JWS can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA.

The content or claims of the JWS are readable by other parties as well(no confidentiality). Hence, a JWS can be used to verify the integrity of the content or claim but it should not be used to transfer sensitive data like passwords. 
JWS is typically used over HTTPS or SSL because it does not inherently prevent the data from being read.

JWS has 3 parts all base64url-encoded and separated by periods:  Header.Payload.Signature

example:

	eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
	eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.
	SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

**Header** is a JSON object that typically contains two properties: The type of token (JWT) and the encryption algorithm used (e.g., HMAC SHA256, RSA, etc). 

Example of JSON header:

	{
	  "alg": "HS256",
	  "typ": "JWT"
	}

**Payload** is another JSON object which contains the data/Claims set.
There are three types of claims: registered, public, and private claims.
	* **Registered: ** These are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims. Some of them are: iss (issuer), exp (expiration time), sub (subject), aud (audience) etc.
	* **Public: ** These are custom claims intended to be understood across systems, outside your own app. To avoid name collisions, they should be registered in the IANA JWT Claims registry or use a collision-resistant namespace (like a URI).
	* **Private: ** Custom claims defined and used only by your app or organization.
	
An example payload could be:

	{
	  "sub": "1234567890",
	  "name": "John Doe",
	  "admin": true
	}

**Signature** is created by signing the Base64Url encoded header and payload with a private/secret key and the algorithm specified in the header.

For example, if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:

	HMACSHA256(
	  base64UrlEncode(header) + "." +
	  base64UrlEncode(payload),
	  secret)

### JSON Web Encryption(JWE)
This is an encrypted JWT, used when you want the payload to be confidential (not just signed).
It guarantees both integrity and confidentiality of the data.
It can be used over plain HTTP as it is inherently encrypting the content.

JWE consists of 5 base64url-encoded parts separated by periods: 
<Protected Header>.<Encrypted Key>.<Initialization Vector>.<Ciphertext>.<Authentication Tag>

Example:

	eyJhbGciOiJSU0EtT0FFUCIsImVuYyI6IkEyNTZHQ00ifQ.
	OKOawDo13gRp2ojaHV7LFpZcgV7T6DVZKTYzRjlao1M.
	48V1_ALb6US04U3b.
	5eym8TW_c8SuK0ltJ3rpYIzOeDQz7zF6AnvGLMvPZB8.
	XFBoMYUZodetZdvTiFvSkQ



**Note:** JWE does not guarantee authenticity by itself, unless it’s combined with a signing mechanism (like JWS or using authenticated key exchange).

## What is JSON Web Key(JWK) and JSON Web Key Set(JWKS)
JWK (JSON Web Key) is a standardized, JSON-based format for representing a cryptographic key.
JWKS (JSON Web Key Set) is a JSON object that contains a collection of JSON Web Keys(JWKs).
**JWK**
It represents a cryptographic key, including public and private keys.
It is used to define a consistent way to represent keys in a machine-readable format, particularly in web applications and services. 
Public keys can be exposed via JWKS endpoint/uri.
The keys can be used to verify JWTs signed with RS256, PS256, etc.
**Use cases** used in many modern identity and security protocols (like OAuth 2.0, OpenID Connect, and JWTs).

**Key Components of a JWK**
Here’s an example of an RSA public key in JWK format:

	{
	  "kty": "RSA",
	  "use": "sig",
	  "alg": "RS256",
	  "kid": "abc123",
	  "n": "0vx7...4E",
	  "e": "AQAB"
	}

Key fields:

| Field | Description                                                     |
| ----- | --------------------------------------------------------------- |
| `kty` | Key type: `"RSA"`, `"EC"` (elliptic curve), `"oct"` (symmetric) |
| `use` | Intended use: `"sig"` (signature) or `"enc"` (encryption)       |
| `alg` | Algorithm the key is meant to use (e.g., `"RS256"`, `"PS256"`)  |
| `kid` | Key ID — helps identify the key                                 |
| `n`   | RSA modulus (Base64URL-encoded)                                 |
| `e`   | RSA public exponent (usually `"AQAB"` for 65537)                |

If it’s a private key, additional fields like d, p, q, etc. are included.

**JWKS**
It's commonly used to store public keys for verifying JWTs.

Example:

	{
	  "keys": [
		{
		  "kty": "RSA",
		  "kid": "key1",
		  "use": "sig",
		  "alg": "RS256",
		  "n": "...",   // modulus
		  "e": "AQAB"   // exponent
		}
	  ]
	}

***JWK and JWKS real life Example:*
Imagine a website using JWTs for authentication. 
The website's server might use a private key to sign JWTs, and the public key corresponding to that private key would be stored in a JWKS. 
Clients can then use this public key to verify the authenticity of the JWTs received from the server. 

## What is JSON Object Signing and Encryption (JOSE)
JOSE is a framework/suite of standards that provide a way to securely transfer information(by signing and encryption) between parties, typically for use in authentication, authorization, and secure communication systems (like OAuth2, OpenID Connect, JWT, etc.).
It's built on JSON and Base64, making it easy to use in web applications. 
It consists of several upcoming RFCs:

| JOSE Standard | Purpose                                                                      | Spec      |
| ------------- | ---------------------------------------------------------------------------- | ----------|
| **JWS**       | JSON Web Signature — *producing and handling digitally signed messages*      | [RFC 7515]|
| **JWE**       | JSON Web Encryption — *producing and handling encrypted messages*            | [RFC 7516]|
| **JWK**       | JSON Web Key — *format and handling of cryptographic keys*                   | [RFC 7517]|
| **JWA**       | JSON Web Algorithms — *algorithms used in JOSE for signing and encryption*   | [RFC 7518]|
| **JWT**       | JSON Web Token — *representation of claims as JSON, protected by JWS or JWE* | [RFC 7519]|


## What is Privacy-Enhanced Mail(PEM)
PEM is a base64-encoded format used to store and share cryptographic material like certificates,keys and other data.
**Initial purpose** It was initially designed for secure email but is now widely used for storing and exchanging keys and certificate.
It is commonly used in TLS/SSL (e.g., HTTPS) for storing private keys, public keys, and X.509 certificates.

**Example:**
A PEM file might contain a private key, a public key, or a certificate. 
Public Key (RSA) in PEM format:

	-----BEGIN PUBLIC KEY-----
	MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A...
	-----END PUBLIC KEY-----
	
## What is X.509 and (Public Key Cryptogrphy Standards)PKCS#8
**X.509** is a standard for public key certificates and the structure of public keys.
It defines the format and structure of these digital documents.
**Think of X.509 as:** A container for public key information (key + algorithm + encoding)

**Format:** Used for public keys, typically wrapped in:

	-----BEGIN PUBLIC KEY-----
	(Base64 data)
	-----END PUBLIC KEY-----


**PKCS#8** is a standard within the Public-Key Cryptography Standards (PKCS) family for storing private keys.
**Think of PKCS#8 as:** A container for private key information (plus algorithm, securely packaged)

**Format:** Used for private keys, typically wrapped in:

	-----BEGIN PRIVATE KEY-----
	(Base64 data)
	-----END PRIVATE KEY-----

## OAuth2 (Open Authorization 2.0)
OAuth 2.0 is an authorization framework that allows users to grant third-party applications access to their resources(eg. email, contacts and other data) on another service(i.e resource server), without sharing their credentials. 
It is a widely used standard for securing access to APIs and enabling "secure delegated access" to services like Google, Facebook, and GitHub.
For example:
> Let’s say you want to use a calendar app that integrates with your Google Calendar. Instead of giving the calendar app your Google username and password (which is risky), OAuth2 allows Google to give the app a token that grants access only to your calendar and only for a specific time, without exposing your login credentials.

**Key Concepts in Oauth2**
* **Resource Owner:** The user who owns the data and grants access to it.
* **Resource Server:** The server where the user's data resides (e.g., Google Calendar API).
* **Client:** The application wanting to access the user's resources (e.g., the calendar app). The application’s access to the user’s account is limited to the scope of the authorization granted (e.g. read or write access)
* **Authorization Server:** The server that authenticates the user and issues access tokens (e.g., Google OAuth server).
* **Access Token:** A credential that a client uses to access protected resources on behalf of the resource owner.
* **Refresh Token:** A long-lived token that can be used to obtain new access tokens when the old ones expire.
* **Scope:** Defines the specific permissions granted to the client (e.g., read only access to email, or write access to social media posts). 

The most common oauth2 flows(or grant types) are the Authorization Code flow, Implicit flow, Resource Owner Password Credentials flow, and Client Credentials flow.
Other flows include the Hybrid flow and Device Authorization flow.
 
Here's a breakdown of the main OAuth 2.0 flows:
**Authorization Code Flow:**
This is the most commonly used and recommended flow for web applications.
It involves an authorization code being exchanged for an access token, enhancing security by keeping the access token hidden from the client-side.
**Purpose:** Most secure flow; used by web apps, mobile apps, and SPAs.
**Implicit Flow(Deprecated):**
Like authorization code grant, implicit grant redirects the user’s browser to the authorization server to get user consent.  
But when redirecting back, rather than provide an authorization code in the request, the access token is granted implicitly in the request.
**Purpose:** Designed for SPAs where tokens are returned directly in the redirect URI.
This flow is not generally recommended anymore(insecure — tokens exposed in browser), and authorization code grant is preferred.
**Resource Owner Password Credentials (ROPC) Flow:**
This flow requires the client to obtain the user's credentials (username and password) and directly exchange them for an access token.
This flow seems suitable for clients that are not browser based, but modern applications often favor asking the user to go to a website in their browser and perform authorization code grant to avoid having to handle the user’s credentials.
It is generally not recommended unless there are specific reasons to use it, as it compromises security. 
**Purpose:** Allows the app to collect the user's username and password directly.
**Client Credentials Flow:**
This flow is like user credentials grant, except that instead of exchanging a user’s credentials for an access token, the client exchanges its own credentials for an access token. 
**Purpose:** Used for server-to-server (machine-to-machine) communication.
**Hybrid Flow:**
This flow combines aspects of the Authorization Code and Implicit flows, offering a balance of security and convenience, often used in conjunction with OpenID Connect. 
It allows clients to receive an ID token (for user identification) and an authorization code (for retrieving access and refresh tokens) in the initial authorization response.
This means the client can immediately verify the user's identity while still securely obtaining access and refresh tokens through a back-channel exchange. 
**Purpose:** SPAs or web apps that want to start interacting with the user right after login (with an ID token) but also complete token exchange on the backend for better security.
**Device Authorization Flow/Device Flow:**
This flow is designed for devices with limited input capabilities or no browser, such as smart TVs or IoT devices. 
It involves obtaining a device code and user verification on a separate device.


**How OAuth 2.0 Authorization Code flow Works**
1. **User Initiates Access:** A user wants to use a third-party application (like a social media app) that needs access to resources on another service (like Google).
2. **Redirection to Authorization Server:** The application redirects the user to the authorization server (e.g., Google's authorization server). 
3. **User Authentication and Consent:** The user authenticates with the authorization server (enters their Google credentials) and grants permission (scopes) to the third-party application. 
4. **Authorization Code:** The authorization server issues an authorization code to the application. 
5. **Access Token Exchange:** The application exchanges the authorization code, along with its client ID and secret, for an access token at the authorization server's token endpoint. 
6. **Resource Access:** The application uses the access token to access the user's resources on the resource server (e.g., Google's API). 
7. **Token Expiration and Refresh:** Access tokens typically have a limited lifespan. A refresh token can be used to obtain a new access token without requiring the user to re-authenticate. 

**How OAuth 2.0 Hybrid flow Works (simplified)**
1. **Initial Request:** The client sends an authorization request to the authorization server, specifying the desired scopes and requesting an ID token and an authorization code.
2. **User Authentication:** The user authenticates with the authorization server.
3. **Authorization Response:** The authorization server redirects the user back to the client, including the ID token and authorization code in the response. 
4. **Token Exchange:** The client, using the authorization code, makes a back-channel request to the token endpoint to retrieve access and refresh tokens. 

**Benefits of Hybrid flow**
* Improved User Experience: The immediate availability of an ID token allows for faster user identification and potentially a faster initial page load.
* Enhanced Security: The back-channel token exchange for access and refresh tokens ensures that sensitive token information is not exposed in the browser's URL or history.
* Flexibility: Hybrid flows offer a balance between the security of the authorization code flow and the speed of the implicit flow, making them suitable for a wider range of applications. 

## OpenID Connect (OIDC)
**OpenID Connect (OIDC)** is an authentication protocol that builds on top of OAuth 2.0. 
While OAuth 2.0 is used for authorization, OIDC adds capabilities for authentication — that is, verifying who the user is.
It allows third-party applications to verify user identities and obtain basic profile information, enabling single sign-on (SSO) and other identity-related services. 
**Key Terms in OIDC**
| Term                        | Description                                                                                                                                              |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ID Token**                | A JWT (JSON Web Token) that contains identity information about the user, issued by the Identity Provider (IdP).                                         |
| **Access Token**            | Used to access protected APIs/resources, including the **UserInfo Endpoint**.                                                                            |
| **Refresh Token**           | Used to get new access tokens without re-authenticating.                                                                                                 |
| **Authorization Code Flow** | A secure flow recommended for web and mobile apps; involves redirecting users to the IdP, getting an authorization code, and exchanging it for tokens.   |
| **Identity Provider (IdP)** | The service that authenticates users and issues tokens (e.g., Google, Okta).                                                                             |
| **Relying Party (RP)**      | The application that relies on the IdP to authenticate users.                                                                                            |
| **Discovery Document**      | A JSON file (`.well-known/openid-configuration`) that describes the IdP’s endpoints and capabilities.                                                    |
| **UserInfo Endpoint**       | An OAuth 2.0 protected resource that returns additional claims (like name, email, etc.) about the authenticated user when accessed with an access token. |

**Typical Flow (OIDC Authorization Code Flow)**
1. User clicks "Log in with X".
2. Browser is redirected to IdP (e.g., Google).
3. User logs in and consents.
4. IdP redirects back to your app with a code.
5. App exchanges code for an ID Token and Access Token.
6. App uses the ID Token to get user info and log them in

**OIDC (OpenID Connect) compliant** means an application or service adheres to the specifications of the OpenID Connect protocol, enabling it to securely verify user identities and provide user information.
To be OIDC compliant, an identity provider (or a client library) must:
* **Implement Required OIDC Flows:**
	* Most commonly: Authorization Code Flow (with support for PKCE in public clients).
	* Others include: Implicit Flow (deprecated), Hybrid Flow, etc.
* **Support Required Endpoints (per discovery document):**
	* /.well-known/openid-configuration (Discovery Document)
	* /authorize (Authorization Endpoint)
	* /token (Token Endpoint)
	* /userinfo (UserInfo Endpoint)
	* /revocation and /introspection (for OAuth 2.0 token lifecycle, optional but recommended)
* **Issue Proper Tokens:**
	* ID Token in JWT format
		* Contains required claims like iss (issuer), sub (subject), aud (audience), exp (expiration), etc.
	* Access Token (used to access APIs)
	* Refresh Token (if applicable)
* **Use Standard Scopes and Claims:**
	* Must support at least:
		* openid (required)
		* profile, email, address, phone (optional but common)
	* Support for standard claims like name, email, sub, preferred_username, etc.
* Use Standard Security Practices:
	* Support for HTTPS
	* Token signing (usually RS256)
	* Optional: token encryption
* Provide the Discovery Document:
	* Hosted at https://<issuer>/.well-known/openid-configuration
	* Includes URLs of endpoints, supported scopes, claims, key sets, etc.

**Examples of OIDC-Compliant Providers**
| Provider      | Compliance Details                                                        |
| ------------- | ------------------------------------------------------------------------- |
| **Google**    | Fully OIDC compliant, widely used for "Login with Google"                 |
| **Microsoft** | Azure AD supports OIDC; provides discovery documents and conforms to spec |
| **Okta**      | OIDC-compliant; supports all major flows and dynamic client registration  |
| **Auth0**     | Fully compliant; also supports advanced customization                     |
| **Keycloak**  | Open source IdP; supports OIDC and SAML                                   |



## Web Security
**1. Same-Origin Policy (SOP)**
SOP is a browser security model that restricts how a web page from one origin can interact with a web page from a different origin.
It helps prevent malicious websites from accessing sensitive data on other websites, thereby enhancing security and privacy. 
An origin is defined by the combination of:
* Protocol (e.g., http or https)
* Host (domain name, like example.com)
* Port (e.g., 80, 443, or custom)
Two URLs have the same origin if all three parts match exactly.

**Example:**
If a script on https://example.com tries to access data from https://anothersite.com, the browser will enforce the same-origin policy.
Because the origins differ (different hostnames), the script will be restricted from accessing data or performing actions on https://anothersite.com. 

🛡️ Purpose
The Same-Origin Policy is designed to:
* Protect user data from malicious websites
* Prevent cross-site scripting (XSS) and cross-site request forgery (CSRF) attacks
* Ensure that scripts can't snoop on or manipulate data from other sites

✅ Allowed Cross-Origin Interactions
SOP is strict but not absolute. There are safe, controlled ways to allow cross-origin access:
* CORS (Cross-Origin Resource Sharing) – allows servers to declare allowed cross-origin requests.
* PostMessage API – allows communication between windows/frames from different origins.
* JSONP – older, limited method for cross-domain requests (GET only).

**2. Cross-Origin Resource Sharing (CORS)**
Cross-Origin Resource Sharing (CORS) is a security feature implemented by web browsers that allows a web page from one origin to request resources from a different origin, only if the target server explicitly allows it.
**Short definition**  A mechanism that lets servers define which domains are allowed to access their resources from a different origin.
CORS is essentially a relaxation of the Same-Origin Policy, enabling controlled access to cross-origin resources.

**Example:**
* Imagine a website (e.g., `https://www.example.com`) needs to display data from an API located on a different domain (e.g., `https://api.example.com`).
* Without CORS, the browser would block the request from `https://www.example.com` to `https://api.example.com`.
* To enable this, the server at `https://api.example.com` would need to be configured to include `Access-Control-Allow-Origin: https://www.example.com`

**How It Works (Basic Flow)**
* A browser sends a cross-origin HTTP request (e.g., with fetch or XMLHttpRequest).
* The server at the target origin responds with specific HTTP headers like:
	* Access-Control-Allow-Origin
	* Access-Control-Allow-Methods
	* Access-Control-Allow-Headers
If the CORS headers match the browser's expectations, the browser allows the response to be read by the calling script.

**✅ Simple CORS Example**
**👨‍💻 JavaScript Code (Client: https://example.com)**

	fetch('https://api.otherdomain.com/data')
	  .then(response => response.json())
	  .then(data => console.log(data))
	  .catch(error => console.error('Error:', error));

**🌐 Server Response (from https://api.otherdomain.com)**


	HTTP/1.1 200 OK
	Access-Control-Allow-Origin: https://example.com
	Content-Type: application/json

	{ "message": "Hello from otherdomain.com!" }

Here, the server explicitly allows https://example.com to access the resource.

**Important CORS Headers**
| Header                             | Purpose                                                                   |
| ---------------------------------- | ------------------------------------------------------------------------- |
| `Access-Control-Allow-Origin`      | Specifies which origins are allowed (e.g., `*`, or `https://example.com`) |
| `Access-Control-Allow-Methods`     | Allowed HTTP methods (`GET`, `POST`, etc.)                                |
| `Access-Control-Allow-Headers`     | Which custom headers can be used in the actual request                    |
| `Access-Control-Allow-Credentials` | Whether to allow credentials (cookies, HTTP auth)                         |

**What is preflight request in CORS**
A **preflight request** is a mechanism used in cross-origin resource sharing (CORS) where a browser sends an HTTP OPTIONS request to the server before making the actual request. 
**Purpose** This preliminary request checks if the server is aware of CORS and if it will allow the subsequent request.
It's a way for the browser to ensure the cross-origin request is safe before sending sensitive data. 
**When preflight request is used:** Preflight requests are triggered when the request method is not GET, POST, or HEAD, or when custom headers are used in the request
or when sending credentials.
**How preflight request works:**
* When a browser encounters a cross-origin request that requires a preflight check, it first sends an OPTIONS request to the server. This OPTIONS request includes headers like:
	* Origin: Specifies the origin (domain) of the client making the request. 
	* Access-Control-Request-Method: Indicates which HTTP method (e.g., PUT, DELETE) will be used in the actual request. 
	* Access-Control-Request-Headers: Specifies which custom headers will be included in the actual request. 
* The server then responds to the OPTIONS request, indicating whether it allows the cross-origin request. This response includes headers like:
	* Access-Control-Allow-Origin: Specifies which origins are allowed to access the resource. 
	* Access-Control-Allow-Methods: Lists the allowed HTTP methods. 
	* Access-Control-Allow-Headers: Lists the allowed custom headers. 
* If the server's response to the preflight request indicates that the actual request is permitted, the browser will then send the actual request. 

**3. Cross-Site Scripting (XSS)**
Cross-Site Scripting (XSS) is a security vulnerability that allows attackers to inject malicious scripts into web pages viewed by other users.
These scripts execute in the victim’s browser and can steal data, hijack sessions, deface websites, or redirect users to malicious sites.
**How it works:**
* Attackers inject malicious scripts into a website, often through input fields, comments sections, or other areas where user-supplied data is accepted and displayed back to other users. 
* **Exploitation:** When a user visits the compromised page, their browser executes the injected script because it originates from a trusted website. 
* **Consequences:** The injected script can then perform actions on behalf of the user, such as accessing their cookies, session tokens, or other sensitive information, or even redirecting them to a different website. 
**Types of XSS:**
* **Reflected XSS (Non-persistent):** The malicious script is reflected off the web server, often in the URL or query parameters. 
**How Reflected XSS works:**
* The attacker sends a specially crafted request to the web server (often by tricking a user into clicking a malicious URL).
* The web server does not store the malicious script anywhere.
* Instead, it immediately includes the malicious input("reflects") (for example, from URL query parameters) in its response HTML.
* That response is then sent back to the user’s browser as-is, so the browser executes the malicious script.

**💻 Example: Breaking it down**
1. The attacker crafts a URL like:
	https://example.com/search?q=<script>alert('Hacked!')</script>
2. The user clicks the URL.
3. The browser sends a request to example.com with the parameter q=<script>alert('Hacked!')</script>.
4. The server takes the value of q and "reflects" it back in the HTML response page without sanitizing or escaping:
	<p>You searched for: <script>alert('Hacked!')</script></p>
5. The browser renders this HTML and runs the <script> tag, triggering the alert.

* **Stored XSS (Persistent):** The malicious script is permanently stored on the target server, such as in a database or comment section. 
**💻 Example:**
	<!-- Malicious comment stored in the database -->
	<script>alert('XSS Attack!');</script>
When any user views the page with that comment, the script runs in their browser.

* **DOM-based XSS:** The vulnerability lies in the client-side JavaScript code, where the malicious script is executed entirely within the browser without ever reaching the server. 
**💻 Example:**
	<!-- Vulnerable JavaScript -->
	<div id="output"></div>
	<script>
	  const params = new URLSearchParams(location.search);
	  document.getElementById("output").innerHTML = params.get("msg");
	</script>
**What this code does:**
* It looks at the URL, specifically the query parameter after ?.
* It takes the value of msg (e.g., msg=hello) and inserts it as raw HTML into the <div id="output">.

If someone visits: 
	https://example.com/page.html?msg=<script>stealCookies()</script>
	
Here’s what happens in the browser:
* location.search = ?msg=<script>stealCookies()</script>
* params.get("msg") = <script>stealCookies()</script>
* innerHTML = "<script>stealCookies()</script>"

🚨 That script is inserted into the DOM and executed(stealCookies() method) by the browser — **no server involved**.

**How to prevent XSS:**
* **Input validation/sanitaization:** Validating and sanitizing all user input to ensure it does not contain malicious code. 
* **Escape Output:** Always escape user input before inserting it into HTML, JS, or attributes.
**escape output:** Convert special characters in user input(eg. <,>) into harmless versions before injecting that input into the webpage.
Example (safe output):
	<!-- Output sanitized -->
	<p>User input: &lt;script&gt;alert('XSS')&lt;/script&gt;</p>
* **Content Security Policy (CSP):** A CSP can block inline scripts or restrict where scripts can load from.
Example:
	Content-Security-Policy: default-src 'self'; script-src 'self'
* **Use HTTP-only Cookies:** This prevents JavaScript from accessing session tokens via document.cookie.
* **Use Trusted Libraries and Frameworks:** Frameworks like React, Angular, and Vue automatically escape content when used correctly.

**4. Clickjacking/Click Hijacking**
Clickjacking, also known as a “UI redress attack”, is an attack where a user is tricked into clicking on something different from what they perceive on a webpage.
This is often achieved by overlaying a transparent or disguised layer over a legitimate website(usually through an invisible iframe), making the user unknowingly interact with the attacker's hidden content.  
Thus, the attacker is “hijacking” clicks meant for the legitimate page and routing them to another page, most likely owned by another application, domain, or both.
**How it works:**
* Attackers create a fake or decoy website that embeds a legitimate website (like a bank's login page) within an iframe. 
* **Overlaying:** The attacker then overlays their own elements (buttons, links, etc.) on top of the legitimate website, hiding the original elements. 
* **Tricking the user:** When a user interacts with the decoy website, thinking they are clicking on something harmless (like a button on a game), they are actually clicking on the hidden, malicious elements of the legitimate website. 
* **Consequences:** This can lead to various harmful actions, such as unknowingly liking a social media page, sharing malicious content, or even unknowingly transferring funds. 
**A real life Scenario of clickjacking:**
* You're logged into your bank in one browser tab.
* You visit a malicious website in another tab that says: 🟢 Click this button to win a free iPhone!
* Behind the scenes, that malicious site loads your bank's "Transfer Funds" page in an invisible iframe and positions the “Confirm” button directly underneath the "Free iPhone" button.
* When you click the "Free iPhone" button, you're actually clicking “Confirm Transfer” on your bank’s page.
**🎨 Visual Representation**
	<!-- Attacker's Page -->
	<button style="z-index: 2; position: absolute;">Claim Prize</button>

	<iframe src="https://bank.com/transfer?amount=10000"
			style="opacity: 0; position: absolute; top: 0; left: 0; z-index: 1;"></iframe>

The iframe is invisible (opacity: 0) and aligned behind the visible button — the user has no idea they’re clicking on a legitimate page.
**How to prevent clickjacking**
* **Use X-Frame-Options HTTP Header:** Tell browsers not to allow your site to be shown in a frame or iframe.
	X-Frame-Options: DENY
Other values:
	*DENY – Never allow framing
	*SAMEORIGIN – Only allow framing by the same domain
* **Use CSP frame-ancestors Directive:** More modern and flexible. Recommended in addition to X-Frame-Options.
	Content-Security-Policy: frame-ancestors 'self'
This means: “Only this domain can embed this site in a frame.”


**5. Content Security Policy (CSP)**
Content Security Policy is a browser security feature that helps prevent/mitigate attacks like Cross-Site Scripting (XSS) and other code injection attacks by controlling which resources the browser is allowed to load and execute.
It works by defining a set of policies through an HTTP header, instructing the browser on which sources are permitted for loading content. 
**What it does:**
* **Resource Control:** CSP primarily controls where a website can load resources from, such as scripts, stylesheets, images, and more.
* **XSS Prevention:** It's a key defense against XSS attacks, where attackers inject malicious scripts into a website. By restricting which sources are allowed, CSP makes it harder for attackers to execute their scripts.
* **Other Protections:** CSP can also help protect against Clickjacking and enforce HTTPS usage. 
**How it works:**
* **HTTP Header:** CSP is implemented as an HTTP header, usually sent from the server to the browser when a webpage is loaded.
* **Policy Directives:** The header contains directives (e.g., script-src, style-src) that specify which sources are allowed for different types of content.
* **Browser Enforcement:** The browser then uses these directives to determine if a resource is allowed to load. If a resource is loaded from an unauthorized source, the browser will block it. 
**Example:**
A typical CSP might look like this:
	Content-Security-Policy: default-src 'self'; script-src 'self' https://code.jquery.com; style-src 'self'; 
	
	* default-src 'self': This directive sets the default policy for all resource types to load from the same origin as the website.
	* script-src 'self' https://code.jquery.com: This directive allows scripts to be loaded from the same origin and from the jQuery CDN.
	* style-src 'self': This directive allows stylesheets to be loaded from the same origin.

To block all inline-script just set:

	Content-Security-Policy: script-src 'self'

If you need inline scripts you can use nonce or hash.
**✅ Using a Nonce**
A “nonce” is a unique, random token (a one-time password) that you include in both the CSP and your <script> tag.
**CSP Header Example**
	Content-Security-Policy: script-src 'self' 'nonce-abc123'
**Matching Script Tag in HTML**
	<script nonce="abc123">
	  console.log("This inline script is allowed");
	</script>

This script is allowed because the nonce (abc123) matches the one in the CSP.
If an attacker injects a script like:
	<script>alert('XSS');</script>
It won’t have the correct nonce, so it will be blocked.
**Important:** The nonce should be different (random) for every request to stop attackers from guessing it.

**✅ Using a Hash**
If your inline script is static (unchanging), you can calculate a SHA-256 hash of the script content and include it in your CSP.
**Example Script:**
	<script>
	  console.log("Hello world");
	</script>
You calculate the SHA-256 of the string:
	console.log("Hello world");
Say the hash is: sha256-AbCdEfGh...
CSP Header:
	Content-Security-Policy: script-src 'self' 'sha256-AbCdEfGh...'
Now only this exact script can run. If even one character changes, it’s blocked.
✅ Hashes are great when scripts are small and never change.

**Without CSP – XSS Risk**
	<!-- Attacker injects this -->
	<script src="https://evil.com/xss.js"></script>

If your site doesn’t have CSP, the browser will load and run it.

** With CSP – Attack Blocked**
If your CSP says script-src 'self', the browser sees: “That script is from evil.com, not self. Block it.”
And it blocks the attack completely.

**Common Directives in CSP**
| Directive                  | What It Controls                                    |
| -------------------------- | --------------------------------------------------- |
| `default-src`              | Default source for all content types                |
| `script-src`               | Allowed sources for JavaScript                      |
| `style-src`                | Allowed sources for CSS                             |
| `img-src`                  | Allowed sources for images                          |
| `object-src`               | Flash/ActiveX (deprecated, but still good to block) |
| `connect-src`              | Where XHR/Fetch/WebSockets can connect              |
| `frame-src`                | What domains can be loaded in `<iframe>`            |
| `report-uri` / `report-to` | Where to send CSP violation reports                 |


**6. Cross-Site Request Forgery (CSRF)**
Cross-Site Request Forgery (CSRF) is a type of attack that tricks a user into unknowingly submitting a malicious request to a trusted website where they’re already authenticated.
In other words, the attacker abuses the user’s session to make unauthorized actions (like changing passwords, transferring funds, or posting content), without the user’s knowledge or consent.
**How CSRF Works (Step-by-Step)**
* User logs into a legitimate site (e.g., bank.com) and gets a session cookie.
* User visits a malicious website (e.g., evil.com) in the same browser session.
* The malicious site sends a request to bank.com using the user’s credentials (cookie is sent automatically by the browser).
* Bank.com processes the request, thinking it came from the legitimate user.

**How to Prevent CSRF**
* **Use CSRF Tokens:** Generating a unique, random token for each user session and including it in forms and other requests. 
	* Only forms that include the correct token will be processed.
	* Token must be stored on the server and validated per session/request.
Example:
	<form action="/transfer" method="POST">
	  <input type="hidden" name="csrf_token" value="a1b2c3d4">
	  <input name="amount" value="100">
	</form>
* **Use SameSite Cookies:** Restricting cookies to the same site (domain) that created them, preventing them from being sent with cross-site requests. 
	Set-Cookie: sessionid=abc123; SameSite=Strict; Secure

	* SameSite=Strict: Cookies not sent on cross-site requests (best security)
	* SameSite=Lax: Allows some safe cross-site use (e.g., link clicks)
	* SameSite=None; Secure: Allows cross-site cookies only if HTTPS is used
* **Validating Referer header:** Checking the Referer header to ensure that the request is coming from the expected domain. 

**7. Inline Frame (iFrame)**
An iFrame (Inline Frame) is an HTML element that allows you to embed content from another website or page into your own.
Basic Syntax:

	<iframe src="https://example.com" width="600" height="400"></iframe>

**Security Risks with iFrames**
* Clickjacking: A malicious site embeds your website in an invisible iframe and tricks users into clicking on things (e.g., "Like" button, purchase button) that they don't see.
* Data Leak: If content inside an iframe can access window.parent, it may read or manipulate parent content.

**Protection Against iFrame Attacks**
* X-Frame-Options Header
	* X-Frame-Options: DENY – Blocks all iframe embedding.
	* X-Frame-Options: SAMEORIGIN – Allows only your own domain to embed the page.
* Content Security Policy (CSP)
Example:

	Content-Security-Policy: frame-ancestors 'self'

To allow framing by anyone: Don’t send `X-Frame-Options`, or use `CSP: frame-ancestors *`

**8. SQL Injection (SQLi)**
SQL injection(SQLi) is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database.
It consists of insertion or “injection” of a SQL query via the input data from the client to the application. 
**How It Works**
If a web application includes untrusted data (like user input) directly in a SQL query without proper validation or escaping, an attacker can inject malicious SQL code. 
This can manipulate the SQL query to perform unintended actions.

**Example**
Suppose you have the following (insecure) SQL query in a web app:

	SELECT * FROM users WHERE username = 'admin' AND password = 'password123';

This is fine if inputs are trusted—but SQL Injection happens when the attacker crafts a malicious input that manipulates the query.
Now, an attacker enters this into the password field:
		' OR '1'='1
And `admin` in the username field.
And the server-side code builds the query like this:
	SELECT * FROM users WHERE username = 'admin' AND password = '' OR '1'='1';
**Note:** the password value ' OR '1'='1 gets inserted as-is into the query string.
Since '1'='1' is always true, the whole WHERE clause becomes true, even if the username/password are wrong.
This lets the attacker log in without valid credentials.

**⚠️ Consequences of SQL Injection**
* Bypass authentication
* Read sensitive data
* Insert, update or delete data
* Execute administrative operations (such as shutdown the DBMS)
* Recover the content of a given file present on the DBMS file system
* In some cases, execute commands on the server

**How to prevent SQL injection**
* Use Prepared Statements / Parameterized Queries (e.g., in Python with sqlite3 or PHP with PDO)
* Validate and sanitize user input
* Use least privilege access for database accounts
* Use ORM frameworks that abstract SQL (like Django ORM, SQLAlchemy, Hibernate)
* Keep software and libraries up to date
* Regular security audits and penetration testing

**9. Directory Traversal/Path Traversal/Directory Climbing**
Directory traversal is a web security vulnerability that allows attackers to access files and directories outside the intended web root directory.
**How it works:**
* **User input manipulation:** Directory traversal attacks exploit vulnerabilities where user-supplied input is used to construct file paths without proper validation or sanitization.
* **".." sequences:** Attackers often use "../" (or similar) sequences to move up the directory tree and access files outside the web root. 
* **Arbitrary file access:** This can lead to the attacker gaining unauthorized access to files and directories on the server. 

**📂 Example**
Imagine a web app lets users request files like this:
	https://example.com/view?file=report.pdf
The backend might then build a path like:
	file_path = "files/" + user_input
So if user_input = "report.pdf", the full path becomes:
	files/report.pdf
But if an attacker sends:
	file=../../../../etc/passwd
The path becomes:
	files/../../../../etc/passwd
Which might resolve to:
	/etc/passwd
And now the attacker is reading sensitive OS files outside the intended files directory.

**What Attackers Can Access**
* Read sensitive system files (e.g., /etc/passwd, C:\Windows\system.ini)
* Read web server config or app source code
* Sometimes write files if the app also supports file uploads

**How to prevent path traversal**
* **Input validation and sanitization:** Thoroughly validate and sanitize all user-supplied file paths to ensure they are within the intended directory. 
* **Whitelisting:** Use whitelists to define allowed file paths or file extensions.
	allowed_files = ['report.pdf', 'summary.txt']
	if user_input in allowed_files:
		open("files/" + user_input)
* **Restricting access:** Limit the directories accessible by web applications and use proper file permissions. 
* Use file IDs instead of names in URLs.

**10. Open Redirect**
An Open Redirect is a vulnerability in a web application that allows an attacker to redirect a user to an arbitrary/malicious website.
A web application has an open redirect when it lets users specify a URL to redirect to, and the application doesn’t validate that the URL is safe or allowed.
**How it works:**
* Open redirects happen when a website's code uses user-supplied input (like a URL parameter) to determine where to send users next, without proper validation or security checks. 
* **Exploitation:** An attacker can craft a malicious URL that includes a link to a legitimate website, but also includes a parameter that redirects the user to a different, malicious site.

**Example:**
If the server-side code blindly redirects users without validation:
	redirect(user_input_url)
Then the attacker can craft a link like:
	https://example.com/redirect?url=http://phishing-site.com
When a user clicks it, they’re first sent to example.com, which seems trustworthy, but are then redirected to the malicious site.

**Security Impact**
While open redirects don’t directly compromise servers or databases, they:
* can lead to users being tricked into visiting harmful websites
* Can be used in phishing and malware attacks
* Undermine user trust
* May be exploited in OAuth redirection attacks (e.g., stealing auth tokens)

**How to prevent open redirects**
* Whitelist allowed redirect URLs: Only allow redirects to trusted paths
* Don't rely on user input for redirects unless absolutely necessary

**11. Insecure Deserialization**
Insecure deserialization is a web application security vulnerability that occurs when an application deserializes untrusted data without proper validation,
potentially leading to remote code execution, data tampering, or denial of service.
If the application blindly trusts the source of this data, an attacker can inject malicious code disguised as a legitimate object. 
**What Is Deserialization?**
**Serialization** = converting objects (like a Python dictionary or a Java object) into a string or byte format to store or send.
**Deserialization** = converting that string or byte data back into an object.

**What Is Insecure Deserialization?**
It’s insecure when:
* The app accepts user-controlled serialized data
* Then blindly deserializes it without validation
* Allowing attackers to inject malicious objects

**✅ Example (Python):**
	import pickle

	data = {'user': 'admin'}
	serialized = pickle.dumps(data)           # ➜ Converts object to byte stream
	deserialized = pickle.loads(serialized)   # ➜ Converts byte stream back to object

**🧨 Example in Python (Pickle RCE)**
	import pickle
	import os

	# Malicious payload
	class Exploit:
		def __reduce__(self):
			return (os.system, ("echo hacked",))

	# Serialize exploit
	payload = pickle.dumps(Exploit())

	# If the server does this:
	pickle.loads(payload)
	
If deserialization occurs(pickle.loads(payload)) this will run(__reduce__ method):
	echo hacked
Imagine if it was:
	os.system("rm -rf /")
💀

**✅ Safer Python Alternative**
	import json

	data = json.loads(user_input)  # JSON can't execute code!


**Security Impact**
* **Remote Code Execution (RCE):** Attackers can execute malicious code on the server, potentially gaining full control. 
* **Data Tampering:** Attackers can modify data stored or processed by the application. 
* **Denial of Service (DoS):** Attackers can disrupt the application's functionality by causing it to crash or become unresponsive. 
* **Authentication Bypass:** Attackers might be able to bypass authentication mechanisms. 

**How to Prevent Insecure Deserialization**
* Validate and sanitize all input
* Never deserialize untrusted data
* Use safer formats like JSON, which don’t support arbitrary code execution
* Use language-specific defenses
	* Python: avoid pickle for untrusted data
	* PHP: avoid unserialize() on user input
	* Java: use safe deserialization frameworks (e.g., Jackson with type restrictions)

**12. Session Management**
Session Management is the process of securely handling a user's interaction with a web application after they log in, ensuring that the user’s identity and permissions are maintained safely throughout their visit.
**What is a Session?**
* When you log into a website, the server creates a session to remember who you are as you move between pages.
* This session usually has a unique session ID (a token) stored in a cookie or URL parameter.
* The server uses that ID to identify your requests without making you log in again each time.
**Why is Session Management Important?**
If session management is weak or broken, attackers can:
* Hijack sessions (steal session IDs and impersonate users)
* Fixate sessions (force users to use a known session ID)
* Replay sessions (reuse old session tokens)
* Session timeout bypass
This can lead to unauthorized access, data theft, or account takeover.
**Key Components of Secure Session Management**
**Authentication**
* Typically involves verifying a user's identity through a login process (username/password, etc.). 
**Session Creation**
* Upon successful authentication, the application creates a unique session ID.
* The session id Should be long, random, and unpredictable.
**Session Storage**
* The server stores session data(securely) associated with the session ID, which could include user information, preferences, shopping cart details, etc. 
**Session Tracking**
* The Session ID is sent to client only as a token.
* The session ID is stored (often in a cookie on the user's browser) and sent with subsequent requests to identify the user. 
**Session Transmission**
* Use Secure cookies (only sent over HTTPS).
* Use HttpOnly cookies (not accessible via JavaScript) to reduce XSS risks.
**Session Expiration**
* Sessions should expire after inactivity (idle timeout).
* Sessions can also expire after a fixed duration (absolute timeout) or when a user logs out.
**Session Renewal**
* Regenerate session IDs after login and sensitive operations to prevent fixation.
**Logout**
* Destroy session server-side on logout.
* Remove session cookie from client.
**Protection against Attacks**
* Implement protections against Cross-Site Request Forgery (CSRF).
* Validate the session’s origin or user-agent if possible.

**How it works:**
* **Initial Login:** A user attempts to log in to a website or application.
* **Authentication:** The application verifies the user's credentials.
* **Session Creation and ID:** If successful, a unique session ID is generated.
* **Session ID Storage:** The session ID is stored on the user's browser, usually as a cookie.
* **Subsequent Requests:** When the user makes subsequent requests, the browser includes the session ID cookie.
* **Server Validation:** The server receives the request and uses the session ID to identify and validate the user.
* **Access Granted:** The application allows the user to continue their session based on the validated session ID. 

**Common Vulnerabilities in Session Management**
* Session Fixation: Attacker sets a session ID for the victim beforehand.
* Session Hijacking: Stealing session IDs via network sniffing or XSS.
* Predictable Session IDs: Easy to guess session tokens.
* Improper Session Expiration: Sessions never expire or last too long.

**Alternatives to cookie-based session management(stateful):**
* **Token-Based Session Management (Stateless / JWT):** Uses tokens instead of server-side sessions.
**How it works:**
* The server generates a self-contained token (often JWT - JSON Web Token) after login.
* The token contains user data and is signed (optionally encrypted).
* Client stores the token (usually in a cookie or localStorage) and sends it with each request. 
**✅ Pros:**
* Stateless — no need for server to store session data.
* Easier to scale horizontally.
**❌ Cons:**
* Token revocation is hard without a server-side blacklist.
* Token size can be large.
* Risk of token theft if stored insecurely (e.g., in localStorage).
**🔐 Security notes:**
* Use short token lifetimes + refresh tokens.
* Avoid storing tokens in localStorage (vulnerable to XSS).

**Server-Side Session Store Variants**
When using cookie-based sessions, you can store sessions in:
| Type                | Description                                                                                   |
| ------------------- | --------------------------------------------------------------------------------------------- |
| **In-Memory**       | Fast, but doesn’t persist across restarts (e.g., `express-session` with default memory store) |
| **Database**        | Stores sessions in SQL/NoSQL DB for persistence                                               |
| **Redis/Memcached** | High-speed, in-memory store — great for large-scale apps                                      |

**13. Rate Limiting and Throttling**
**Rate limiting** is a policy that restricts how many requests a client can make to a server in a defined time frame.
Essentially, it sets a cap on the number of requests allowed within a given period. 
**How it works:**
* **Time Windows:** Rate limits are typically defined by a time window (e.g., requests per minute, requests per hour, requests per day). 
* **Request Counting:** The system tracks the number of requests made by a user or application within that time window. 
* **Action on exceeding limit:** Rejects requests that exceed the limit, typically returning an error (e.g., 429 Too Many Requests). 
**Various Implementations:**
Rate limiting can be implemented at different levels, such as on the API gateway, at the application level, or on the load balancer. 
**Examples:**
* An API might limit a user to 100 requests per minute. 
* A website might limit the number of form submissions from a single IP address to prevent spam. 
* An e-commerce site might limit the number of requests to its inventory API to prevent scraping. 
**Purpose of rate limiting**
* **Prevent Resource Exhaustion:**
	* Rate limiting helps prevent a single user or application from overwhelming a server or service with too many requests, which could lead to performance degradation or even service outages. 
* **Protect Against Attacks:**
	* It's a key defense against denial-of-service (DoS) and distributed denial-of-service (DDoS) attacks, which flood a system with requests to make it unavailable. 
* **Ensure Fair Usage:**
	* Rate limiting ensures that all users have a reasonable opportunity to access a resource, preventing one user from monopolizing it. 
* **Control Costs:**
	* In cloud environments, excessive API usage can lead to increased costs. Rate limiting can help control these costs by preventing unexpected spikes in usage. 
* **Maintain Service Stability:**
	* By managing the load, rate limiting helps maintain the stability and reliability of the service. 

**Throttling** involves slowing down/limiting the number of operations or requests within a specific time frame. 
It's a way to manage resource usage and maintain system stability. 

**Examples:**
* An API might limit the number of requests a user can make per minute, hour, or day. 
* A cloud service might throttle the number of files a user can upload or download within a specific time frame. 
* Some streaming services throttle video quality if a user is using too much bandwidth. 

**Purpose of Throtling**
* **Prevents system overload:**
	* By limiting resource consumption, throttling helps prevent one user from overwhelming the system and impacting others.
* **Ensures fair usage:**
	* It distributes resources more evenly, so no single user or application takes up more than their fair share.
* **Maintains API availability:**
	* Throttling helps keep APIs responsive and reliable for all users, even under heavy load. 

| Aspect                       | Rate Limiting                                                                | Throttling                                                                             |
| ---------------------------- | ---------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **Hard Limit vs. Smoothing** | Enforces a **hard limit** on the number of requests allowed in a time frame. | Focuses on **smoothing out** traffic fluctuations by slowing down request rates.       |
| **Rejection vs. Delay**      | **Rejects** requests immediately once the limit is reached (e.g., HTTP 429). | May **delay**, queue, or slow down requests rather than outright rejecting them.       |
| **User Experience**          | Can cause **abrupt disruptions**, like sudden blocking of requests.          | Aims for a **smoother experience** by slowing responses instead of blocking.           |
| **System Protection**        | Protects system by strictly limiting request volume to prevent overload.     | Helps handle traffic spikes and maintain **system stability** through gradual control. |







