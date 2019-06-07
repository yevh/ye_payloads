
Cryptographic recommendations
------------------------------------------------------------
In this sheet presented cryptographic recommendation and libraries to use.


Recommendation:
------------------------------------------------------------
```
Key exchange: Diffie–Hellman key exchange with minimum 2048 bits
Message Integrity: HMAC-SHA2
Message Hash: SHA2 256 bits
Assymetric encryption: RSA 2048 bits
Symmetric-key algorithm: AES 128 bits
Password Hashing: Argon2, PBKDF2, Scrypt, Bcrypt
```

Recommended libraries:
```
Python: MbedTLS, Libsodium, PyNaCl, Libnacl.
Ruby: Nacl, djb's.
JS: Crypto-js.
Go: Crypto.
Java: Java.security, Javax.crypto.
PHP: Hash, OpenSSL.
C/C++: OpenSSL.
```

Do not use:
```
C: random(), rand() ----> getrandom(2) 
Java: java.util.Random() ----> java.security.SecureRandom
PHP: rand() or mt_rand() ----> random_int() or random_bytes()
```

References:
------------------------------------------------------------
[Guide to Cryptography](https://www.owasp.org/index.php/Guide_to_Cryptography)    
[Mozilla TLS wiki](https://wiki.mozilla.org/Security/Server_Side_TLS#)    
