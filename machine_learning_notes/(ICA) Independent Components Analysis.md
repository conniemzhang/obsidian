#machine_learning #notes 

High Level Story: Cocktail Party Problem -- separating voices from difference microphones based on intensity. Must have a known number of speakers $S_1, S_2$, etc. A known number of microphones pick up the speakers voices. Assume same number of speakers and microphones.

 We don't see $S_1, S_2$ time series, we only see $X_1^{(y)}, X_2^{(t)}$ the intensities over time at the microphones. Each microphone data point is a mixture of the speakers, for ex:
 $$X_j^{(t)} = a_{j1}S_1^{(t)} + a_{j2}S_2^{(t)}$$
 $X^{(t)} = AS^{(t)}$ where $X^{(t)}$ is the observed data, and both $A$ (mixture) and $S^{(t)}$ (speaker intensity) are latent variables.
>  **latent variables** are not directly measurable, and are inferred through observable variables.

### Formulation
Given $x^{(i)} ... x^{(n)} \in \mathbb{R}^d$ where $d$ is both the number of speakers and microphones.
Do: find $S^{(i)}...S^{(n)} \in \mathbb{R}^d$
and $A \in \mathbb{R^{dxd}}$ s.t. $x^{(t)} = As^{(t)}$ 
We call $A$ the mixing matrix, and $w = A^{-1}$ is the unmixing matrix.

Write $\mathbf{w} = \begin{pmatrix} w^T_1 \\ \vdots \\ w^T_d \end{pmatrix}$ so $S_j^{(t)} = \mathbf{w}_jx^{(t)}$ which is the inverse and what we need to multiply by.

Some Caveats:
* $A$ does not vary with time (we assume)
* there is inherent ambiguity in this model
	* Speaker 1 and Speaker 2 is opaque (no labels)
	* Can't determine absolute intensity because we multiple two things together. Can only know relative intensities because the mixing matrix multiplied by a scalar remains the same:
		* $(cA)(c^{-1}s^{(t)}) = As^{(t)}$
* **Speakers cannot be Gaussian**
	* $X^{(i)} \sim \mathcal{N}(\mu, AA^T) \rightarrow$ if $U^TU = I$, $AU$ generates the same data.
	* This means any rotation of A generates the same data
		* Gaussians are rotationally invariant

**Algorithm**: Gradient Descent & MLE

Detour: Something about transforming the PDF of one function to another one? You can calculate it by multiplying by the determinant. Then you can get the P(x) in terms of Px(wx)

A little unclear, see notes.

$$P(s) = \prod_{j=1}^{d}P_s(S_j)$$
$$P(s) = \prod_{j=1}^{d}P_s(\mathbf{w}x)(det(\mathbf{w}))$$
Key technical bit (g(x) can be any rotationally invariant function)
set $P_S(x) \propto g'(x)$ for $g(x) = (1 + e^{-x})^{-1}$
Solve
$$\ell(\mathbf{w}) = \sum_{t=1}^n\sum_{j=1}^{d}\log g'(\mathbf{w}_j x^{(t)}) + \log|\det(\mathbf{w})|$$
 