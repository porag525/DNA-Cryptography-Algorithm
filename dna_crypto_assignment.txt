# DNA Cryptography Algorithm (DNACrypto)

## 1. Introduction
DNA Cryptography is an innovative security method inspired by biological DNA, which stores complex information using four chemical bases: Adenine (A), Thymine (T), Cytosine (C), and Guanine (G). This algorithm uses DNA-like sequences to securely encode plaintext messages with an additional layer of mutation for enhanced security.

---

## 2. Key Concepts

### DNA Base Mapping:
| Binary | DNA Base |
|--------|----------|
| 00     | A        |
| 01     | T        |
| 10     | C        |
| 11     | G        |

### Mutation Rules:
- **Complement:** A ⇆ T, C ⇆ G
- **Reverse:** Reverse the sequence (applied only for odd keys)

---

## 3. Encryption Algorithm (DNACrypto-Enc)

### Input:
- Plaintext `P`
- Key `K`

### Output:
- Ciphertext `C`

### Steps:
1. Convert each character in `P` to its 8-bit binary value.
2. Divide the binary into 2-bit chunks and map to DNA bases.
3. Apply mutations:
   - If `K` is **even**: Apply complement only.
   - If `K` is **odd**: Apply complement and reverse.
4. Concatenate the mutated sequences to produce `C`.

### Encryption Formula:
```
b_i = B(p_i)
d_i = D(b_i)
m_i = Comp(d_i)                if K % 2 == 0
m_i = Rev(Comp(d_i))           if K % 2 == 1
C = {m_1, m_2, ..., m_n}
```

---

## 4. Decryption Algorithm (DNACrypto-Dec)

### Input:
- Ciphertext `C`
- Key `K`

### Output:
- Plaintext `P`

### Steps:
1. Split the ciphertext into individual DNA sequences.
2. Apply reverse mutations:
   - If `K` is **even**: Apply complement only.
   - If `K` is **odd**: Reverse then complement.
3. Map DNA bases back to binary.
4. Convert binary to ASCII characters.

### Decryption Formula:
```
d_i = Comp(m_i)                 if K % 2 == 0
d_i = Comp(Rev(m_i))            if K % 2 == 1
b_i = D^-1(d_i)
p_i = B^-1(b_i)
P = {p_1, p_2, ..., p_n}
```

---

## 5. Dry Run Example

### Plaintext: `"Algorithm"`
### Key: 5 (odd)

### Step 1: ASCII to Binary
| Character | ASCII | Binary      |
|-----------|-------|------------|
| A         | 65    | 01000001   |
| l         | 108   | 01101100   |
| g         | 103   | 01100111   |
| o         | 111   | 01101111   |
| r         | 114   | 01110010   |
| i         | 105   | 01101001   |
| t         | 116   | 01110100   |
| h         | 104   | 01101000   |
| m         | 109   | 01101101   |

### Step 2: Binary to DNA Mapping
| Binary       | DNA     |
|-------------|---------|
| 01000001    | T A A T |
| 01101100    | T C G A |
| 01100111    | T C T G |
| 01101111    | T C G G |
| 01110010    | T G A C |
| 01101001    | T C C T |
| 01110100    | T G T A |
| 01101000    | T C C A |
| 01101101    | T C G T |

### Step 3: Apply Mutation (Key = 5, odd)
| Original | Complemented | Reversed |
|----------|--------------|----------|
| TAAT     | ATTA         | ATTA     |
| TCGA     | AGCT         | TCGA     |
| TCTG     | AGAC         | CAGA     |
| TCGG     | AGCC         | CCGA     |
| TGAC     | ACTG         | GTCA     |
| TCCT     | AGGA         | AGGA     |
| TGTA     | ACAT         | TACA     |
| TCCA     | AGGT         | TGGA     |
| TCGT     | AGCA         | ACGA     |

### Step 4: Final Ciphertext:
```
ATTA TCGA CAGA CCGA GTCA AGGA TACA TGGA ACGA
```

---

## 6. Decryption Dry Run (for 'ATTA')
1. Reverse: ATTA (odd key)
2. Complement: TAAT
3. DNA to Binary: 01 00 00 01 → 01000001 → 'A'

---

## 7. Advantages
- Bio-inspired, visually intuitive.
- Multi-layered security.
- Easy to implement in code.

---

## 8. Limitations
- Suitable for short messages.
- Requires secure key sharing.

---

## 9. Applications
- Secure messaging.
- Steganography.
- Educational cryptography models.

---

## 10. Flowchart Overview
```
Plaintext → Binary → DNA → Mutation → Ciphertext
Ciphertext → Reverse Mutation → Binary → Plaintext
