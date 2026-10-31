# Lab-Exercise---2---Playfair-Cipher
## Aim 
To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.
## Procedurea
```
Step 1: Design of PlayFair Cipher algorithm
Step 2: Implementation using C or python code
Step 3: Testing algorithm with different key values.
```
## PROGRAM:
```
def generate_matrix(key):
    key = key.upper().replace("J", "I")
    seen = set()
    matrix_letters = []

    for char in key:
        if char.isalpha() and char not in seen:
            seen.add(char)
            matrix_letters.append(char)

    alphabet = "ABCDEFGHIKLMNOPQRSTUVWXYZ"  # Note: 'J' is omitted
    for char in alphabet:
        if char not in seen:
            seen.add(char)
            matrix_letters.append(char)

    # Build 5x5 matrix
    matrix = [matrix_letters[i : i + 5] for i in range(0, 25, 5)]
    return matrix


def prepare_text(text):
    text = text.upper().replace("J", "I")
    cleaned = [c for c in text if c.isalpha()]

    pairs = []
    i = 0
    while i < len(cleaned):
        a = cleaned[i]
        if i + 1 < len(cleaned):
            b = cleaned[i + 1]
            if a == b:
                pairs.append(a + "X")
                i += 1
            else:
                pairs.append(a + b)
                i += 2
        else:
            pairs.append(a + "X")
            i += 1
    return pairs


def playfair_encrypt(plaintext, key):
    matrix = generate_matrix(key)
    pairs = prepare_text(plaintext)

    def position(char):
        for r in range(5):
            for c in range(5):
                if matrix[r][c] == char:
                    return r, c
        return None

    ciphertext = ""

    for pair in pairs:
        r1, c1 = position(pair[0])
        r2, c2 = position(pair[1])

        if r1 == r2:  # Same row
            ciphertext += matrix[r1][(c1 + 1) % 5]
            ciphertext += matrix[r2][(c2 + 1) % 5]
        elif c1 == c2:  # Same column
            ciphertext += matrix[(r1 + 1) % 5][c1]
            ciphertext += matrix[(r2 + 1) % 5][c2]
        else:  # Rectangle rule
            ciphertext += matrix[r1][c2]
            ciphertext += matrix[r2][c1]

    return matrix, pairs, ciphertext


key = input("Enter the key: ")
plaintext = input("Enter the plaintext: ")

matrix, pairs, ciphertext = playfair_encrypt(plaintext, key)

print("\nKey Matrix:")
for row in matrix:
    print(" ".join(row))

print("\nPlaintext pairs:", ", ".join(pairs))
print("Encrypted text:", ciphertext)
```
## Output
<img width="1290" height="321" alt="image" src="https://github.com/user-attachments/assets/741c6da1-4c38-48ee-a9bb-015477e4ae13" />

## Result
The program is executed successfully. 
