# Cryptography

## SHA256

- SHA stands for Secure Hash Algorithm and 256 is the number of the bits it takes up in memory.
- The hash is always 64 characters long and consists of digits and letters from A to F (Hexadecimal Hash).
- Each character takes 4 bits (2^4=16) and 4*64=256 bits.

## The 5 requirements for Hash algorithms

1. **One-way**: Only can be calculated to create hash but this hash can't be reversed to create data.
2. **Deterministic**: The result will be the same same no matter how many times it has been calculated.
3. **Fast Computation**: Hash calculation must be significantly fast.
4. **The Avalanche Effect**: Means that any tiny change would alter the result Hash completely.
5. Withstand collisions: As the number of possible different hashes is limited (exactly 16^64), so it is possible that there would be two different files may result into the same Hash. But it is very rare for this occurrence to happen and it is not possible for artificial collisions. Artificial collisions means that when pirates try to create data file that would result to the same Hash.
