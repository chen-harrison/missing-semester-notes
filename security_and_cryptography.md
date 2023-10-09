# Security and Cryptography

### Hash Functions

- Entropy: measure of randomness, works as a measure of password strength  
    $bits.of.entropy= log_2(num.possibilities)$
    - 40 bits of entropy protects against online guessing, 80+ for offline
- Cryptographic hash function: maps data of arbitrary size to fixed size
    - SHA1 used by git maps takes inputs of varying size and creates 160-bit output
    - Properties
        - Deterministic: same input generates same output
        - Non-invertible: cannot extract input if given its hash output
        - Target collision resistant: knowing an input, it’s hard to find a different input with the same hash output
        - Collision resistant: (strictly stronger condition than target collision resistant) hard to find two inputs with same hash output
    - Applications
        - Git addressing objects: necessary to prevent security leaks, no collision resistance would cause issues with mixed up files/commits
        - Identify file contents: if I know the hash output of a desired file, like an OS file, when I download a copy of that file from a third-party, I can compare its hash with the trusted hash to ensure contents are the same
        - Commitment scheme: aka “flipping a coin in your head”, where you generate a random number and share its hash with opponent, so they do not know the generated number and can guess an outcome, but afterwards can verify that the number outcome you share after the guess was the same from the start
- Key derivation functions (KDFs)
    - Similar to hash functions, producing fixed-length output, but deliberately slow to compute, which deters offline brute-force attacks
    - Applications
        - Producing keys for passphrases used in other cryptographic algorithms (e.g. symmetric cryptography)
        - Storing login credentials, with an added salt, i.e. randomized data unique to each password offsetting the hash output of password

### Cryptography

- Symmetric cryptography
    - (Randomized) key generation with high entropy function creates key
    - Functions
        - `encrypt(plain_text: array<byte>, key) -> array<byte>  (the cipher_text)`
        - `decrypt(cipher_text: array<byte>, key) -> array<byte>  (the plain_text)`
    - Properties
        - Given cipher text, can’t figure out plain text without key
        - Correctness, i.e. `decrypt(encrypt(plain_text, key), key) = plain_text`
    - Application
        - Locally generate key and encrpy files before uploading to cloud storage, decrypt when you pull it back down
- Asymmetric cryptography
    - Key generation creates creates public and private keys
    - Functions
        - `encrypt(plain_text: array<byte>, public_key) -> array<byte>  (the cipher_text)`
        - `decrypt(cipher_text: array<byte>, private_key) -> array<byte>  (the plain_text)`
        - `sign(message: array<byte>, private key) -> array<byte>  (the signature)`
        - `verify(message: array<byte>, signature: array<byte>, public key) -> bool  (whether or not the signature is valid)`
    - The distinction between public and private means you can distribute public key widely to allow others to create encrypted info, but only you can decipher it with the private key
    - Sign and verify allows owner of the private to be verified by those with a public key, like a  signature