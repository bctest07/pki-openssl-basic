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