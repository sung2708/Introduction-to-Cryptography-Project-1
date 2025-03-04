# PROJECT 1 - RSA

## 1. Prime Number Checking (4 points)

### 1.1 Definition of a Prime Number
A positive integer $n \in \mathbb{Z}^+$ is called a prime number if and only if it has exactly two positive divisors: 1 and itself.

#### Examples:
- **2, 3, 5, 7** are prime numbers because they have exactly two positive divisors: 1 and themselves.
- **1** is not a prime number because it has only one positive divisor: 1.
- **4, 6, 8** are not prime numbers because they have at least three positive divisors: 1, 2, and themselves.

### 1.2 Suggested Prime Number Checking Algorithms
Below are some algorithms for prime number checking that you may implement:

1. Brute-force algorithm.
2. Fermat's algorithm.
3. Miller-Rabin algorithm.
4. AKS algorithm.

You are allowed to use other prime number checking algorithms not listed above.

### 1.3 Problem Requirements
In this section, students are required to design a program to check whether a given positive integer $n \in \mathbb{Z}^+$ is a prime number. The program must meet the following requirements:

- The implementation must use the **C++** programming language. Any other programming language will not be accepted and will receive a score of **0**.
- Only standard libraries available up to **C++17** are allowed. Any other libraries used in the implementation will result in a score of **0**.
- The entire source code must be contained in a **single file** named `bai1.cpp`.
- After compiling the source code into `a.exe`, the program must be executed using the following command:
  ```sh
  .\a.exe test.inp test.out
  ```
  where `test.inp` is the input file containing the test data, and `test.out` is the output file storing the program's result.
- The maximum execution time for each test case is **60 seconds**. If the program exceeds this limit, the test case will not be counted for scoring.

### 1.3.1 Program Files
- **Input file (`test.inp`)** contains a single positive integer $n \in \mathbb{Z}^+$ represented in **uppercase hexadecimal format** in **big-endian** notation.
- **Output file (`test.out`)** contains:
  - `0` if the number is **not** a prime number.
  - `1` if the number **is** a prime number.

### 1.3.2 Examples

#### Example 1
**Input (`test.inp`)**:
```
65
```
**Output (`test.out`)**:
```
1
```
**Explanation**: `0x65 = 101`, which is a prime number, so the result is `1`.

#### Example 2
**Input (`test.inp`)**:
```
2406
```
**Output (`test.out`)**:
```
0
```
**Explanation**: `0x2406 = 9222 = 2 × 3 × 29 × 53`, which is not a prime number, so the result is `0`.

### 1.3.3 Constraints
- **35% of test cases (35% of total points)**: Input number is **64-bit long**.
- **25% of test cases (25% of total points)**: Input number is **128-bit long**.
- **20% of test cases (20% of total points)**: Input number is **256-bit long**.
- **15% of test cases (15% of total points)**: Input number is **512-bit long**.
- **5% of test cases (5% of total points)**: Input number is **1024-bit long**.

## 2. Key Generation for RSA System (2.5 points)

### 2.1 Definition of RSA Key Generation Algorithm

Let $p$ and $q$ be two large prime numbers such that $p \neq q$. Then, define:
- $N = p \cdot q$
- $\varphi(N) = (p - 1) \cdot (q - 1)$
- There exists a pair of positive integers $(e, d)$ where $e, d < \varphi(N) < N$ satisfying:
  \[ e \cdot d \equiv 1 \pmod{\varphi(N)} \]

From this, the public key of the RSA system is defined as the pair $(N, e)$, and the private key is the integer $d$.

### 2.2 Problem Requirements

In this section, students are required to design a program that generates the private key $d$ from two given large prime numbers $p, q$ and a given public exponent $e$. The program must meet the following requirements:

- The implementation must be in **C++**. Any other programming language will **not** be accepted, and the submission will receive **0 points**.
- Only standard libraries available in **C++17 or earlier** are allowed. The use of any other libraries will result in **0 points**.
- The entire source code must be contained in a single file named **bai2.cpp**.
- After compilation into an executable file **a.exe**, the program must be executed using the following command:
  ```sh
  .\a.exe test.inp test.out
  ```
  where `test.inp` is the input file, and `test.out` is the output file.
- The maximum execution time for each test case is **20 seconds**. If the program exceeds this limit, the test case will not be graded.

### 2.2.1 Program Files

- The file `test.inp` consists of **three lines**:
  1. The first line contains the prime number **p**.
  2. The second line contains the prime number **q**.
  3. The third line contains the public key exponent **e**.
  
  All numbers in this file are stored using **uppercase hexadecimal digits** in **big-endian format**.

- The program's output is stored in `test.out`. This file contains:
  - The **smallest positive integer** $d$ that satisfies the RSA key generation condition, stored in **uppercase hexadecimal digits** in **big-endian format**.
  - If no such $d$ exists, the output should be `-1`.

### 2.2.2 Example

#### **Example 1**

**Input (`test.inp`)**
```
9D
C1
17
```

**Output (`test.out`)**
```
60A7
```

**Explanation:**
- $p = 0x9D = 157$, $q = 0xC1 = 193$
- $\varphi(N) = (p - 1) \cdot (q - 1) = 29952$
- Given $e = 0x17 = 23$, the smallest valid $d = 24743 = 0x60A7$

#### **Example 2**

