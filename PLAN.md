# Spark 2.5 4B Burger Plan

Base: `spark2_5` - hidden 2560, 36 layers, vocab 131072, sliding x3 + full x1, head_dim 256, 16/4 heads, gelu.

Goal: one 4B that does writing + RP + reasoning + memory/tools. Merge-only.

## 0. Compatibility rule
Merge by weight only if `model_type + hidden + layers + vocab` match.
- Group A (direct TIES/DARE): SparkMuse-4B, Spark-X2.5-Writing-EP1, spark-4b-engram, samai-4b backbone [strip ponder MoE]. All 2560/36L/131072.
- Hidden-2560 graftable via passthrough (whole blocks, no averaging): Qwen3-4B family, K2-Horizon. Keep base embed/lm_head.
- Out: Qwen2.5-3B 2048-hidden, Nemotron-H 3136-hidden 42L+Mamba, Omni multimodal. Need projs = training, skip.

## 1. Pass 1 - spark-core (Group A)
Method: TIES + DARE, base = spark-2.5-4b.
Evolve per-layer `weight 0-1 + density 0.3-0.8` with Mergenetic NSGA-II.
Fitness: writing + agent + RP + reasoning, 150-200 samples each, subsampled lm-eval.
Output: `spark-core` - CPU merge, T4 eval. Fixes seesaw via Pareto, not single score.

## 2. Pass 2 - burger (passthrough, no averaging)
36 layers 0-35. Buns fixed, evolve middle.
- 0-5 bottom bun: spark-base, embed + syntax
- 6-14 patty writing/RP: Spark-X2.5-Writing-EP1
- 15-22 patty reasoning: samai-4b / SparkMuse-4B
- 23-29 patty memory/tools: spark-4b-engram
- 30-35 top bun: spark-base, norm + head

Swap-ins (all 2560-hidden): Qwen3-4B donor, K2-Horizon donor.
Genotype: 4 cut points +-2 + donor per slot. CMA-ES/GA, 20 pop x 10 gens.
Vocab stays 131072 from base. MLP mismatch irrelevant - whole blocks copied.

## 3. Kaggle vs local
- Kaggle T4 16GB / 9h: merges on CPU, evals subsampled, 1 donor swap at a time, QLoRA heal only if needed. Internet ON.
- Local 24GB+: joint eval, full NSGA-II, longer SFT heal 200 steps.

## 4. Anti-collapse
High density 0.7-1.0 spread thin, DARE sparsity on, never 10 models at 0.5 weight. Buns fixed first run. If NaN: hidden mismatch sneaked in - check `hidden_size`.

## 5. Run order
1. `mergekit-yaml configs/spark-core-ties.yml`
2. `mergekit-yaml configs/burger-v1.yml`
3. evo cuts/donors via `evo/mergenetic.yml`
4. 200-step SFT heal only if talks-but-off
