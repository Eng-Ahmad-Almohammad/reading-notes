# Ceasar Cipher

### Ceasar Cipher: is one of the simplest and most widely known encryption techniques. It is a type of substitution cipher in which each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet. For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.

### The transformation can be represented by aligning two alphabets; the cipher alphabet is the plain alphabet rotated left or right by some number of positions. For instance, here is a Caesar cipher using a left rotation of three places, equivalent to a right shift of 23 (the shift parameter is used as the key):
```
Plain:    ABCDEFGHIJKLMNOPQRSTUVWXYZ
Cipher:   XYZABCDEFGHIJKLMNOPQRSTUVW
```

### The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the scheme, A → 0, B → 1, ..., Z → 25.[2] Encryption of a letter x by a shift n can be described mathematically as,[3]

### E(x)= n + x mod 26
### Decryption is performed similarly,
### ### E(x)= n - x mod 26

### The replacement remains the same throughout the message, so the cipher is classed as a type of monoalphabetic substitution, as opposed to polyalphabetic substitution.

## Usage
### Caesar ciphers can be found today in children's toys such as secret decoder rings. A Caesar shift of thirteen is also performed in the ROT13 algorithm, a simple method of obfuscating text widely found on Usenet and used to obscure text (such as joke punchlines and story spoilers), but not seriously used as a method of encryption
### The Vigenère cipher uses a Caesar cipher with a different shift at each position in the text; the value of the shift is defined using a repeating keyword. If the keyword is as long as the message, is chosen at random, never becomes known to anyone else, and is never reused, this is the one-time pad cipher, proven unbreakable. The conditions are so difficult they are, in practical effect, never achieved.
## Breaking the cipher
### The Caesar cipher can be easily broken even in a ciphertext-only scenario. Two situations can be considered:

1- an attacker knows (or guesses) that some sort of simple substitution cipher has been used, but not specifically that it is a Caesar scheme;
2- an attacker knows that a Caesar cipher is in use, but does not know the shift value.
### In the first case, the cipher can be broken using the same techniques as for a general simple substitution cipher, such as frequency analysis or pattern words. While solving, it is likely that an attacker will quickly notice the regularity in the solution and deduce that a Caesar cipher is the specific algorithm employed.
### In the second instance, breaking the scheme is even more straightforward. Since there are only a limited number of possible shifts (25 in English), they can each be tested in turn in a brute force attack. One way to do this is to write out a snippet of the ciphertext in a table of all possible shifts – a technique sometimes known as "completing the plain component". The example given is for the ciphertext "EXXEGOEXSRGI"; the plaintext is instantly recognisable by eye at a shift of four. Another way of viewing this method is that, under each letter of the ciphertext, the entire alphabet is written out in reverse starting at that letter. This attack can be accelerated using a set of strips prepared with the alphabet written down in reverse order. The strips are then aligned to form the ciphertext along one row, and the plaintext should appear in one of the other rows.