**Input (`test.inp`)**
```
1A7B
1E2F
208
```

**Output (`test.out`)**
```
-1
```

**Explanation:**
- $p = 0x1A7B = 6779$, $q = 0x1E2F = 7727$
- $\varphi(N) = (p - 1) \cdot (q - 1) = 52366828$
- Since $\gcd(e, \varphi(N)) = 4 \neq 1$, no valid $d$ exists, so the program outputs `-1`.

### 2.2.3 Constraints

- **40%** of test cases (40% of the total points) have prime numbers $p, q$ of **64-bit** length.
- **30%** of test cases (30% of the total points) have prime numbers $p, q$ of **128-bit** length.
- **15%** of test cases (15% of the total points) have prime numbers $p, q$ of **256-bit** length.
- **10%** of test cases (10% of the total points) have prime numbers $p, q$ of **512-bit** length.
- **5%** of test cases (5% of the total points) have prime numbers $p, q$ of **1024-bit** length.
- **All test cases guarantee that** $e < \min(p, q)$.

## 3RSA Encryption and Decryption (3.5 points)

### 3.1 RSA Encryption and Decryption Algorithm
The encryption and decryption algorithms in RSA operate similarly. A message \( m \) (or ciphertext \( c \)) is exponentiated with the public key \( e \) (or private key \( d \)) modulo \( N \).

- **Encryption Algorithm**:
  - Given a public key pair \( (N, e) \) generated in the key generation algorithm and a message \( m \in \mathbb{Z}^+ \) such that \( m < N \), the ciphertext \( c \in \mathbb{Z}^+ \) is computed as:
    \[ c = m^e \mod N \]

- **Decryption Algorithm**:
  - Given a public modulus \( N \) and a private key \( d \) generated in the key generation algorithm, and a ciphertext \( c \in \mathbb{Z}^+ \) such that \( c < N \), the original message \( m \in \mathbb{Z}^+ \) is retrieved as:
    \[ m = c^d \mod N \]

### 3.2 Problem Requirements
Since RSA encryption and decryption algorithms are straightforward, students will be given a more challenging task.

In this section, students must design a program to find a ciphertext \( c_j \) from a given array of ciphertexts after encrypting a message \( m_i \) using the given public key \( (N, e) \). The program must meet the following requirements:

- The implementation must be written in **C++**. Any other programming language will receive a score of **zero**.
- Only **standard libraries from C++17 or earlier** are allowed. Using any external libraries will result in a score of **zero**.
- The entire source code must be contained within a **single file** named `bai3.cpp`.
- After compilation into `a.exe`, the program must be executed using the following command:
  ```sh
  .\a.exe test.inp test.out
  ```
  where `test.inp` contains the input data and `test.out` stores the program's output.
- The maximum runtime for each test case is **60 seconds**. If the program exceeds this time limit, the test case will not be scored.

#### 3.2.1 Input and Output Files

- **Input File (`test.inp`)**:
  - The first line contains two positive integers **x** and **y**, stored as **big-endian decimal numbers**, representing the number of messages and the number of available ciphertexts, respectively.
  - The second line contains two hexadecimal uppercase numbers **N** and **e**, stored as **big-endian hexadecimal numbers**, representing the public key.
  - The next **x** lines each contain a message \( m_i \), stored as a **big-endian hexadecimal number**.
  - The next **y** lines each contain a ciphertext \( c_j \), stored as a **big-endian hexadecimal number**.

- **Output File (`test.out`)**:
  - A single line containing **x** elements, each representing the index \( j \) of the matching ciphertext in the given array such that:
    \[ c_j = m_i^e \mod N \]
    - If no match is found, output `-1`.

#### 3.2.2 Example

##### **Input (`test.inp`)**
```
3 10
105B 1F
42
A8
5D
A5F
E1C
EF3
67A
357
92B
E46
84A
7A1
C50
```

##### **Output (`test.out`)**
```
-1 4 9
```

##### **Explanation:**
Given messages:
```
[m_0 = 0x42, m_1 = 0xA8, m_2 = 0x5D] = [66, 168, 93]
```
Given ciphertexts:
```
[2655, 3612, 3827, 1658, 855, 2347, 3654, 2122, 1953, 3152]
```
Public key:
```
(N, e) = (0x105B, 0x1F) = (4187, 31)
```

- \( m_0 = 66 \) has no matching ciphertext, so output `-1`.
- \( m_1 = 168 \) has ciphertext \( c_4 = 855 \), since \( 168^{31} \mod 4187 = 855 \), so output `4`.
- \( m_2 = 93 \) has ciphertext \( c_9 = 3152 \), since \( 93^{31} \mod 4187 = 3152 \), so output `9`.

#### 3.2.3 Constraints

- **2 ≤ x ≤ 5, 10 ≤ y ≤ 20**
- **30% of test cases (30% of total score):** The modulus \( N \) has a bit length **≤ 64**.
- **30% of test cases (30% of total score):** The modulus \( N \) has a bit length **64 < |N| ≤ 128**.
- **20% of test cases (20% of total score):** The modulus \( N \) has a bit length **128 < |N| ≤ 256**.
- **10% of test cases (10% of total score):** The modulus \( N \) has a bit length **256 < |N| ≤ 512**.
- **10% of test cases (10% of total score):** The modulus \( N \) has a bit length **512 < |N| ≤ 1024**.
