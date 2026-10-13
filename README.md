<!-- solve-problem:21462b77-27f0-46c6-b895-ad405a0913e7 -->
# Sum-of-square-roots comparison in NP

A [Tangle Solve problem](https://solve.tangle.tools/problems/21462b77-27f0-46c6-b895-ad405a0913e7).

## What is the problem?

Given integers $a_1, \dots, a_n$ and integer coefficients $c_1, \dots, c_n$ (encoded in binary), decide whether $\sum_{i=1}^n c_i \sqrt{a_i}$ is positive, negative, or zero — and, crucially, decide it **within the complexity class NP**. Membership in decidability terms is trivial (the sign is a computable real quantity); the question is whether a "yes" instance admits a certificate verifiable in polynomial time. The natural certificate would be a precision bound: a rational $r$ and an integer $B$ such that if the sum is nonzero, its magnitude exceeds $2^{-B}$ with $B = \mathrm{poly}(\text{input length})$. Then approximating the sum to $B + O(1)$ bits settles the sign. Thus the problem reduces to: **prove (or disprove) a polynomial upper bound on the bits needed to separate such a sum from zero**, i.e., on $-\log \left| \sum_i c_i \sqrt{a_i} \right|$ when the sum is nonzero. The weaker task of computing the sign exactly (in exponential time) is known. Some formulations restrict to $c_i \in \{+1,-1\}$ and $a_i$ positive integers — the case arising from Euclidean lengths. Ambiguity note: "in NP" could also mean the decision problem with promise of nonzero sum; most work targets the promise version, since the zero case relates to (also hard) sum-of-radicals identity testing.

## Why does it matter?

Resolving it would settle the exact complexity of fundamental geometric optimization problems: the Euclidean traveling salesman problem, shortest paths among obstacles, and minimum-weight triangulation are known to lie in NP **only if** this comparison is in NP — computing tour/pertour lengths involves sums of $\sqrt{\text{integer}}$. NP-hardness of these problems (via rational reductions) combined with NP membership would give complete problems, restoring the standard completeness picture for exact Euclidean geometry. It also matters for exact algebraic computation: it is a prototypical case of the general "sign determination for succinct algebraic numbers" question, relevant to the complexity of numerical analysis and the counting hierarchy.

## What's already known?

- The problem was posed by O'Rourke (1981) as American Mathematical Monthly Problem 6369, motivated by exact TSP in the plane.
- The sign can be computed in exponential time (or PSPACE without better bounds) by repeated squaring / algebraic manipulation; the general algebraic-number machinery (resultants, isolating intervals) gives the sign but with exponentially large derived quantities in the worst analyzed cases — it does not yield polynomial bit bounds.
- The problem sits in the **counting hierarchy**: Allender, Bürgisser, Kjeldgaard-Pedersen, Miltersen (2009) show that various sums of radicals / numerical predicates lie in CH (specifically the PosSLP-style framework and results on arithmetic circuit comparison), placing the decision in $\mathrm{P}^{\mathrm{PP}}$-like classes. CH containment is the best known general upper bound; it is far above NP (unless CH collapses).
- A folklore bound: if the sum is nonzero, one can show the sum exceeds roughly $1/\prod(\text{something exponential})$ via norm arguments — the norm of $\sum c_i\sqrt{a_i}$ over its splitting field is a nonzero integer bounded by exponentially large quantities, giving an exponential (in $n$ and coefficient sizes) bit bound, hence exponential-time algorithms. The gap between exponential bounds and the conjectured polynomial bound is the entire problem.
- No nontrivial lower bound on complexity is known; no one has ruled out a polynomial bit bound.

## What would count as solving it?

1. **Upper bound / NP membership:** a proof that for any nonzero sum $\sum c_i\sqrt{a_i}$, $-\log\left|\sum c_i \sqrt{a_i}\right| = \mathrm{poly}(L)$ where $L$ is the total input bit length — plus (easy) a polynomial-time verifier using the bound. This settles the standard formulation.
2. **Sharper classification:** e.g., placement in the polynomial hierarchy PH, or a proof that the problem is complete for some class between NP and CH under appropriate reductions.
3. **Lower bound / structural result:** a proof that the problem is not in NP under some assumption (e.g., relative to an oracle), or hardness for CH.
4. **Partial results of interest:** polynomial bit bounds for restricted families (bounded $n$, repeated $a_i$ structure, coefficients in $\{-1,1\}$ with $a_i$ of bounded bit length) that strictly improve on the norm-based exponential bounds.

A referee would accept a rigorous bit-bound theorem with explicit polynomial dependence on $n$ and the $a_i, c_i$ bit lengths, or a completed reduction establishing a complexity classification.

## How to start

1. Read the ABKM 2009 paper, especially the treatment of PosSLP and sums of square roots — it shows how "comparison of succinctly represented algebraic numbers" sits in CH and what the technical barrier is (the norm/norm-trace argument degenerates).
2. Understand the norm argument precisely: for $\alpha = \sum c_i \sqrt{a_i}$, take the field norm $N(\alpha) \in \mathbb{Z} \setminus \{0\}$; the bound $|N(\alpha)| \le (\text{stuff})^{\deg}$ yields $|\alpha| \ge |N| / \prod_\sigma |\sigma(\alpha)|$. Analyze where cancellation can make conjugate values exponentially large relative to $\alpha$ — that's the loss.
3. Try small-$n$ and structured cases ($n = 2, 3$, pairwise-coprime squarefree $a_i$, $\pm 1$ coefficients) where exact analyses of conjugate growth are feasible; look for combinatorial structure in cancellations.
4. Main obstacle: there is no known technique controlling simultaneous cancellation across all conjugates; direct analytic bounds fail because the $c_i\sqrt{a_i}$ can nearly cancel. Consider whether an NP-hardness-in-the-other-direction (e.g., "sign of sum of radicals is CH-hard") is equally plausible.

## Key references

- Joseph O'Rourke, "Advanced Problem 6369," *American Mathematical Monthly* 88 (1981), 769 — the original problem statement asking for the complexity of comparing sums of square roots. (verify exact page)
- Eric Allender, Peter Bürgisser, Johan Kjeldgaard-Pedersen, Peter Bro Miltersen, "On the Complexity of Numerical Analysis," *SIAM Journal on Computing* 38(5), 2009 (preliminary version STOC 2006) — places PosSLP and related sum-of-radical comparison problems in the counting hierarchy and surveys the sum-of-square-roots problem. https://epubs.siam.org/doi/10.1137/070697853 (verify link)
- The Open Problems Project (TOPP), Problem 33, "Sum of square roots" — a maintained statement of the problem and its significance for Euclidean TSP being in NP. https://topp.openproblem.net/ (verify)
- (Background, optional) Peter Bürgisser and Felipe Cucker, work on condition numbers and the complexity of numerical computation — broader context for exact algebraic comparison. (verify relevance)

## Warnings

- The problem is about **certificates / bit bounds**, not about algorithms: exhibiting a polynomial-time algorithm is overkill (and would imply P = the relevant class trivially only for this promise problem); the crux is the separation-from-zero bound.
- Watch the zero case: certifying $\sum c_i \sqrt{a_i} = 0$ is related to polynomial identity testing–type questions; be explicit whether you work with a promise of nonzeroness.
- The norm argument gives $|\alpha| \ge 2^{-\mathrm{exp}}$; many attempted "solutions" in the literature incorrectly claim polynomial bounds by miscounting conjugate magnitudes. Carefully bound $\max_\sigma |\sigma(\alpha)|$.
- "In NP" here means over the standard binary encoding of inputs; real-RAM or unit-cost models change the answer trivially.
- Squarefree reduction: WLOG the $a_i$ are distinct squarefree positive integers (extract square factors into $c_i$), but this changes coefficient sizes — track the bit-length accounting through such normalizations.

---
*`ALGO-000156` · unverified*

## Acceptance guidance

1. **Upper bound / NP membership:** a proof that for any nonzero sum $\sum c_i\sqrt{a_i}$, $-\log\left|\sum c_i \sqrt{a_i}\right| = \mathrm{poly}(L)$ where $L$ is the total input bit length — plus (easy) a polynomial-time verifier using the bound. This settles the standard formulation.
2. **Sharper classification:** e.g., placement in the polynomial hierarchy PH, or a proof that the problem is complete for some class between NP and CH under appropriate reductions.
3. **Lower bound / structural result:** a proof that the problem is not in NP under some assumption (e.g., relative to an oracle), or hardness for CH.
4. **Partial results of interest:** polynomial bit bounds for restricted families (bounded $n$, repeated $a_i$ structure, coefficients in $\{-1,1\}$ with $a_i$ of bounded bit length) that strictly improve on the norm-based exponential bounds.

A referee would accept a rigorous bit-bound theorem with explicit polynomial dependence on $n$ and the $a_i, c_i$ bit lengths, or a completed reduction establishing a complexity classification.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/21462b77-27f0-46c6-b895-ad405a0913e7?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000156.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000156)
