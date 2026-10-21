# Rana Hammad

Final-year BS Computer Science at NUST SEECS, Islamabad.

I work on how optimization algorithms are evaluated. Each project below takes an experimental
design that is standard in the metaheuristics literature and adds the one control it usually
leaves out: a random baseline over the same operators, the exact optimum, a held-out test fold, a
full budget profile. In all four, adding the control changes the conclusion.

None of these effects is new on its own, and each repository cites the work it reproduces. What
the projects add is a measurement of how large each effect is, under one statistical protocol.

---

## Research software

Shared across all four: evaluation budgets enforced in code, seeds recorded per run, Friedman
tests with Holm-corrected Wilcoxon post-hoc comparisons and Cliff's δ effect sizes, and a stated
**Limitations** section. Every table and figure regenerates from the raw results with one `make`
target. MIT licensed.

### [metaheuristics-bench](https://github.com/Just-Hammad/metaheuristics-bench) · Oct 2025 – Feb 2026

Five optimizers (DE, PSO, GA, IPOP-CMA-ES, random search) on the 24 BBOB functions at D=10 and
20,000 evaluations, plus a structural-bias test on an objective that carries no information.

- On a pure-noise objective, DE/rand/1/bin finishes biased toward the domain boundary in 10 of 10
  dimensions after Holm correction, 15% farther from the centre than uniform sampling. Random
  search, the control, is not flagged. This reproduces the structural-bias effect described by
  Kononova et al. (2015).
- PSO solves 1.88× as many targets as DE at about 600 evaluations. DE overtakes it at about 5,200
  and solves 1.76× as many by 20,000. A single end-of-run ranking hides the reversal.

*Limits:* default parameters, one dimension. Bias is measured for each algorithm together with its
bound-handling rule, and this design cannot separate the two.

### [rl-operator-selection](https://github.com/Just-Hammad/rl-operator-selection) · Mar – May 2026

Five bandit policies choosing among five DE mutation operators, compared with uniform random
selection over the same pool and with JADE. 24 BBOB functions, D=5 and D=20, 14,400 runs.

- At D=5 all five policies beat uniform random selection, four of them significantly. At D=20 none
  do, and two are significantly worse.
- Every policy converges on DE/best/1, the operator that improves the parent most often and the
  worst of the five fixed operators by final error. The harder a policy commits to its top
  operator, the worse it ranks (Spearman ρ = 0.90).
- Against a fixed `best/1` baseline, the same D=20 runs show all five policies significantly
  better. The baseline decides the headline. Karafotias et al. (2013) made this argument for
  parameter control, and Hanna et al. (2025) found the same result in program repair.

*Limits:* restricted budget (500 × D), one BBOB instance, F and CR held fixed.

### [threshold-metaheuristics](https://github.com/Just-Hammad/threshold-metaheuristics) · Jun – Jul 2026

Multilevel Otsu and Kapur thresholding solved exactly by an O(C·L²) dynamic program, with PSO, DE,
GA and random search measured against the proven optimum. 28,000 runs on 14 images, 96 tests.

- The dynamic program returns the proven optimum in every case, in 3.4–7.8 ms. At six classes the
  metaheuristics reach it in 81% (PSO), 64% (DE) and 48% (GA) of runs. Exact solutions have been in
  print since Liao et al. (2001); what is usually missing is the comparison against them.
- It is slower than scikit-image's `threshold_multiotsu` at two and three classes, and 40,968×
  faster at six.
- PSNR, SSIM and FSIM disagree with Dice about which criterion is better only where the two
  segmentations differ by less than 0.005 Dice, which is the range in which papers use them to
  separate methods.

*Limits:* separable criteria and 1-D histograms only. The metric comparison uses synthetic ground
truth.

### [moea-feature-selection](https://github.com/Just-Hammad/moea-feature-selection) · Jun – Aug 2026

NSGA-II and NSGA-III feature selection on a synthetic dataset and the colon microarray dataset (n = 62), against
matched-budget random subsets, t-test with Benjamini–Hochberg, mRMR, LASSO, Model-X knockoffs and
an oracle, under nested cross-validation.

- On the synthetic data, NSGA-II beats random subsets decisively on the inner-CV objective
  (hypervolume δ = +0.999) and not on held-out error (δ = +0.065, Holm *p* = 1.00). Reporting
  inner-CV error would have shown a large win that is not there, the selection-bias problem
  described by Ambroise & McLachlan (2002).
- The t-test filter used 8 evaluations to NSGA-II's 888 and ranked better on held-out error. Of
  ten planted features it recovered seven; NSGA-II recovered none.

*Limits:* two datasets, one budget (900 evaluations), one inner classifier.

---

## Writing

**Four Omitted Controls in Metaheuristic Optimization Experiments.** A preprint that puts the four
studies under one protocol and one argument. Link to follow.

## Current research

**Bone mineral density from plain radiographs.** Final-year project in the
[BIOMISA](http://biomisa.org/) group at NUST, supervised by Prof. Dr. Muhammad Usman Akram. A
self-supervised Vision Transformer estimating bone mineral density from standard spinal X-rays, as
a low-cost alternative to DEXA scanning, trained on paired radiograph, DEXA and blood-count data
from two Islamabad hospitals. In progress.

## Elsewhere

I also work as a full-stack and applied LLM engineer, currently at Swix AI: agent platforms,
retrieval pipelines and real-time multimodal systems. That code is private client work and is not
here.

**Tools:** Python, NumPy, SciPy, pandas, scikit-learn, pymoo, moocore, IOHexperimenter,
scikit-posthocs, scikit-image, PyTorch, MATLAB, LaTeX.

**Contact:** hammadarif564@gmail.com
