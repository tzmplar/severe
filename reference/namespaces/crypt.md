# crypt

## Functions

### random

```lua
function crypt.random(length: number): string
```

Generates a random byte buffer of the given length. Returns a string of raw bytes.

### random\_deterministic

```lua
function crypt.random_deterministic(length: number, seed: string): string
```

Generates a deterministic random buffer of given length using seed (32 bytes). Returns a string of raw bytes.

### sha256

```lua
function crypt.hash.sha256(message: string): string
```

Computes the SHA-256 hash of the message. Returns a string of 32 bytes.

### sha512

```lua
function crypt.hash.sha512(message: string): string
```

Computes the SHA-512 hash of the message. Returns a string of 64 bytes.

### blake2b

```lua
function crypt.hash.blake2b(message: string, outlen: number?): string
```

Computes the BLAKE2b hash of the message. `outlen` is optional and defaults to 32; must be between 1 and 64. Returns a string of `outlen` bytes.

### pwhash

```lua
function crypt.pwhash(password: string, outlen: number): string
```

Derives a key from the password using Argon2id. Returns a binary key of `outlen` bytes.

### pwhash\_str

```lua
function crypt.pwhash_str(password: string): string
```

Hashes the password into a safe string for storage.

### pwhash\_str\_verify

```lua
function crypt.pwhash_str_verify(hash: string, password: string): boolean
```

Verifies the password against the hash. Returns `true` if the password matches, `false` otherwise.

### seal

```lua
function crypt.secretbox.seal(plaintext: string, nonce: string, key: string): string
```

Encrypts the plaintext using symmetric encryption with XSalsa20-Poly1305. `nonce` must be 24 bytes, `key` must be 32 bytes. Returns the ciphertext.

### open

```lua
function crypt.secretbox.open(ciphertext: string, nonce: string, key: string): string
```

Decrypts the ciphertext using symmetric decryption with XSalsa20-Poly1305. `nonce` must be 24 bytes, `key` must be 32 bytes. Returns the plaintext.

### encrypt

```lua
function crypt.aead.encrypt(plaintext: string, nonce: string, key: string, ad: string?): string
```

Encrypts the plaintext using AEAD XChaCha20-Poly1305. `nonce` and `key` are required, `ad` (additional data) is optional. Returns the ciphertext.

### decrypt

```lua
function crypt.aead.decrypt(ciphertext: string, nonce: string, key: string, ad: string?): string
```

Decrypts the ciphertext using AEAD XChaCha20-Poly1305. `nonce` and `key` are required, `ad` (additional data) is optional. Returns the plaintext.

### keypair

```lua
function crypt.box.keypair(): table
```

Generates a Curve25519 keypair. Returns a table with `public` and `secret` keys (both strings).

### encrypt

```lua
function crypt.box.encrypt(message: string, nonce: string, pub: string, sec: string): string
```

Encrypts the message using public and secret keys. `nonce` must be 24 bytes, `pub` and `sec` are 32 bytes. Returns the ciphertext.

### decrypt

```lua
function crypt.box.decrypt(ciphertext: string, nonce: string, pub: string, sec: string): string
```

Decrypts the ciphertext using public and secret keys. `nonce` must be 24 bytes, `pub` and `sec` are 32 bytes. Returns the plaintext.

### seal

```lua
function crypt.box.seal(message: string, pub: string): string
```

Anonymously seals the message for the receiver’s public key. `pub` is 32 bytes. Returns the ciphertext.

### seal\_open

```lua
function crypt.box.seal_open(ciphertext: string, pub: string, sec: string): string
```

Opens the sealed message using the receiver’s public and secret keys. `pub` and `sec` are 32 bytes. Returns the plaintext.

### beforenm

```lua
function crypt.box.beforenm(pub: string, sec: string): string
```

Computes a shared key from public and secret keys for reuse. `pub` and `sec` are 32 bytes. Returns the shared key.

### keypair

```lua
function crypt.sign.keypair(): table
```

Generates an Ed25519 signing keypair. Returns a table with `public` (32 bytes) and `secret` (64 bytes) keys.

### sign

```lua
function crypt.sign.sign(message: string, sec: string): string
```

Signs the message with the secret key. `sec` is 64 bytes. Returns the signed message.

### open

```lua
function crypt.sign.open(signed: string, pub: string): string
```

Verifies and extracts the message from the signed message. `pub` is 32 bytes. Returns the original message.

### detached

```lua
function crypt.sign.detached(message: string, sec: string): string
```

Creates a detached signature for the message. `sec` is 64 bytes. Returns the signature.

### verify\_detached

```lua
function crypt.sign.verify_detached(sig: string, message: string, pub: string): boolean
```

Verifies the detached signature against the message and public key. `pub` is 32 bytes. Returns `true` if valid, `false` otherwise.

### encode

```lua
function crypt.base64.encode(raw: string): string
```

Base64 encodes the raw string. Returns the encoded string.

### decode

```lua
function crypt.base64.decode(b64: string): string
```

Base64 decodes the string. Returns the raw bytes.

### sha256

```lua
function crypt.hmac.sha256(message: string, key: string): string
```

Computes HMAC-SHA256 of the message with the key. Returns a string of 32 bytes.

### sha512

```lua
function crypt.hmac.sha512(message: string, key: string): string
```

Computes HMAC-SHA512 of the message with the key. Returns a string of 64 bytes.

### hkdf\_sha256

```lua
function crypt.hkdf_sha256(ikm: string, salt: string, info: string, outlen: number): string
```

Performs HKDF-SHA256 key derivation. Returns a binary key of `outlen` bytes.

### encode

```lua
function crypt.json.encode(t: table): string
```

Encodes a table to JSON. See https://create.roblox.com/docs/reference/engine/classes/HttpService#JSONEncode for details.

### decode

```lua
function crypt.json.decode(s: string): table
```

Decodes JSON to a table. See https://create.roblox.com/docs/reference/engine/classes/HttpService#JSONDecode for details.
