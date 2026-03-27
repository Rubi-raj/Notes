# 🔐 Encoding vs Hashing vs Encryption

## 🔐 Encoding

* Converts data from **one format to another** so systems can understand or transmit it.
* Used for **data representation**, not security.
* **Fully reversible🔁** - anyone can decode it.
* **Bi-Directional** transformation.
* Eg:- **URL** are encoded to send special characters.
* Formats: `UTF-8`,`Base64`,`Binary`,`HEX`

## 🔐 Hashing

* Converts data into a **fixed-length hash value**.
* **One-way (irreversible)** process.
* Used mainly for **password storage** and **data integrity**.
* Eg:- **User password** do Hashing and stored in database.
* Formats: `SHA-256`,`BCrypt`,`Argon2`

## 🔐 Encryption

* Converts readable data (**plaintext**) into **ciphertext**.
* Requires a **key** to decrypt.
* Used for **secure communication**.
* Eg:- **WhatsApp** encrypting the user message.
* There are two types:
    * **Symmetric Encryption** - **Same key** for encryption and decryption. Eg: `AES`,`ChaCha20` etc.
    * **Asymmetric Encryption** - Uses two keys **Public Key**(encrypt) and **Private Key**(decrypt). Eg: `RSA`,`ECE` etc.