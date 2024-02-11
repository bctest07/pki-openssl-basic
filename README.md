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
