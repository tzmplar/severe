# crypt

Cryptography library providing various cryptographic functions for encryption, hashing, signing, and encoding.

> **Note:** All arguments for crypt functions should be assumed as strings unless otherwise specified.

## Random

## crypt.random

### Definition

```luau
function crypt.random(size: string): string
```

### Parameters

| Name | Type   | Description                          |
| ---- | ------ | ------------------------------------ |
| size | string | The size of random data to generate  |

### Returns

| Type   |
| ------ |
| string |

### Description

Generates cryptographically secure random bytes of the specified size.

---

## crypt.random_deterministic

### Definition

```luau
function crypt.random_deterministic(size: string, seed: string): string
```

### Parameters

| Name | Type   | Description                          |
| ---- | ------ | ------------------------------------ |
| size | string | The size of random data to generate  |
| seed | string | The seed for deterministic generation |

### Returns

| Type   |
| ------ |
| string |

### Description

Generates deterministic random bytes of the specified size using the provided seed.

---

## Hash

## crypt.hash.sha256

### Definition

```luau
function crypt.hash.sha256(data: string): string
```

### Parameters

| Name | Type   | Description           |
| ---- | ------ | --------------------- |
| data | string | The data to hash      |

### Returns

| Type   |
| ------ |
| string |

### Description

Computes the SHA-256 hash of the input data.

---

## crypt.hash.sha512

### Definition

```luau
function crypt.hash.sha512(data: string): string
```

### Parameters

| Name | Type   | Description           |
| ---- | ------ | --------------------- |
| data | string | The data to hash      |

### Returns

| Type   |
| ------ |
| string |

### Description

Computes the SHA-512 hash of the input data.

---

## crypt.hash.blake2b

### Definition

```luau
function crypt.hash.blake2b(data: string): string
```

### Parameters

| Name | Type   | Description           |
| ---- | ------ | --------------------- |
| data | string | The data to hash      |

### Returns

| Type   |
| ------ |
| string |

### Description

Computes the BLAKE2b hash of the input data.

---

## Password Hashing

## crypt.pwhash

### Definition

```luau
function crypt.pwhash(password: string, salt: string?): string
```

### Parameters

| Name     | Type    | Description                      |
| -------- | ------- | -------------------------------- |
| password | string  | The password to hash             |
| salt     | string? | Optional salt for hashing        |

### Returns

| Type   |
| ------ |
| string |

### Description

Hashes a password using a secure password hashing algorithm. If salt is not provided, one is generated automatically.

---

## crypt.pwhash_str

### Definition

```luau
function crypt.pwhash_str(password: string): string
```

### Parameters

| Name     | Type   | Description              |
| -------- | ------ | ------------------------ |
| password | string | The password to hash     |

### Returns

| Type   |
| ------ |
| string |

### Description

Hashes a password and returns a string that includes the salt and hash parameters for later verification.

---

## crypt.pwhash_str_verify

### Definition

```luau
function crypt.pwhash_str_verify(hash: string, password: string): boolean
```

### Parameters

| Name     | Type   | Description                            |
| -------- | ------ | -------------------------------------- |
| hash     | string | The hash string from pwhash_str        |
| password | string | The password to verify                 |

### Returns

| Type    |
| ------- |
| boolean |

### Description

Verifies a password against a hash string created by `pwhash_str`.

---

## Secretbox

## crypt.secretbox.seal

### Definition

```luau
function crypt.secretbox.seal(message: string, nonce: string, key: string): string
```

### Parameters

| Name    | Type   | Description                    |
| ------- | ------ | ------------------------------ |
| message | string | The message to encrypt         |
| nonce   | string | The nonce (number used once)   |
| key     | string | The secret key                 |

### Returns

| Type   |
| ------ |
| string |

### Description

Encrypts a message using secret-key authenticated encryption.

---

## crypt.secretbox.open

### Definition

```luau
function crypt.secretbox.open(cipher: string, nonce: string, key: string): string
```

### Parameters

| Name   | Type   | Description                    |
| ------ | ------ | ------------------------------ |
| cipher | string | The encrypted message          |
| nonce  | string | The nonce (number used once)   |
| key    | string | The secret key                 |

### Returns

| Type   |
| ------ |
| string |

### Description

Decrypts a message encrypted with `secretbox.seal`.

---

## AEAD

## crypt.aead.encrypt

### Definition

```luau
function crypt.aead.encrypt(message: string, aad: string, nonce: string, key: string): string
```

### Parameters

