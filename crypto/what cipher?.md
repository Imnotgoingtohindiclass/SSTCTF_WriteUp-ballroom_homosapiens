# what cipher?

## Challenge:
### my friend sent me this flag, I wonder what it means? vinegar{t1wzy3vl_15_ffu_wp+x3y_oy3i4m_4wxo0gex_w0+s_ey3_uliznyy3}

### flag format is xsstctf{REDACTED}

## Solution:
The first clue to solving this challenge is that the encrypted text starts with vinegar. Vinegar is a sour-tasting liquid made through the fermentation of ethanol by acetic acid bacteria. It is commonly used in cooking, cleaning, and food preservation. Not very useful in terms of cybersecurity and capture-the-flags. But from experience, we know that there is an encryption method which sounds similar to vinegar, called vigenere. 

Here is a breakdown of how a vigenere cipher works:

Say we are given a plaintext that we want to send to our ally which has to be encrypted quickly.
```
ATTACKATDAWN
```

In order to encrypt this, we need an encryption key. The lenght of the encryption key has to be equal to the lenght of the ciphertext. Let's say we pick the key `LEMON`. Since `ATTACKATDAWN` has 12 characters, while `LEMON` has 5 characters, we can repeat the key until it is equal to the lenght of the ciphertext, thus getting a key of:
```
LEMONLEMONLE
```

Each letter in the plaintext is shifted forward in the alphabet based on the corresponding letter in the key.

#### **Formula:**
For each letter at position `i`, encryption is performed as:
```
C_i = (P_i + K_i) mod 26
```
where:
- `C_i` = Ciphertext letter at position `i`
- `P_i` = Plaintext letter at position `i` (converted to a number: A=0, B=1, ..., Z=25)
- `K_i` = Key letter at position `i` (converted similarly)
- `mod 26` ensures values wrap around within the alphabet

| Plaintext | A | T | T | A | C | K | A | T | D | A | W | N |
|-----------|---|---|---|---|---|---|---|---|---|---|---|---|
| Key       | L | E | M | O | N | L | E | M | O | N | L | E |
| Shift     | +11 | +4 | +12 | +14 | +13 | +11 | +4 | +12 | +14 | +13 | +11 | +4 |
| Ciphertext| L | X | F | O | P | V | E | F | R | N | H | R |

So, the final ciphertext is:
```
LXFOPVEFRNHR
```

To decrypt, the process is reversed by shifting **backward** using the key.

#### **Formula:**
```
P_i = (C_i - K_i) mod 26
```
where:
- `P_i` = Decrypted plaintext letter at position `i`
- `C_i` = Ciphertext letter at position `i`
- `K_i` = Key letter at position `i`

Using the same example, we reverse the shifts and retrieve the original plaintext: **"ATTACKATDAWN"**.

Knowing how a vigenere cipher works allows us to reverse the key, and thus find the plaintext encoded to vinegar{t1wzy3vl_15_ffu_wp+x3y_oy3i4m_4wxo0gex_w0+s_ey3_uliznyy3}. Since we know that xsstctf is encoded to vinegar, we can figure out that the first 7 characters of the key is `YQVLEHM`.

Without any extra clues, it is impossible to figure out the rest of the key. But what we know from vigenere ciphers, is that if the lenght of the key is not equal to the lenght of the ciphertext, so it is not too far fetched to think that maybe this 7 character key `YQVLEHM` was repeated. 

Testing this theory, by decoding vinegar{t1wzy3vl_15_ffu_wp+x3y_oy3i4m_4wxo0gex_w0+s_ey3_uliznyy3} with YQVLEHM using [dCode](https://www.dcode.fr/vigenere-cipher).
This gives us the flag xsstctf{v1gen3re_15_the_be+t3r_ca3s4r_4lth0ugh_b0+h_ar3_insecur3}

flag: xsstctf{v1gen3re_15_the_be+t3r_ca3s4r_4lth0ugh_b0+h_ar3_insecur3}