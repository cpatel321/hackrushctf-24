Translatation of the title: "le chiffrage indéchiffrable" is the indecipherable encryption. So this hints that the flag is OIERG{7z15_0s3_1_i0g3_y45_mlp} is encrypted. 
Upon scrolling through both the files, we found the key of the encryption. We tried some strings from the .ll file and .s file but none of them worked.

```python
def decrypt(encrypted_message, key):
    decrypted_message = ""
    key = key.lower()  # Convert key to lowercase

    for i in range(len(encrypted_message)):
        char = encrypted_message[i]
        key_char = key[i % len(key)]  # Repeat key if it's shorter than the encrypted message
        if char.isalpha():  # Check if the character is an alphabet
            if char.islower():  # Check if the character is lowercase
                base = ord('a')
            else:
                base = ord('A')
            shift = ord(key_char) - ord('a') if key_char.islower() else ord(key_char) - ord('A')
            decrypted_char = chr((ord(char) - base - shift) % 26 + base)  # Perform the reverse substitution
            decrypted_message += decrypted_char
        else:
            decrypted_message += char

    return decrypted_message

# Example usage
encrypted_message = "OIERG{7z15_0s3_1_i0g3_y45_mlp}"
key = "hrcybersecctf"
decrypted_message = decrypt(encrypted_message, key)
print("Decrypted message:", decrypted_message)

```

Flag: HRCTF{7h15_0n3_1_h0p3_w45_fun}