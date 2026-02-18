# Eigenvalues and Eigenvectors

## Introduction

Imagine you have a machine that takes in arrows (vectors) and spits out new arrows. Most arrows that go in come out pointing in a completely different direction — rotated, stretched, flipped, some combination of all three. But a few special arrows come out pointing in *exactly the same direction* they went in. They might be longer or shorter, maybe flipped backwards, but the direction is preserved. Those special arrows are **eigenvectors**, and the factor by which they're stretched is the **eigenvalue**.

Why should you care? Because these special directions reveal the *skeleton* of what a transformation actually does. Strip away all the complexity of a matrix — the mixing of coordinates, the rotation, the shearing — and what remains are a handful of directions that the matrix treats simply: just scale, no rotate.

This turns out to be one of the most powerful ideas in applied mathematics. Without eigenvalues and eigenvectors:

- **Google's PageRank** wouldn't work — it relies on finding the dominant eigenvector of the web's link matrix.
- **Principal Component Analysis (PCA)** couldn't reduce a 1,000-dimensional dataset to a manageable handful of dimensions.
- **Differential equations** describing everything from bridge vibrations to population dynamics would be vastly harder to solve.
- **Quantum mechanics** would lack its mathematical language — observable quantities literally *are* eigenvalues.

The reason is always the same: eigenvalues and eigenvectors decompose something complicated into a sum of simple, independent parts.

---

## Core Concepts

### What a matrix "does" to a vector

A matrix $A$ is a function that eats a vector and produces a new vector. For a 2×2 matrix, it takes a 2D arrow and returns a different 2D arrow:

```
A · v = w
```

Most of the time, `w` points somewhere completely different from `v`. The matrix has both rotated and scaled it.

### The special directions

An eigenvector $v$ is a nonzero vector where the matrix *doesn't* change the direction — it only scales:

```
A · v = λ · v
```

The scalar $λ$ (lambda) is the eigenvalue. It tells you *how much* the eigenvector gets stretched:

| λ value | What happens to v |
|---------|-------------------|
| λ = 3 | Stretched to 3× its length |
| λ = 1 | Unchanged — a fixed point of the transformation |
| λ = 0 | Crushed to the zero vector (v is in the null space) |
| λ = −1 | Flipped to point the opposite way |
| λ = 0.5 | Shrunk to half its length |

**Key insight:** The eigenvector defines a *direction*. Any scalar multiple of an eigenvector is also an eigenvector with the same eigenvalue. So we're really talking about *eigenlines* (or eigenspaces), not individual arrows.

### Why "eigen"?

"Eigen" is German for "own" or "characteristic." An eigenvector is a vector that is *characteristic* of the transformation — it reveals the transformation's own, intrinsic behavior.

### How to find them

Rearrange $A v = λ v$ into:

```
(A - λI) v = 0
```

For a nonzero solution $v$ to exist, the matrix $(A - λI)$ must be singular — it must squish some nonzero vector to zero. That happens exactly when:

```
det(A - λI) = 0
```

This is called the **characteristic equation**. For an $n \times n$ matrix, it's a polynomial of degree $n$ in $λ$, so there are at most $n$ eigenvalues (counting multiplicity, and allowing complex numbers).

**The recipe:**
1. Write out $A - λI$
2. Compute the determinant and set it to zero
3. Solve the resulting polynomial for $λ$ — those are the eigenvalues
4. For each $λ$, solve $(A - λI)v = 0$ to find the eigenvectors

### A mental model: the stretching skeleton

Think of a 2D transformation as doing two things simultaneously: stretching along the eigenvector directions, each by its own eigenvalue. *Every* vector in the plane is some combination of the eigenvectors, so *every* output is determined by just those two stretches.

```
            eigenvector v₁ (λ₁ = 2)
                 ↑  stretched 2×
                 |
                 |
  ───────────────┼──────────────→  eigenvector v₂ (λ₂ = 0.5)
                 |                  shrunk to 0.5×
                 |
```

Any input vector is a blend of $v_1$ and $v_2$. The matrix stretches the $v_1$ component by 2 and the $v_2$ component by 0.5, independently. That decomposition into independent, simple operations is the entire power of the idea.

### Diagonalization: the payoff

If a matrix $A$ has $n$ linearly independent eigenvectors, you can write:

```
A = P D P⁻¹
```

where $D$ is a diagonal matrix of eigenvalues and $P$ is the matrix whose columns are the eigenvectors. This is called **diagonalization**, and it's enormously useful because:

- **Powers of A** become trivial: $A^k = P D^k P^{-1}$, and raising a diagonal matrix to a power just raises each diagonal entry to that power.
- **Matrix exponentials** (critical for differential equations) decompose the same way.
- **Understanding** the transformation becomes direct — you're just reading off stretches along independent axes.

---

## Examples

### Example 1: A 2×2 matrix by hand

Let:

```
A = | 2  1 |
    | 1  2 |
```

**Step 1 — Characteristic equation:**