| Name    | Type   | Description                              |
| ------- | ------ | ---------------------------------------- |
| message | string | The message to encrypt                   |
| aad     | string | Additional authenticated data            |
| nonce   | string | The nonce (number used once)             |
| key     | string | The secret key                           |

### Returns

| Type   |
| ------ |
| string |

### Description

Encrypts a message using authenticated encryption with associated data (AEAD).

---

## crypt.aead.decrypt

### Definition

```luau
function crypt.aead.decrypt(cipher: string, aad: string, nonce: string, key: string): string
```

### Parameters

| Name   | Type   | Description                              |
| ------ | ------ | ---------------------------------------- |
| cipher | string | The encrypted message                    |
| aad    | string | Additional authenticated data            |
| nonce  | string | The nonce (number used once)             |
| key    | string | The secret key                           |

### Returns

| Type   |
| ------ |
| string |

### Description

Decrypts a message encrypted with `aead.encrypt`.

---

## Public-Key Box

## crypt.box.keypair

### Definition

```luau
function crypt.box.keypair(): (string, string)
```

### Returns

| Type             |
| ---------------- |
| (string, string) |

### Description

Generates a new public-key pair for box encryption. Returns `(publicKey, secretKey)`.

---

## crypt.box.encrypt

### Definition

```luau
function crypt.box.encrypt(message: string, nonce: string, publicKey: string, secretKey: string): string
```

### Parameters

| Name      | Type   | Description                         |
| --------- | ------ | ----------------------------------- |
| message   | string | The message to encrypt              |
| nonce     | string | The nonce (number used once)        |
| publicKey | string | The recipient's public key          |
| secretKey | string | The sender's secret key             |

### Returns

| Type   |
| ------ |
| string |

### Description

Encrypts a message using public-key authenticated encryption.

---

## crypt.box.decrypt

### Definition

```luau
function crypt.box.decrypt(cipher: string, nonce: string, publicKey: string, secretKey: string): string
```

### Parameters

| Name      | Type   | Description                         |
| --------- | ------ | ----------------------------------- |
| cipher    | string | The encrypted message               |
| nonce     | string | The nonce (number used once)        |
| publicKey | string | The sender's public key             |
| secretKey | string | The recipient's secret key          |

### Returns

| Type   |
| ------ |
| string |

### Description

Decrypts a message encrypted with `box.encrypt`.

---

## crypt.box.seal

### Definition

```luau
function crypt.box.seal(message: string, publicKey: string): string
```

### Parameters

| Name      | Type   | Description                    |
| --------- | ------ | ------------------------------ |
| message   | string | The message to encrypt         |
| publicKey | string | The recipient's public key     |

### Returns

| Type   |
| ------ |
| string |

### Description

Encrypts a message using sealed box encryption (anonymous sender).

---

## crypt.box.open

### Definition

```luau
function crypt.box.open(cipher: string, publicKey: string, secretKey: string): string
```

### Parameters

| Name      | Type   | Description                    |
| --------- | ------ | ------------------------------ |
| cipher    | string | The encrypted message          |
| publicKey | string | The recipient's public key     |
| secretKey | string | The recipient's secret key     |

### Returns

| Type   |
| ------ |
| string |

### Description

Decrypts a message encrypted with `box.seal`.

---

## crypt.box.beforenm

### Definition

```luau
function crypt.box.beforenm(publicKey: string, secretKey: string): string
```

### Parameters

| Name      | Type   | Description              |
| --------- | ------ | ------------------------ |
| publicKey | string | The other party's public key |
| secretKey | string | Your secret key          |

### Returns

| Type   |
| ------ |
| string |

### Description

Computes a shared secret for faster encryption/decryption between the same parties.

---

## Signing

## crypt.sign.keypair

### Definition

```luau
function crypt.sign.keypair(): (string, string)
```

### Returns

| Type             |
| ---------------- |
| (string, string) |

### Description

Generates a new key pair for digital signatures. Returns `(publicKey, secretKey)`.

---

## crypt.sign.sign

### Definition

```luau
function crypt.sign.sign(message: string, secretKey: string): string
```

### Parameters

| Name      | Type   | Description              |
| --------- | ------ | ------------------------ |
| message   | string | The message to sign      |
| secretKey | string | The secret signing key   |

### Returns

| Type   |
| ------ |
| string |

### Description

Signs a message and returns the signature concatenated with the message.

---

## crypt.sign.open

### Definition

```luau
function crypt.sign.open(signedMessage: string, publicKey: string): string
```

### Parameters

