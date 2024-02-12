# Cryptography Simplified

## 1. DES (Data Encryption Standard)

### 1.1 OpenSSL Example

    openssl enc -e -des -in {input_file_name} -out {output_file_name} -K {64-bit key} -iv {64-bit IV} -nosalt -a

    # Example
    # Encryption
    openssl enc -e -des -in plaintext -out cipher -K 0123456789ABCDEF -iv 0000000000000000 -nosalt -a

    # Decryption
    openssl enc -d -des -in cipher -out plain -K 0123456789ABCDEF -iv 0000000000000000 -nosalt -a

* enc: Encrypt/Decrypt command
* -e: Specify encrypt method
* -des: Use DES algorithm
* -in {input_file_name}: Input file. Note, DES takes input in ASCII format for encryption.
* -out {output_file_name}: Output file name where ciphertext will be stored.
* -K {key}: Provide 64 bit RAW Key in HEX format
* -iv {iv}: Initialization Vector, not used in DES ECB mode.
* -nosalt: Do not use salt
* -a: Output in Base64 format 
* -d: Decrypt

### 1.2 Online Tools
    http://des.online-domain-tools.com/

## 2. 3DES (Triple DES)

### 2.1 OpenSSL Example

    openssl enc -e -des-ede3-cbc -in {input_file_name} -out {output_file_name} -K {192-bit key} -iv {iv} -a

    #Example
    #Encryption
    openssl enc -e -des-ede3-cbc -in plain -out cipher -iv 1122334455667788 -K 111111111111111122222222222222223333333333333333 -a

    #Decryption
    openssl enc -d -des-ede3-cbc -in cipher -out plain -iv 1122334455667788 -K 111111111111111122222222222222223333333333333333 -a

* enc: Encrypt/Decrypt command
* -e: Specify encrypt method
* -des-ede3-cbc: Use 3DES algorithm in CBC mode
* -in {input_file_name}: Input file. Note, DES takes input in ASCII format for encryption.
* -out {output_file_name}: Output file name where ciphertext will be stored.
* -K {key}: Provide 128/192 bit RAW Key in HEX format
* -iv {iv}: Provide Initialization Vector
* -a: Output in Base64 format
* -d: Decrypt
* For decryption openssl can take input in base64 format if -a option is defined.

### 2.2 Online Tools
    http://tripledes.online-domain-tools.com/

## 3. AES (Advanced Encryption Standard)

### 3.1 OpenSSL Example

    openssl enc -e -des-ede3-cbc -in {input_file_name} -out {output_file_name} -K {192-bit key} -iv {iv} -a

    #Example
    #Encryption
    openssl enc -e -aes128 -in plain -out cipher -iv 00000000000000000000000000000000 -K 11111111111111112222222222222222 -a

    #Decryption
    openssl enc -d -aes128 -in cipher -out plain -iv 00000000000000000000000000000000 -K 11111111111111112222222222222222 -a

* enc: Encrypt/Decrypt command
* -e: Specify encrypt method
* -aes128: Use AES algorithm with 128 bit (16 byte) key
* -in {input_file_name}: Input file. Note, DES takes input in ASCII format for encryption.
* -out {output_file_name}: Output file name where ciphertext will be stored.
* -K {key}: Provide 128 bit RAW Key in HEX format
* -iv {iv}: Provide Initialization Vector
* -a: Output in Base64 format
* -d: Decrypt
* For decryption openssl can take input in base64 format if -a option is defined.

### 3.2 Online Tools
    http://aes.online-domain-tools.com/

## 4. RSA (Rivest Shamir Alderman)

### 4.1 OpenSSL Example

    # Generation
    openssl genrsa -out private.key 4096
    openssl rsa -in private.key -pubout -out public.key

    # View
    openssl rsa -in private.key -noout -text
    openssl rsa -in public.key -pubin -noout -text

    # Encrypt/Decrypt
    openssl rsautl -encrypt -inkey public.key -pubin -in plain
    openssl rsautl -decrypt -inkey private.key -in encrypted

    # Digital Signature
    openssl dgst -sha256 -sign private.key -out plain.signature plain
    openssl dgst -sha256 -verify public.key -signature plain.signature plain
    # OR 
    openssl rsautl -sign -inkey private.key -in plain -out plain.signature
    openssl rsautl -verify -inkey public.key -pubin -in plain.signature


### 4.2. OpenSSL Digital Certificates

    #Digital Certificate
    #Create CSR 
    openssl req -key private.key -new -out ca.csr

    # OR both Private Key and CSR
    openssl req -newkey rsa:2048 -keyout domain.key -out domain.csr

    #Signing Certificate
    #Self Sign
    openssl x509 -signkey private.key -in ca.csr -req -days 365 -out ca.crt
    #Sign with CA Key and CRT
    openssl x509 -CA ca.crt -CAkey private.key -in server.csr -req -days 365 -out server.crt

    #Encrypting/Decrypting with Certificate
    openssl rsautl -encrypt -inkey server.crt -certin -in plain -out encrypted

## 5. ECDH (Elliptic Curve Diffie Helman)

### 5.1 OpenSSL Example

    # Entity 1 key generation
    openssl ecparam -name prime256v1 -out curve.pem
    openssl ecparam -name prime256v1 -genkey -noout -out private.pem
    openssl ec -in private.pem -pubout -out public.pem

    # Entity 2 (Other) key generation
    openssl ecparam -name prime256v1 -out curve_other.pem
    openssl ecparam -name prime256v1 -genkey -noout -out private_other.pem
    openssl ec -in private_other.pem -pubout -out public_other.pem

    # Shared Secret Entity 1
    openssl pkeyutl -derive -inkey private.pem  -peerkey public_other.pem -out secret.bin

    # Shared Secret Entity 2 (Other)
    openssl pkeyutl -derive -inkey private_other.pem  -peerkey public.pem -out secret_other.bin

    # Compare secret.bin and secret_other.bin using xxd command
    xxd secret.bin
    xxd secret_other.bin

    #or use diff command
    diff secret.bin secret_other.bin