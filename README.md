# Belief-Aware Guided SAC for Autonomous Driving

Code for the paper

> Haklidir, M. (2026). When Does Adaptive Guidance Help? Belief-Aware Privileged Distillation for Autonomous Driving Under Partial Observability. arXiv:2605.26155. Accepted at the CVPR 2026 Workshop on Autonomous Driving (WAD). https://doi.org/10.48550/arXiv.2605.26155

Guided Soft Actor-Critic (GSAC) distills a privileged full-state teacher into a partial-observation student with a fixed distillation coefficient λ. Belief-Aware GSAC (BA-GSAC) modulates λ with the disagreement of an ensemble of forward models and serves here as a testbed for one question: when does adaptive guidance actually help? Five strategies (fixed λ = 0.01 and 0.1, adaptive, linear decay, vanilla SAC) are compared across three POMDP difficulty levels on Highway-Env. Under mild and moderate partial observability the adaptive coefficient looks useful in single-seed runs; under severe occlusion (3 seeds for every method) it collapses to λ_min within about 3K steps. The paper traces this to observability blindness: an ensemble that predicts partial observations reaches low disagreement even under heavy occlusion, because it models what is visible and cannot detect what is missing. A simple linear decay schedule gives the best severe-POMDP results, so the scheduling effect rather than the ensemble drives the stability benefit.

## Contents

```
notebooks/ba_gsac_highway.ipynb      environment wrapper, GSAC and BA-GSAC agents, main experiments,
                                     figures and Table I, warmup ablation
notebooks/reviewer_baselines.ipynb   baselines added in review: fixed λ = 0.01 and 0.5, linear decay,
                                     SAC with history K = 3, multi-seed mild and moderate runs
results/exp1_fixed_lam001.json       cumulative result checkpoints of the reviewer notebook, saved after
results/exp2_fixed_lam05.json        each experiment block
results/exp3_decay.json
results/exp4_sac_history.json
```

## Running

Both notebooks are written for Google Colab: open one, Runtime > Run all. The main notebook takes 20 to 30 minutes on a GPU with the default 15,000 steps per experiment; the reviewer notebook takes 15 to 18 hours on a T4 and saves a JSON checkpoint after each experiment block. Packages are listed in `requirements.txt`.

The base method is also available as a standalone implementation at https://github.com/haklidir/guided-sac.

## Citation

See `CITATION.cff`.

## License

MIT, see `LICENSE`.
