# PROJECT 1 - RSA

## 1. Prime Number Checking (4 points)

### 1.1 Definition of a Prime Number
A positive integer $n \in \mathbb{Z}^+$ is called a prime number if and only if it has exactly two positive divisors: $1$ and itself.

#### Examples:
* **2, 3, 5, 7** are prime numbers because they have exactly two positive divisors: $1$ and themselves.
* **1** is not a prime number because it has only one positive divisor: $1$.
* **4, 6, 8** are not prime numbers because they have at least three positive divisors: $1$, $2$, and themselves.

### 1.2 Suggested Prime Number Checking Algorithms
Below are some algorithms for prime number checking that you may implement:

1.  Brute-force algorithm.
2.  Fermat's algorithm.
3.  Miller-Rabin algorithm.
4.  AKS algorithm.

You are allowed to use other prime number checking algorithms not listed above.

### 1.3 Problem Requirements
In this section, students are required to design a program to check whether a given positive integer $n \in \mathbb{Z}^+$ is a prime number. The program must meet the following requirements:

* The implementation must use the **C++** programming language. Any other programming language will not be accepted and will receive a score of **0**.
* Only standard libraries available up to **C++17** are allowed. Any other libraries used in the implementation will result in a score of **0**.
* The entire source code must be contained in a **single file** named `bai1.cpp`.
* After compiling the source code into `a.exe`, the program must be executed using the following command:
    ```sh
    .\a.exe test.inp test.out
    ```
    where `test.inp` is the input file containing the test data, and `test.out` is the output file storing the program's result.
* The maximum execution time for each test case is **60 seconds**. If the program exceeds this limit, the test case will not be counted for scoring.

#### 1.3.1 Program Files
* **Input file (`test.inp`)** contains a single positive integer $n \in \mathbb{Z}^+$ represented in **uppercase hexadecimal format** in **big-endian** notation.
* **Output file (`test.out`)** contains:
    * `0` if the number is **not** a prime number.
    * `1` if the number **is** a prime number.

#### 1.3.2 Examples

**Example 1**
* **Input (`test.inp`)**: `65`
* **Output (`test.out`)**: `1`
* **Explanation**: $0x65 = 101$ in decimal, which is a prime number, so the result is $1$.

**Example 2**
* **Input (`test.inp`)**: `2406`
* **Output (`test.out`)**: `0`
* **Explanation**: $0x2406 = 9222 = 2 \times 3 \times 29 \times 53$ in decimal, which is not a prime number, so the result is $0$.

#### 1.3.3 Constraints
* **35% of test cases**: Input number is **64-bit** long.
* **25% of test cases**: Input number is **128-bit** long.
* **20% of test cases**: Input number is **256-bit** long.
* **15% of test cases**: Input number is **512-bit** long.
* **5% of test cases**: Input number is **1024-bit** long.

---

## 2. Key Generation for RSA System (2.5 points)

### 2.1 Definition of RSA Key Generation Algorithm
Let $p$ and $q$ be two large prime numbers such that $p \neq q$. Then, define:
* $N = p \cdot q$
* $\phi(N) = (p - 1) \cdot (q - 1)$
* There exists a pair of positive integers $(e, d)$ where $e, d < \phi(N) < N$ satisfying:
    $$e \cdot d \equiv 1 \pmod{\phi(N)}$$

From this, the public key of the RSA system is defined as the pair $(N, e)$, and the private key is the integer $d$.

### 2.2 Problem Requirements
In this section, students are required to design a program that generates the private key $d$ from two given large prime numbers $p, q$ and a given public exponent $e$.

* The implementation must be in **C++** (Standard **C++17** or earlier).
* The entire source code must be contained in a single file named `bai2.cpp`.
* Execution command:
    ```sh
    .\a.exe test.inp test.out
    ```
* The maximum execution time for each test case is **20 seconds**.

#### 2.2.1 Program Files
* **Input (`test.inp`)** consists of three lines ($p, q, e$) in **uppercase hexadecimal, big-endian**.
* **Output (`test.out`)**:
    * The **smallest positive integer** $d$ satisfying the condition, in **uppercase hexadecimal**.
    * If no such $d$ exists, output `-1`.

