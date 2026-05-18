# Notation guide

## General rules

- Keep notation consistent across the manuscript.
- Avoid bold math symbols.
- Do not reuse a symbol for different quantities.
- Define every variable, matrix, operator, and hyperparameter before first use.
- State dimensions when a variable or matrix is introduced.

## Dimensions

| Symbol | Meaning |
|---|---|
| `M` | number of microphones |
| `N` | number of focus-grid points |
| `J` | number of sources |
| `K` | number of snapshots |
| `F` | number of frequency bins |
| `L` | number of unfolded iterations / network layers |

Do not use lowercase `m` and `n` for these quantities.

## Core symbols

| Symbol | Meaning |
|---|---|
| `C \in \mathbb{C}^{M \times M}` | true microphone CSM |
| `\hat{C} \in \mathbb{C}^{M \times M}` | estimated microphone CSM |
| `Q \in \mathbb{C}^{N \times N}` | true source CSM |
| `\hat{Q} \in \mathbb{C}^{N \times N}` | estimated source CSM |
| `x \in \mathbb{R}_+^N` | true source-strength vector |
| `\hat{x} \in \mathbb{R}_+^N` | estimated source-strength vector |
| `H \in \mathbb{C}^{M \times N}` | propagation matrix on the focus grid |
| `A \in \mathbb{R}^{M^2 \times N}` | real-valued CMF sensing matrix |
| `y \in \mathbb{R}^{M^2}` | vectorized CSM data |
| `\sigma^2` | spatially white noise variance |
| `\lambda` | regularization parameter |

Under the incoherent-source CMF model, use `Q = \operatorname{diag}(x)`.
For CMF-C, keep `Q` as a full positive-semidefinite matrix and do not replace it by `\operatorname{diag}(x)`.

## Matrix and operator conventions

- Use lowercase letters for vectors and uppercase letters for matrices.
- Use `(\cdot)^\mathsf{H}` for the Hermitian transpose.
- Use `(\cdot)^\mathsf{T}` only for real-valued transpose.
- Use `(\cdot)^*` for complex conjugation.
- Use `\mathbb{E}\{\cdot\}` for expected value.
- Use `\operatorname{diag}(x)` to build a diagonal matrix from a vector.

## Propagation model

Use the free-field transfer coefficient with reference location

\[
H_{m,n} = \frac{r_{0,n}}{r_{m,n}} \exp\!\bigl(-\mathrm{i}k(r_{m,n}-r_{0,n})\bigr),
\]

where `r_{m,n}` is the distance from focus-grid point `n` to microphone `m` and `r_{0,n}` is the distance from focus-grid point `n` to the reference location.

## CMF structure

Use

\[
C = H Q H^\mathsf{H} + \sigma^2 I
\]

and, under the incoherent-source assumption,

\[
C = H \operatorname{diag}(x) H^\mathsf{H} + \sigma^2 I
= \sum_{n=1}^{N} x_n h_n h_n^\mathsf{H} + \sigma^2 I ,
\]

where `h_n` is the `n`th column of `H`.

Introduce `A` columnwise as

\[
A = [a_1,\dots,a_N], \qquad a_n = \mathcal{V}(h_n h_n^\mathsf{H}),
\]

with the elementwise matrix entry

\[
(h_n h_n^\mathsf{H})_{i,j} = H_{i,n} H_{j,n}^* .
\]

## Vectorization

- Define the vectorization operator `\mathcal{V}` explicitly when first used.
- For CMF, `\mathcal{V}` must match the Acoular implementation:
  stack the real parts of the upper-triangular CSM entries including the diagonal, then the imaginary parts of the strict upper-triangular entries.
- With this convention, `y = \mathcal{V}(\hat{C}) \in \mathbb{R}^{M^2}`.
- If diagonal removal is discussed later, define it as a separate operator and do not reuse the same symbol silently.

## Optimization problems

Use the full CMF model with `\sigma^2 I` before introducing the sparse least-squares form.

For sparse reconstruction, use

\[
\hat{x} = \arg\min_{x \geq 0} \frac{1}{2}\|Ax-y\|_2^2 + \lambda \|x\|_1 .
\]

Estimates use `\hat{\cdot}` throughout.

## Iterative algorithms

- Superscripts in parentheses, e.g. `x^{(k)}`, denote iteration index `k`.
- Subscripts denote element or layer index where the context is clear.
- Learnable parameters of a DUN use calligraphic letters, e.g. `\mathcal{W}`.
