# Erdős 505 dimension-one repair context

This is a non-authoritative producer aid for the exact target
`formal:erdos-505-test-dim-one`. It does not contain a completed proof term and
does not change the theorem, verifier, axiom policy, or Vela authority state.

## Why this repair exists

The first frozen Canopus attempt returned `null` before verification or
landing. It correctly declined to invent a proof, but its trace shows that the
worker spent the attempt rediscovering the packet layout and lacked the small
set of exact Mathlib names needed to express the elementary argument.

- Run: `run_5407a1cb-ac23-4927-b3ac-ad790df32544`
- Mission root: `sha256:9f986c8d1811f1387071ccfc8ae903aa201904ee1a3c220ac07873b7becb9328`
- Engine-result root: `sha256:6a0e7fa1776657b5f8254f697b8cbc36adef3e1391ac43dceb51ff5f7d241b0c`
- Worker-output root: `sha256:bc0e18d5e7074e2fc7d8be2d5ccec029d9fc387f862c8f292b7c622d6aa093d9`
- Failure root: `sha256:56a73a30a44cf7ffd2ba97c3a0127e4ff5a893d3a9e52a997d0d0d7576e63e20`
- Activity tip: `sha256:9755b56ce98b42d269939b4a9764e6cad7fe397c3544c8351184782d1d4b0136`
- Observed result: `engine_non_success`; verifier and landing were not run.

## Frozen environment

- Lean: `leanprover/lean4:v4.27.0`
- Mathlib: `a3a10db0e9d66acbebf76c5e6a135066525ac900`
- Imports available to the verifier:
  - `Mathlib.Analysis.InnerProductSpace.PiL2`
  - `Mathlib.Topology.MetricSpace.Bounded`

The following names were checked in that exact network-denied image:

- `IsometryEquiv.mk'`
- `EuclideanSpace.single`
- `EuclideanSpace.dist_single_same`
- `IsometryEquiv.diam_image`
- `Bornology.IsBounded.subset_Icc_sInf_sSup`
- `Real.diam_eq`
- `Real.diam_Icc`
- `Real.diam_Ioc`

Standard `fin_cases`, `simp`, and `linarith` tactics are available under the
two frozen imports.

## Reviewed mathematical route

1. Build an isometric equivalence between `ℝ` and
   `EuclideanSpace ℝ (Fin 1)`. The forward map is
   `EuclideanSpace.single 0`; the inverse evaluates coordinate `0`.
2. Map `S` through the inverse equivalence to a bounded real set `T`. Use the
   isometry to transport its diameter and the positive-diameter hypothesis.
3. Put `a = sInf T`, `b = sSup T`, and `m = (a + b) / 2`.
4. Cover `T` by the two real intervals `Icc a m` and `Ioc m b`. The bounded-set
   interval lemma supplies membership in `Icc a b`; split on `x ≤ m`.
5. `Real.diam_eq` identifies `diam T` with `b - a`. `Real.diam_Icc` and
   `Real.diam_Ioc` identify each half's diameter, and positivity makes both
   strictly smaller than `diam T`.
6. Map the two intervals forward through the isometric equivalence. Transport
   both the cover and the strict diameter inequalities.

The producer must still write the exact Lean term. The only admissible artifact
is the raw UTF-8 term beginning with `by`; the frozen capsule independently
supplies the theorem signature, elaborates it, and rejects `sorryAx` or any
unregistered axiom.
