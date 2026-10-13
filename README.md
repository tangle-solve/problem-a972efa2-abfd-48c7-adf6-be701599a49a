<!-- solve-problem:a972efa2-abfd-48c7-adf6-be701599a49a -->
# A 4/3 approximation for metric TSP

A [Tangle Solve problem](https://solve.tangle.tools/problems/a972efa2-abfd-48c7-adf6-be701599a49a).

## What is the problem?

The **symmetric metric Traveling Salesperson Problem (TSP)**: given a complete undirected graph on n vertices with edge weights satisfying the triangle inequality (c(u,v) ≤ c(u,w) + c(w,v)), find a Hamiltonian cycle of minimum total weight. The task: design a **polynomial-time algorithm that always returns a tour of cost at most (4/3)·OPT**, where OPT is the optimal tour cost. This is conjectured to be the right answer because the best inapproximability bound is only 1235/1234 ≈ 1.0036 (Karpinski–Lampis–Schmied, for metric TSP; verify exact constant), so a 4/3 (or even better) algorithm is not ruled out. Note variants: this is the *symmetric* metric case; the *graph-TSP* special case (shortest-path metric of an unweighted graph) already has a 4/3-approximation by Mömke–Svensson and a tight 7/5 by Sebő–Vygen. The open problem is the general metric setting.

## Why does it matter?

Metric TSP is arguably the most-studied problem in approximation algorithms; the ratio 3/2 stood unimproved for 44 years (1976–2020) and is taught as the canonical example. A 4/3 algorithm would likely require fundamentally new structural ideas (e.g., a principled way to combine matching with parity correction) that would transfer to vehicle routing, network design, and ATSP. Practically, even tiny asymptotic improvements in TSP approximations influence heuristics and integer-programming cut generation used daily in logistics.

## What's already known?

- **Christofides (1976):** compute a minimum spanning tree, a minimum-weight perfect matching on its odd-degree vertices, take an Eulerian walk, shortcut. Ratio 3/2. Matching lower bounds: on worst instances this analysis is tight.
- **Karlin–Klein–Oveis Gharan (2021, STOC):** broke the barrier with ratio 3/2 − ε for ε ≈ 10⁻³⁶. They randomly sample the spanning tree from a maximum-entropy distribution and analyze the matching via graph fattening. The point is the technique: randomness in tree selection beats deterministic MST.
- **Traub–Vygen (2022) and subsequent work:** further improvements; the current best ratio is roughly 1.5 − 10⁻³⁴ (verify current record, it moves slowly). Traub–Vygen's monograph (2024) surveys the whole landscape.
- **Graph-TSP:** 1.4 (Mömke–Svensson), 1.4−ε (Mucha), 7/5 (Sebő–Vygen, 2014) — tight up to ε.
- Known structural approach: the "best-of-many" Christofides, Subtour LP integrality ratio conjectured to be 4/3 (currently bounded between 4/3 and 1.5; verify latest). Wolleb's 2023 analysis of the Subtour LP for graph-TSP gives 4/3 for that case.

## What would count as solving it?

A polynomial-time (possibly randomized) algorithm A and a proof that for every metric instance, E[cost(A(I))] ≤ (4/3)·OPT(I). Acceptable variants in increasing difficulty:
1. A deterministic 4/3-approximation for general metrics.
2. A randomized 4/3-approximation in expectation.
3. An algorithm achieving (4/3 + ε) for arbitrary ε > 0 (a "4/3-asymptotic" result).
4. Also valuable: proving the Subtour LP integrality gap is ≤ 4/3, since a strong LP rounding could then give the algorithm.
A referee needs a complete correctness and ratio analysis; heuristic/experimental evidence does not suffice.

## How to start

1. Read Traub–Vygen's monograph *Approximation Algorithms for Traveling Salesman Problems* (2024), especially chapters on symmetric metric TSP, graph-TSP, and the KKO technique — this is the single best map of the field.
2. Understand the KKO analysis in depth: the maximum-entropy spanning tree distribution, the "fattening" of the induced matching polytope, and exactly where their ε comes from — their slack is the natural place to push.
3. Study the Sebő–Vygen 7/5 graph-TSP proof; its "matroid parity / removable pairing" machinery may generalize beyond graph metrics.
4. Main obstacle: no known relaxation of TSP is proven to have integrality gap ≤ 4/3 for general metrics, and worst-case examples for Christofides variants cluster near 4/3, so any analysis must be tight in a genuinely new way. Consider attacking the Subtour LP gap as a stepping stone.

## Key references

- N. Christofides (1976), *Worst-case analysis of a new heuristic for the travelling salesman problem*, Technical Report 388, GSIA, CMU. The classic MST + matching + shortcutting 3/2-approximation.
- A. Karlin, N. Klein, S. Oveis Gharan (2021), *A (Slightly) Improved Approximation Algorithm for Metric TSP*, STOC 2021, arXiv:2007.01409. Samples a max-entropy spanning tree and proves 3/2 − ε ≈ 10⁻³⁶ via matching-polytope fattening.
- M. Traub, J. Vygen (2024), *Approximation Algorithms for Traveling Salesman Problems*, Cambridge University Press, DOI: 10.1017/9781009445436. Comprehensive monograph covering Christofides variants, graph-TSP, LP bounds, and recent improvements.
- A. Sebő, J. Vygen (2014), *Shorter tours by nicer ears: 7/5-approximation for the graph-TSP, TSP for graphic matroids*, STOC 2014. The tight 7/5 algorithm for graph metrics using ear decompositions.
- S. Boyd, R. Sitters, S. van der Ster, L. Stougie (2014?), *TSP on cubic graphs* (verify) — special-case 4/3 results showing where the target is achievable.

## Warnings

- "4/3" appears in several distinct statements (graph-TSP 4/3, Subtour LP gap conjecture 4/3, half-integral LP conjecture) — don't conflate them with the general-metric algorithmic problem.
- KKO's ε is astronomically small; naive parameter-tuning of their analysis will not reach 4/3 — new structure is needed.
- Instances where Christofides is exactly 3/2 exist, so any improvement must use randomization or a different lower bound than MST + matching.
- Check the current best ratio before claiming novelty; the record creeps up in small increments (verify latest Traub–Vygen papers).

---
*`ALGO-000105` · unverified*

## Acceptance guidance

A polynomial-time (possibly randomized) algorithm A and a proof that for every metric instance, E[cost(A(I))] ≤ (4/3)·OPT(I). Acceptable variants in increasing difficulty:
1. A deterministic 4/3-approximation for general metrics.
2. A randomized 4/3-approximation in expectation.
3. An algorithm achieving (4/3 + ε) for arbitrary ε > 0 (a "4/3-asymptotic" result).
4. Also valuable: proving the Subtour LP integrality gap is ≤ 4/3, since a strong LP rounding could then give the algorithm.
A referee needs a complete correctness and ratio analysis; heuristic/experimental evidence does not suffice.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/a972efa2-abfd-48c7-adf6-be701599a49a?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000105.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000105)
