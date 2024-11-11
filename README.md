# EX-NO-9-RSA-Algorithm
## DATE:03.10.2024
## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:

Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Conert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```
import random

def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

def mod_inverse(e, phi):
    for d in range(1, phi):
        if (e * d) % phi == 1:
            return d
    return None

def generate_keys():
    p = 61
    q = 53
    n = p * q
    phi = (p - 1) * (q - 1)
    e = random.choice([i for i in range(2, phi) if gcd(i, phi) == 1])
    d = mod_inverse(e, phi)
    return (e, n), (d, n)

def encrypt(message, public_key):
    e, n = public_key
    encrypted_message = [(ord(char) ** e) % n for char in message]
    return encrypted_message

def decrypt(encrypted_message, private_key):
    d, n = private_key
    decrypted_message = ''.join([chr((char ** d) % n) for char in encrypted_message])
    return decrypted_message

public_key, private_key = generate_keys()
print(f"Public Key: {public_key}")
print(f"Private Key: {private_key}")

message = input("Enter a message to encrypt: ")
print(f"Original Message: {message}")

encrypted_message = encrypt(message, public_key)
print(f"Encrypted Message: {encrypted_message}")

decrypted_message = decrypt(encrypted_message, private_key)
print(f"Decrypted Message: {decrypted_message}")


```
## Output:

![image](https://github.com/user-attachments/assets/c30531d7-c019-4895-8ca8-85b98b87beaa)



## Result:
 The program is executed successfully.
