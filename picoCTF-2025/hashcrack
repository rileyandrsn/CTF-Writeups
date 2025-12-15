
# hashcrack
- Year: 2025
- CTF: picoCTF
- Category: Cryptography
- Difficulty: Easy

## Overview
This challenge required recovering plaintext passwords from three consecutive cryptographic hashes in order to access a protected secret.

## Vulnerability
The hashes provided were generated using fast, general-purpose cryptographic hash functions (MD5, SHA-1, and SHA-256) without salting. These algorithms are vulnerable to dictionary and brute-force attacks because they prioritize speed rather than password storage.

## Key Observation
I observed that all three hashing algorithms were fast and unsalted, making them ideal candidates for offline dictionary attacks using common password wordlists.

## Approach
1. Identified the hashing algorithm used for each hash using *HashID*
2. Selected a dictionary attack using the *rockyou.txt* wordlist due to the attack model
3. Utilized John the Ripper to recover the plaintext passwords for each hash
4. Repeated steps 1-3 for each hash, using the recovered plaintext as input for the next stage

## Why This Worked
Fast hash functions such as MD5, SHA-1, and SHA-256 are computationally inexpensive to evaluate, allowing an attacker to test a large number of password guesses quickly in an offline attack. When passwords are weak or reused, dictionary attacks can recover plaintext passwords in seconds.

## Key Takeaway
Passwords should be stored using specifically designed password hashing functions such as Argon2 and bcrypt, using salts, additional random data fed into the hash function. This prevents dictionary attacks and makes brute-force password-cracking computationally expensive.
