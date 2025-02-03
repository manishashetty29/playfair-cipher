# PLAYFAIR CIPHER
# Playfair Cipher Encryption & Decryption

This repository contains a Python program that implements the **Playfair Cipher** to encrypt and decrypt text. The code is designed to be executed in **Google Colab** and can be cloned from GitHub for local execution.

## 🔍 About the Code
The **Playfair Cipher** is a digraph substitution cipher that encrypts text based on a 5x5 matrix of letters generated using a key. Each pair of letters in the plaintext is transformed based on their positions in the matrix.

### 🔑 Logic of the Code
- **Matrix Creation**:
  - A 5x5 matrix is generated using the key, eliminating duplicate letters and merging 'J' with 'I'.
  - The remaining letters of the alphabet are appended to complete the matrix.
- **Encryption**:
  - The plaintext is converted to uppercase and formatted by replacing 'J' with 'I' and removing spaces.
  - If the plaintext length is odd, an 'X' is appended.
  - Letter pairs are substituted based on the following rules:
    - If letters are in the same row, they shift right.
    - If letters are in the same column, they shift down.
    - Otherwise, letters are swapped based on their rectangle positions.
- **Decryption**:
  - The reverse process of encryption is applied using the same matrix.

### 🔄 Example Execution
```
Enter the plain text: instruments
Enter the key: monarchy
Encrypted message: gatlmzclrqtx

Enter the cipher text: gatlmzclrqtx
Enter the key: monarchy
Decrypted message: instrumentsx
```

## 🛠 How to Run the Code
### Option 1: Open in Google Colab
To directly open the notebook in Google Colab, click the button below:

### https://colab.research.google.com/github/manishashetty29/playfair-cipher/blob/main/Untitled0.ipynb

### Option 2: Clone the Repository and Run Locally
1. **Clone the repository** using Git:
   ```sh
   git clone https://github.com/manishashetty29/playfair-cipher.git
   ```
2. **Navigate to the project directory**:
   ```sh
   cd playfair-cipher
   ```
3. **Run the script** in Python:
   ```sh
   python Untitled0.ipynb
   ```

## 📜 Code Explanation
```python
def create_matrix(key):
    alphabet="ABCDEFGHIKLMNOPQRSTUVWXYZ"
    matrix=[]
    key="".join(dict.fromkeys(key.upper().replace("J","I")+alphabet))
    for i in range(0,25,5):
        matrix.append(list(key[i:i+5]))
    return matrix
```
- **`create_matrix(key)`** generates a 5x5 letter matrix based on the key.

```python
def find_position(matrix,char):
    for row in range (5):
        for col in range (5):
            if matrix[row][col]==char:
                return row,col
```
- **`find_position(matrix, char)`** finds the row and column index of a character in the matrix.

```python
def encrypt(ptext,key):
    matrix=create_matrix(key)
    ptext=ptext.upper().replace("J","I").replace(" ","")
    if len(ptext) %2 !=0:
        ptext+="X"
    ciphertext=""
    for i in range(0,len(ptext),2):
        a,b=ptext[i],ptext[i+1]
        row1,col1=find_position(matrix,a)
        row2,col2=find_position(matrix,b)
        if row1==row2:
            ciphertext+=matrix[row1][(col1+1)%5]+matrix[row2][(col2+1)%5]
        elif col1==col2:
            ciphertext+=matrix[(row1+1)%5][col1]+matrix[(row2+1)%5][col2]
        else:
            ciphertext+=matrix[row1][col2]+matrix[row2][col1]
    return ciphertext
```
- **`encrypt(ptext, key)`** processes the plaintext into ciphertext using the Playfair Cipher rules.

```python
def decrypt(text,key):
    matrix=create_matrix(key)
    text=text.upper().replace("J","I").replace(" ","")
    plaintext=""
    for i in range(0,len(text),2):
        a,b=text[i],text[i+1]
        row1,col1=find_position(matrix,a)
        row2,col2=find_position(matrix,b)
        if row1==row2:
            plaintext+=matrix[row1][(col1-1)%5]+matrix[row2][(col2-1)%5]
        elif col1==col2:
            plaintext+=matrix[(row1-1)%5][col1]+matrix[(row2-1)%5][col2]
        else:
            plaintext+=matrix[row1][col2]+matrix[row2][col1]
    return plaintext
```
- **`decrypt(text, key)`** reverses the encryption process to retrieve the original text.

```python
ptext=input("Enter the plain text:")
key=input("Enter the key:")
print("Encrypted message:",encrypt(ptext,key))
text=input("Enter the cipher text:")
key=input("Enter the key:")
print("Decrypted message:",decrypt(text,key))
```
- Takes user input for encryption and decryption.
- Prints the resulting encrypted and decrypted messages.

## 📌 Features
✅ Implements Playfair Cipher for secure encryption
✅ Encryption and decryption functions
✅ Works on Google Colab & locally
✅ Easy to clone and run