```
A - λI = | 2-λ   1  |
         |  1   2-λ |

det(A - λI) = (2-λ)(2-λ) - (1)(1)
            = λ² - 4λ + 4 - 1
            = λ² - 4λ + 3
            = (λ - 1)(λ - 3)
```

Eigenvalues: **λ₁ = 1** and **λ₂ = 3**.

**Step 2 — Eigenvectors:**

For λ₁ = 1:
```
(A - 1·I)v = | 1  1 | |v₁|   |0|
             | 1  1 | |v₂| = |0|

→ v₁ + v₂ = 0  →  v₁ = [-1, 1]ᵀ  (or any scalar multiple)
```

For λ₂ = 3:
```
(A - 3·I)v = | -1  1 | |v₁|   |0|
             |  1 -1 | |v₂| = |0|

→ -v₁ + v₂ = 0  →  v₂ = [1, 1]ᵀ  (or any scalar multiple)
```

**Interpretation:** This matrix stretches things along the diagonal $[1,1]$ by a factor of 3, and along the anti-diagonal $[-1,1]$ by a factor of 1 (leaves it alone). It's a stretch in one direction and identity in the perpendicular direction.

### Example 2: Rotation has no real eigenvectors

Consider a 90° rotation matrix:

```
R = | 0  -1 |
    | 1   0 |
```

Characteristic equation:
```
det(R - λI) = λ² + 1 = 0  →  λ = ±i
```

The eigenvalues are *complex* ($i$ and $-i$). There's no real-valued direction that stays pointing the same way after a 90° rotation — and that's exactly what the math tells you. Every real arrow gets rotated, none are preserved.

This isn't a failure of the theory. It's the theory correctly telling you: "This transformation has no preferred real directions."

### Example 3: Computing A¹⁰⁰ the easy way

Going back to Example 1, suppose you need $A^{100}$. Doing 100 matrix multiplications would be painful. But with diagonalization:

```
A = PDP⁻¹

where P = | -1  1 |    D = | 1  0 |
          |  1  1 |        | 0  3 |

A¹⁰⁰ = P D¹⁰⁰ P⁻¹ = P | 1    0   | P⁻¹
                         | 0   3¹⁰⁰ |
```

Raising a diagonal matrix to a power is trivial — you just raise each entry. This turns an intractable computation into a simple one.

### Example 4: Fibonacci numbers from eigenvalues

The Fibonacci recurrence $F_{n+1} = F_n + F_{n-1}$ can be written as a matrix equation:

```
| Fₙ₊₁ |   | 1  1 | | Fₙ   |
| Fₙ   | = | 1  0 | | Fₙ₋₁ |
```

The eigenvalues of this matrix are $\phi = \frac{1+\sqrt{5}}{2} \approx 1.618$ (the golden ratio) and $\hat{\phi} = \frac{1-\sqrt{5}}{2} \approx -0.618$. This directly gives you the closed-form formula:

```
Fₙ = (φⁿ - φ̂ⁿ) / √5
```

The dominant eigenvalue $\phi$ explains why Fibonacci numbers grow at rate $\approx 1.618^n$ — and why consecutive Fibonacci ratios converge to the golden ratio.

---

## Summary

### Key takeaways

1. **Eigenvectors are the directions a matrix treats simply** — scale only, no rotation. Eigenvalues are the scale factors.
2. **They reveal the skeleton of a transformation.** Every vector's fate is determined by how it decomposes along the eigenvector directions.
3. **The characteristic equation** $\det(A - \lambda I) = 0$ finds eigenvalues; back-substitution finds eigenvectors.
4. **Diagonalization** ($A = PDP^{-1}$) is the practical payoff — it makes powers, exponentials, and analysis of a matrix straightforward.
5. **Complex eigenvalues** aren't a problem — they indicate rotation, which is genuinely present in the transformation.

### Common pitfalls

- **Eigenvectors are directions, not unique vectors.** Any nonzero scalar multiple of an eigenvector is also an eigenvector. Don't be surprised when two sources give "different" eigenvectors for the same matrix.
- **Not every matrix is diagonalizable.** If a matrix doesn't have $n$ linearly independent eigenvectors (the "defective" case), you need Jordan normal form instead.
- **Zero can be an eigenvalue.** It means the matrix sends some nonzero vector to zero — the matrix is singular. Don't confuse "eigenvalue of zero" with "has no eigenvalue."
- **Eigenvalues of symmetric matrices are always real.** If your matrix is symmetric and you're getting complex eigenvalues, check your arithmetic.

### Where to go next

- **Singular Value Decomposition (SVD):** Generalizes eigendecomposition to rectangular matrices. Every matrix has an SVD, even non-square and defective ones.
- **Spectral theorem:** For symmetric matrices, eigenvectors are always orthogonal — this is the foundation of PCA.
- **Jordan normal form:** What happens when diagonalization fails — the next-best decomposition.
- **Matrix exponentials:** Used everywhere in differential equations and dynamical systems, built directly on eigendecomposition.
