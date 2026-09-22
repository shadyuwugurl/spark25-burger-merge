# spark25-burger-merge

Merge-only Franken-model plan. Base `spark2_5` 2560-hidden / 36L / vocab 131072. No distill.

Sandwich: Spark buns, donor patties, evolve cuts + donors. Hidden fixed at 2560.

## Layout
- `PLAN.md` - full burger plan
- `configs/burger-v1.yml` - manual passthrough starter (MergeKit)
- `configs/spark-core-ties.yml` - Group A TIES/DARE core
- `evo/mergenetic.yml` - evolutionary search config
- `scripts/` - (add) merge + eval helpers for Kaggle / local

## Quickstart
1. Merge Group A core on CPU: `mergekit-yaml configs/spark-core-ties.yml`
2. Burger assemble on CPU: `mergekit-yaml configs/burger-v1.yml`
3. Evo cuts/donors with Mergenetic, 150-sample evals on T4
4. Keep hidden=2560, buns fixed, evolve middle first

## Tags
`llm-merging`, `mergekit`, `mergenetic`, `evolutionary-search`, `frankenmerge`, `passthrough`, `qwen`, `spark`, `4b-llm`, `kaggle`
