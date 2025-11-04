# Structural Calibration and Sigma Distribution of Even Perfect Numbers

This repository contains the reference implementation that goes with the paper **“Structural Calibration and Sigma Distribution of Even Perfect Numbers”**. The code shows how to detect even perfect numbers **without calling a separate Mersenne-prime routine**, by enforcing the structural constraints of the **sigma rectangle (SR)** and the **Discrete Hierarchical Tiling (DHT)** on triangular numbers. This approach is **conditioned on the classical Euclid–Euler characterization** of even perfect numbers.

---

## 1. What it does

- Enumerates **triangular numbers**  
  For odd `n`, we form
  $$T_n = \frac{n(n+1)}{2}, \qquad L = \frac{n+1}{2}, \qquad k = n,$$
  and we view $M = T_n$ as a candidate.

- Enforces the **even SR structure**  
  In the even perfect case the wide pillar is dyadic, so we require
  $$L = 2^a.$$
  This is the SR/DHT version of the Euclid–Euler shape.

- Checks the **median identity**  
  The sigma rectangle has a median column at $L/2$, and the small divisors below $L$ must be exactly the dyadic ones $\{1,2,4,\dots,L/2\}$. They satisfy
  $$(1 + 2 + \dots + L/2) + L = k,$$
  which forces
  $$k = 2L - 1,$$
  and therefore
  $$M = L(2L-1) = 2^a(2^{a+1}-1).$$

- Optionally checks the **calibration equality** from the paper  
  For even perfect numbers we have an exact formula for the largest proper divisor:
  $$R(L) = \frac{L(L+2)}{8}, \qquad
  \Theta(L) = 8 - \frac{20}{L+2}, \qquad
  GD(M) = \Theta(L)\,R(L).$$
  The code can evaluate this to confirm the certification numerically.

**Result:** under the Euclid–Euler characterization, whenever a triangular number passes these structural tests, the algorithm records it as an even perfect number — and it does so without using a dedicated Mersenne-primality subroutine.

---

## 2. Why this is interesting

Classically, even perfect numbers are obtained from Mersenne primes. The paper shows that in the even case the SR/DHT structure is strong enough to **reconstruct the Euclid–Euler form from local divisor geometry** (dyadic columns + median + calibration). The repo is the concrete version of that statement.

This repo corresponds to the “algorithm detection and enumeration” section of the paper:
1. extract an SR base $(k,L)$;
2. check DHT (dyadic pillar, median, signature);
3. check calibration;
4. rule out intruders by the local step formula.

---

## 3. How to run

- open the main Python script in this repo;
- set the scan limit (for instance on `n` or on the triangular value);
- run: the script will print the even perfect numbers it finds in order (6, 28, 496, 8128, …).

You can increase the limit to reach the larger known even perfect numbers. The structural tests stay simple because they only look at divisors **below** $L$ and at one explicit formula for the largest divisor.

---

## 4. Notes

- **6 is accepted**: it is triangular and perfect, so it passes the structural filter even though it is a degenerate case.
- **No new integer class**: the old working label “beautiful numbers” referred to “numbers that pass the SR filter”. In this repo we keep the classical name: these are **even perfect numbers**.
- **CPU-friendly**: all tests are local and integer-based. A faster version (vectorized / GPU) is possible because the SR checks are independent between candidates.

---

## 5. Reference

If you use this code, please cite the paper:

> Daniel Sautot, *Structural Calibration and Sigma Distribution of Even Perfect Numbers*, 2025.

and the earlier SR/DHT description:

> Daniel Sautot, *The Sigma Rectangle Framework and a Certified Descent Approach to Odd Perfect Numbers*, Zenodo, 2025, doi:10.5281/zenodo.17383511.
