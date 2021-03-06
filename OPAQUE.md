# OPAQUE Parameters

Currently all parameters are hardcoded, but there's nothing stoping you
and set stronger values for the password hash, or changing the curve
from 25519 to 448 goldilocks.

## The Curve

This OPAQUE implementation is based on libdecaf using the 25519 curve,
but can be easily adapted to use goldilocks448. This means currently
all keys are 32 byte long.

## Other Crypto building blocks

This OPAQUE implementation relies on libsodium as a dependency to
provide all other cryptographic primitives:

   - crypto_generichash[1] outputs 32 byte hashes generated by Blake2b
   - crypto_secretbox[2] uses the XSalsa20 stream cipher for encryption
     and the Poly1305 MAC for authentication
   - crypto_pwhash[3] uses the Argon2 function with
     `crypto_pwhash_OPSLIMIT_INTERACTIVE`,
     `crypto_pwhash_MEMLIMIT_INTERACTIVE` as security parameters.
   - randombytes attempts to use the cryptographic random source of
     the underlying operating system[4]


[1] https://download.libsodium.org/doc/hashing/generic_hashing
[2] https://download.libsodium.org/doc/secret-key_cryptography/authenticated_encryption
[3] https://download.libsodium.org/doc/password_hashing/the_argon2i_function
[4] https://download.libsodium.org/doc/generating_random_data
