# ColumnEncryption

Encrypting a column on a postgres table while the data is at rest.

Two Choices

* Symmetric Keys - One key does it all
* Asymmetric Keys - Encrypt using public key, Decrypt using private key

No one approach is better encryption than the other, and both have pros and cons for security.


## Setup Postgres for Column Level Encryption

Start up postgres (e.g. psql) and execute - CREATE EXTENSION pgcrypto ;

CREATE TABLE secdemo (id SERIAL, pan VARCHAR(19), pan_symmetric TEXT UNIQUE, pan_asymmetric TEXT UNIQUE) ;

INSERT INTO secdemo (pan, pan_symmetric)
VALUES ('5413330089010640', pgp_sym_encrypt('5413330089010640','VerySecretKey' ) ) ;

Example of how it is stored on disc

id |       pan        |                                                                             pan_symmetric              
| pan_asymmetric
----+------------------+--------------------------------------------------------------------------------------------------------
----------------------------------------------------------------+----------------
1 | 5413330089010640 | \xc30d04070302198131d44dd7f27f7fd241013c68e01ecc965e41afe8331c3424508a578fc88cedf2fd3bee293a28ece175622
db9e24ced6beffc2abd747fb0e5586ef4cd4f98cee5a8612440b8e09331a813 |


Now we want to get it back - recover the original PAN

select id, pgp_sym_decrypt(pan_symmetric::BYTEA,'VerySecretKey') from secdemo;

id | pgp_sym_decrypt  
----+------------------
1 | 5413330089010640

## Column Encryption is secure

Key is not stored in code. Key is only injected into the container on startup