| Name          | Type   | Description                        |
| ------------- | ------ | ---------------------------------- |
| signedMessage | string | The signed message from sign()     |
| publicKey     | string | The public verification key        |

### Returns

| Type   |
| ------ |
| string |

### Description

Verifies and extracts the original message from a signed message.

---

## crypt.sign.detached

### Definition

```luau
function crypt.sign.detached(message: string, secretKey: string): string
```

### Parameters

| Name      | Type   | Description              |
| --------- | ------ | ------------------------ |
| message   | string | The message to sign      |
| secretKey | string | The secret signing key   |

### Returns

| Type   |
| ------ |
| string |

### Description

Signs a message and returns only the signature (detached from the message).

---

## crypt.sign.verify_detached

### Definition

```luau
function crypt.sign.verify_detached(signature: string, message: string, publicKey: string): boolean
```

### Parameters

| Name      | Type   | Description                   |
| --------- | ------ | ----------------------------- |
| signature | string | The detached signature        |
| message   | string | The original message          |
| publicKey | string | The public verification key   |

### Returns

| Type    |
| ------- |
| boolean |

### Description

Verifies a detached signature for a message.

---

## Base64

## crypt.base64.encode

### Definition

```luau
function crypt.base64.encode(data: string): string
```

### Parameters

| Name | Type   | Description           |
| ---- | ------ | --------------------- |
| data | string | The data to encode    |

### Returns

| Type   |
| ------ |
| string |

### Description

Encodes data to Base64 format.

---

## crypt.base64.decode

### Definition

```luau
function crypt.base64.decode(data: string): string
```

### Parameters

| Name | Type   | Description                 |
| ---- | ------ | --------------------------- |
| data | string | The Base64 data to decode   |

### Returns

| Type   |
| ------ |
| string |

### Description

Decodes Base64 encoded data.

---

## HMAC

## crypt.hmac.sha256

### Definition

```luau
function crypt.hmac.sha256(data: string, key: string): string
```

### Parameters

| Name | Type   | Description           |
| ---- | ------ | --------------------- |
| data | string | The data to hash      |
| key  | string | The secret key        |

### Returns

| Type   |
| ------ |
| string |

### Description

Computes an HMAC using SHA-256.

---

## crypt.hmac.sha512

### Definition

```luau
function crypt.hmac.sha512(data: string, key: string): string
```

### Parameters

| Name | Type   | Description           |
| ---- | ------ | --------------------- |
| data | string | The data to hash      |
| key  | string | The secret key        |

### Returns

| Type   |
| ------ |
| string |

### Description

Computes an HMAC using SHA-512.

---

## HKDF

## crypt.hkdf.sha256

### Definition

```luau
function crypt.hkdf.sha256(key: string, salt: string, info: string): string
```

### Parameters

| Name | Type   | Description                      |
| ---- | ------ | -------------------------------- |
| key  | string | The input keying material        |
| salt | string | The salt value                   |
| info | string | The context and application info |

### Returns

| Type   |
| ------ |
| string |

### Description

Derives a key using HKDF (HMAC-based Key Derivation Function) with SHA-256.

---

## JSON

## crypt.json.encode

### Definition

```luau
function crypt.json.encode(data: table): string
```

### Parameters

| Name | Type  | Description           |
| ---- | ----- | --------------------- |
| data | table | The table to encode   |

### Returns

| Type   |
| ------ |
| string |

### Description

Encodes a Luau table to a JSON string.

---

## crypt.json.decode

### Definition

```luau
function crypt.json.decode(json: string): table
```

### Parameters

| Name | Type   | Description     |
| ---- | ------ | --------------- |
| json | string | The JSON string |

### Returns

| Type  |
| ----- |
| table |

### Description

Decodes a JSON string to a Luau table.

---

## Hexadecimal

## crypt.hexadecimal.encode

### Definition

```luau
function crypt.hexadecimal.encode(bytes: string): string
```

### Parameters

| Name  | Type   | Description           |
| ----- | ------ | --------------------- |
| bytes | string | The bytes to encode   |

### Returns

| Type   |
| ------ |
| string |

### Description

Encodes bytes to hexadecimal string representation.

---

## crypt.hexadecimal.decode

### Definition

```luau
function crypt.hexadecimal.decode(hex: string): string
```

### Parameters

| Name | Type   | Description                 |
| ---- | ------ | --------------------------- |
| hex  | string | The hexadecimal string      |

### Returns

| Type   |
| ------ |
| string |

### Description

Decodes a hexadecimal string to bytes.

