# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```
import random

# ---------- Modular exponentiation ----------
def power(base, exp, mod):
    return pow(base, exp, mod)

# ---------- Modular inverse ----------
def mod_inverse(a, p):
    # Fermat's Little Theorem (since p is prime)
    return pow(a, p - 2, p)

# ---------- Key generation ----------
def generate_keys():
    p = 467  # large prime
    g = 2    # primitive root modulo p
    x = random.randint(2, p - 2)  # private key
    y = power(g, x, p)            # public key
    return (p, g, y), x

# ---------- Encryption ----------
def encrypt(public_key, message):
    p, g, y = public_key
    k = random.randint(2, p - 2)  # random session key
    c1 = power(g, k, p)
    s = power(y, k, p)
    c2 = (message * s) % p
    return (c1, c2)

# ---------- Decryption ----------
def decrypt(private_key, ciphertext, p):
    c1, c2 = ciphertext
    s = power(c1, private_key, p)
    s_inv = mod_inverse(s, p)
    m = (c2 * s_inv) % p
    return m

# ---------- MAIN PROGRAM ----------
if __name__ == "__main__":
    print("=== ElGamal Encryption & Decryption Demo ===")

    # Generate keys
    public_key, private_key = generate_keys()
    p, g, y = public_key

    # Take user input (numeric message)
    user_msg = input("\nEnter a message (number only): ")

    try:
        message = int(user_msg)
        if message >= p:
            raise ValueError("Message must be smaller than p.")
    except ValueError:
        print(" Invalid input. Please enter a number smaller than p.")
        exit()

    # Encrypt
    ciphertext = encrypt(public_key, message)

    # Decrypt
    decrypted_message = decrypt(private_key, ciphertext, p)

    # Display results
    print("\nEncrypted Data (c1, c2):", ciphertext)
    print("Decrypted Data:", decrypted_message)

    if decrypted_message == message:
        print("\nDecryption successful — message restored correctly! ")
    else:
        print("\nDecryption failed! ")
```



## Output:
`<img width="808" height="342" alt="image" src="https://github.com/user-attachments/assets/9fe0db3b-6bd5-46a6-b000-36145d311896" />



## Result:
The program is executed successfully.
