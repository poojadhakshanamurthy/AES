# EX-8-ADVANCED-ENCRYPTION-STANDARD ALGORITHM
# Aim:
To use Advanced Encryption Standard (AES) Algorithm for a practical application like URL Encryption.

# ALGORITHM:
AES is based on a design principle known as a substitution–permutation.
AES does not use a Feistel network like DES, it uses variant of Rijndael.
It has a fixed block size of 128 bits, and a key size of 128, 192, or 256 bits.
AES operates on a 4 × 4 column-major order array of bytes, termed the state
# PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <openssl/evp.h>
int main()
{
unsigned char key[16] = "0123456789abcdef";
unsigned char iv[16] = "abcdef9876543210";
unsigned char url[100];
unsigned char encrypted[200];
unsigned char decrypted[200];
int len, encrypted_len, decrypted_len;
printf("Enter URL: ");
scanf("%99s", url);
EVP_CIPHER_CTX *ctx;
ctx = EVP_CIPHER_CTX_new();
EVP_EncryptInit_ex(ctx, EVP_aes_128_cbc(), NULL, key, iv);
EVP_EncryptUpdate(ctx, encrypted, &len, url, strlen((char *)url));
encrypted_len = len;
EVP_EncryptFinal_ex(ctx, encrypted + len, &len);
encrypted_len += len;
printf("Encrypted URL: ");
for(int i = 0; i < encrypted_len; i++)
printf("%02x", encrypted[i]);
EVP_CIPHER_CTX_free(ctx);
ctx = EVP_CIPHER_CTX_new();
EVP_DecryptInit_ex(ctx, EVP_aes_128_cbc(), NULL, key, iv);
EVP_DecryptUpdate(ctx, decrypted, &len, encrypted, encrypted_len);
decrypted_len = len;
EVP_DecryptFinal_ex(ctx, decrypted + len, &len);
decrypted_len += len;
decrypted[decrypted_len] = '\0';
printf("\nDecrypted URL: %s", decrypted);
EVP_CIPHER_CTX_free(ctx);
return 0;
}
```


# OUTPUT:
<img width="1522" height="736" alt="image" src="https://github.com/user-attachments/assets/be0e71a4-a37c-4d09-bd84-7c4ea1dd4d0e" />


# RESULT:
Thus, the AES algorithm was successfully implemented in C to encrypt and decrypt a URL using the AES-128 encryption technique.