#### 2.2.2 Example

**Example 1**
* **Input**:
    ```
    9D
    C1
    17
    ```
* **Output**: `60A7`
* **Explanation**:
    * $p = 0x9D = 157$, $q = 0xC1 = 193$
    * $\phi(N) = (p - 1) \cdot (q - 1) = 156 \cdot 192 = 29952$
    * Given $e = 0x17 = 23$, the smallest valid $d$ satisfying $23 \cdot d \equiv 1 \pmod{29952}$ is $d = 24743 = 0x60A7$.

**Example 2**
* **Input**:
    ```
    1A7B
    1E2F
    208
    ```
* **Output**: `-1`
* **Explanation**:
    * $p = 0x1A7B = 6779$, $q = 0x1E2F = 7727$
    * $\phi(N) = (p - 1) \cdot (q - 1) = 6778 \cdot 7726 = 52366828$
    * Since $\gcd(e, \phi(N)) = \gcd(520, 52366828) = 4 \neq 1$, no valid modular inverse $d$ exists, so the program outputs `-1`.

#### 2.2.3 Constraints
* **40%**: $p, q$ have a length of **64-bit**.
* **30%**: $p, q$ have a length of **128-bit**.
* **15%**: $p, q$ have a length of **256-bit**.
* **10%**: $p, q$ have a length of **512-bit**.
* **5%**: $p, q$ have a length of **1024-bit**.
* **Note**: All test cases guarantee that $e < \min(p, q)$.

---

## 3. RSA Encryption and Decryption (3.5 points)

### 3.1 RSA Encryption and Decryption Algorithm
* **Encryption**: Given public key $(N, e)$ and message $m < N$:
    $$c = m^e \pmod{N}$$
* **Decryption**: Given modulus $N$ and private key $d$:
    $$m = c^d \pmod{N}$$

### 3.2 Problem Requirements
Design a program to find the index of a ciphertext $c_j$ from a given array that matches a message $m_i$ after it has been encrypted using the public key $(N, e)$.

* Language: **C++** (Standard **C++17** or earlier).
* File name: `bai3.cpp`.
* Execution command:
    ```sh
    .\a.exe test.inp test.out
    ```
* Maximum runtime: **60 seconds** per test case.

#### 3.2.1 Input and Output Files
* **Input (`test.inp`)**:
    1.  Line 1: $x$ (number of messages) and $y$ (number of ciphertexts) in **decimal**.
    2.  Line 2: $N$ and $e$ in **uppercase hexadecimal**.
    3.  Next $x$ lines: Each line is a message $m_i$ in **hexadecimal**.
    4.  Next $y$ lines: Each line is a ciphertext $c_j$ in **hexadecimal**.
* **Output (`test.out`)**:
    * A single line containing $x$ space-separated indices. For each $m_i$, output the index $j$ (starting from $0$) such that $c_j = m_i^e \pmod{N}$. If no match is found for a message, output `-1`.

#### 3.2.2 Example
* **Input**:
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
* **Output**: `-1 4 9`
* **Explanation**:
    * Given messages: $[m_0 = 0x42, m_1 = 0xA8, m_2 = 0x5D] = [66, 168, 93]$ in decimal.
    * Public key: $(N, e) = (0x105B, 0x1F) = (4187, 31)$.
    * Calculation:
        1. $m_0 = 66^{31} \pmod{4187} = 3450$. $3450$ is not in the ciphertext list, so output `-1`.
        2. $m_1 = 168^{31} \pmod{4187} = 855$. $855 = 0x357$ is $c_4$ in the list, so output `4`.
        3. $m_2 = 93^{31} \pmod{4187} = 3152$. $3152 = 0xC50$ is $c_9$ in the list, so output `9`.

#### 3.2.3 Constraints
* $2 \le x \le 5, 10 \le y \le 20$.
* **30%**: $|N| \le 64$ bits.
* **30%**: $64 < |N| \le 128$ bits.
* **20%**: $128 < |N| \le 256$ bits.
* **10%**: $256 < |N| \le 512$ bits.
* **10%**: $512 < |N| \le 1024$ bits.
