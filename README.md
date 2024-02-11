# Cryptography Simplified

## DES (Data Encryption Standard)

### OpenSSL Example

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

### Online Tools
    http://des.online-domain-tools.com/