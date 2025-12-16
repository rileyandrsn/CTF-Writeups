# EVEN RSA CAN BE BROKEN???

- Year: 2025

- CTF: picoCTF

- Category: Cryptography

- Difficulty: Easy

  

## Overview

This challenge involved breaking an RSA encryption by exploiting an improperly generated modulus.

  

## Vulnerability

The vulnerability arises in the provided value n factored as p · 2, meaning one of the "primes" was the trivial prime of 2. This fundamentally weakened RSA's security, as it violated a requirement for secure RSA: n should be the product of two large primes. As a result, Euler's totient simplified to **ϕ**(n) = (p-1)·(2-1) = (p-1). With **ϕ**(n) known, the private exponent d can be computed as the modular inverse of e modulo p-1, allowing for a straightforward decryption of the provided ciphertext.

  

## Key Observation

The critical observation was that the modulus n, when analyzed using FactorDB, was composed of a large prime number (p) and the trivial prime 2.

  

## Approach

1. Identified the modulus n to be composite

2. Upon further analysis, discovered the values of p and the trivial prime of 2

3. Wrote a Python script to verify the values of p and 2, and calculate the private exponent d

4. Used the private exponent d and modulus n to decrypt the ciphertext into plaintext

  

## Why This Worked

RSA relies on the difficulty of factoring a modulus composed of two large prime numbers. In this challenge, the modulus was insecurely generated as n = p · 2, making it trivial to factor. Because one factor was 2, Euler's totient simplified to **ϕ**(n) = p - 1, which can be directly computed. Knowing **ϕ**(n) allows the private exponent d to be derived from the public exponent e, enabling me to decrypt the ciphertext.
  

## Key Takeaway

When generating an RSA public-private key pair, the modulus should be composed of two large prime numbers to increase the difficulty of computing the factors.

## Python Code

```python
from Crypto.Util.number import inverse, long_to_bytes

# given values
n =  17128535096756005524651844930361796834121371055987700334457406254480074049425818227220681239750301789350035449157668182384519264691747574818379872953458614
e =  65537
c =  6787292851215106862745645178047313196324306302752779837750316788956629167465449151629776063369354430030768693407430580617575455272358561831191263646879429

# found values
p =  8564267548378002762325922465180898417060685527993850167228703127240037024712909113610340619875150894675017724578834091192259632345873787409189936476729307
q =  2

print((p*q) == n) # True

d =  inverse(e, p-1) # compute d = e^-1 mod (p-1)

m =  pow(c, d, n) # decrypt ciphertext to plaintext

print(long_to_bytes(m)) # convert to readable format (flag)
```
