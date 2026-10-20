# Belief-Aware Guided SAC for Autonomous Driving

Code for the paper *Belief-Aware Guided SAC for Autonomous Driving Under Uncertainty* (Mehmet Haklıdır and Hakan Temeltaş), CVPR 2026 Workshop on Autonomous Driving (WAD).

BA-GSAC extends Guided Soft Actor-Critic (Haklidir and Temeltas, IEEE Access 2021) with a belief-aware guidance mechanism. An ensemble of forward models estimates epistemic uncertainty from its disagreement, and the distillation coefficient that ties the control actor to the privileged guiding actor is adapted to that uncertainty: more guidance in novel or uncertain situations, less once the agent is confident. The experiments run on Highway-Env under three levels of partial observability (observation noise, vehicle occlusion, delay) and compare BA-GSAC with fixed-guidance GSAC and SAC.

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
