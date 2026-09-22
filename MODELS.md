# Donor inventory - Spark 2.5 4B burger

Base: `spark2_5`, hidden 2560 / 36L / vocab 131072. Merge rule: weight-average only on exact shape match, passthrough needs hidden 2560.

## A. User-supplied 3-4B pool (verbatim, all considered)

Spark / Samai core - 2560-hidden, direct burger candidates:
- https://huggingface.co/tchbcb/samai-4b
- https://huggingface.co/hcnote/SparkMuse-4B
- https://huggingface.co/hcnote/Spark-X2.5-4B-Writing-EP1
- https://huggingface.co/darioooooo0o/spark-4b-engram
- https://huggingface.co/hotdogs/Qwen3.5-4B-MoLE
- https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Nano-4B-BF16
- https://huggingface.co/kingabzpro/nemotron-3-nano-4b-bf16-psychology-qa-lora
- https://huggingface.co/squ11z1/Mythos-nano
- https://huggingface.co/ProCreations/tutori-board-nemotron
- https://huggingface.co/Tesleum/shirdel-agent-4b

Qwen / Omni / misc 3-4B - graft or distill only, check hidden/vocab first:
- https://huggingface.co/Qwen/Qwen2.5-Omni-3B
- https://huggingface.co/AlexWortega/openjev
- https://huggingface.co/TokenRhythm/NeoHorse-1-4B
- https://huggingface.co/FlashLabs/Chroma-4B
- https://huggingface.co/NexaAI/OmniNeural-4B
- https://huggingface.co/sensenova/InteractiveOmni-4B
- https://huggingface.co/Nanbeige/Nanbeige4.2-3B
- https://huggingface.co/Qwen/Qwen-Drive-1.0-4B
- https://huggingface.co/IFM/K2-Horizon-3.7B
- https://huggingface.co/InternScience/Agents-A1-4B
- https://huggingface.co/CloudGoat/Mephisto-4B-v2.1
- https://huggingface.co/CloudGoat/Mephisto-4B-v2
- https://huggingface.co/CloudGoat/Mephisto-4B-0725
- https://huggingface.co/hotdogs/Agents-A1-4B-kimi-Preview
- https://huggingface.co/wcamon/Agents-A1-4B-Wringer-Q2.6
- https://huggingface.co/hotdogs/Agents-A1-4B-Fable-Preview
- https://huggingface.co/Lolol857/Mephisto-JOSIE-AREX-4B
- https://huggingface.co/hotdogs/Agents-A1-4B-kimi-Preview-heretic
- https://huggingface.co/DareModels/dare4b
- https://huggingface.co/hungrynovalabs/nova-pup-4b
- https://huggingface.co/ermiaazarkhalili/Agents-A1-4B-SFT-Fable5-Glint
- https://huggingface.co/hotdogs/Agents-A1-4B-cyber-lora
- https://huggingface.co/WeiboAI/VibeThinker-3B
- https://huggingface.co/microsoft/Fara1.5-4B
- https://huggingface.co/knowledgator/retrico-lm-4b
- https://huggingface.co/RefinedNeuro/VibeThinker-3B-Hermes
- https://huggingface.co/RefinedNeuro/RefinedToolCallV5-3b
- https://huggingface.co/nvidia/Cosmos3-Edge-Policy-DROID
- https://huggingface.co/ProCreations/grug-3b
- https://huggingface.co/heterodoxin/vibethinker-3b-apostate
- https://huggingface.co/Goekdeniz-Guelmez/JOSIE-2-4B-OSS
- https://huggingface.co/Aryanne/Astrea-RP-v1-4B
- https://huggingface.co/Chun121/Qwen3-4B-RPG-Roleplay-V2
- https://huggingface.co/bunnycore/Qwen-2.5-3b-RP
- https://huggingface.co/bunnycore/Qwen-2.5-3b-Evol-CoT-V3
- https://huggingface.co/bunnycore/mergekit-ties-fsxpicz
- https://huggingface.co/bunnycore/Qwen-2.5-3b-Evol-CoT
- https://huggingface.co/bunnycore/Qwen2.5-3B-MiniMix
- https://huggingface.co/bunnycore/Qwen2.5-3B-Loki
- https://huggingface.co/bunnycore/Qwen-2.5-3b-Evol-CoT-v2
- https://huggingface.co/bunnycore/Replete-Qwen-2.5-3b-CoT-RP
- https://huggingface.co/bunnycore/Qwen-2.5-3B-Remix
- https://huggingface.co/trollek/Qwen2.5-3B-Renoia

## B. Extra families - davidau / nightmedia / bunnycore / zeroxclem / jackrong

Concrete hits from catalog search (3-6B, trending):
- bunnycore Qwen2.5-3B merges: `bunnycore/Qwen2.5-3B-Loki`, `bunnycore/Qwen2.5-3B-MiniMix`, `bunnycore/Qwen-2.5-3b-Evol-CoT*`, `bunnycore/Qwen-2.5-3b-RP`, `bunnycore/mergekit-ties-fsxpicz` - qwen2 2048-hidden, merge among themselves only
- bunnycore MiniCPM5-2B line [2B, out of burger hidden]: `bunnycore/MiniCPM5-2B-Code`, `bunnycore/SuperMiniCPM5-2B` - excluded, wrong arch/size
- nightmedia Qwen3-4B: `nightmedia/Qwen3-4B-Traveler-qx86-hi-mlx`, `nightmedia/Qwen3-4B-Architect-mxfp4-mlx`, `nightmedia/Qwen3-4B-Agent-Claude-Gemini-heretic-qx86-hi-mlx` - MLX-only quants, need safetensors original for merge, else exclude
- jackrong Qwen3.5-4B reasoning: `Jackrong/Qwen3.5-4B-Claude-4.6-Opus-Reasoning-Distilled-v2` [safetensors, usable], plus GGUF/MLX variants [quant-only, excluded from weight merge]
- zeroxclem: all 8B Llama-3.1 merges [Stheno-Hercules, Hermes3-SuperNova-Purosani] - excluded, 8B + llama arch, not 2560 burger
- davidau/qwen 3-6B trending: no catalog hits under that author filter at check time - use search links below to re-check

Discovery search links (re-run before merge, catalog shifts):
- https://huggingface.co/models?num_parameters=min:3B,max:6B&sort=trending&search=davidau%2Fqwen
- https://huggingface.co/models?num_parameters=min:3B,max:6B&p=1&sort=trending&search=nightmedia%2Fqwen
- https://huggingface.co/models?num_parameters=min:3B,max:6B&sort=trending&search=nightmedia%2Fqwen
- https://huggingface.co/models?num_parameters=min:3B,max:6B&sort=trending&search=bunnycore
- https://huggingface.co/models?num_parameters=min:3B,max:6B&sort=trending&search=bunnycore%2Fqwen
- https://huggingface.co/models?num_parameters=min:3B,max:6B&p=1&sort=trending&search=bunnycore%2Fqwen
- https://huggingface.co/models?num_parameters=min:3B,max:6B&p=2&sort=trending&search=bunnycore%2Fqwen
- https://huggingface.co/models?num_parameters=min:3B,max:6B&sort=trending&search=zeroxclem
- https://huggingface.co/models?num_parameters=min:3B,max:6B&sort=trending&search=jackrong
- https://huggingface.co/models?num_parameters=min:3B,max:6B&p=1&sort=trending&search=jackrong
- https://huggingface.co/models?num_parameters=min:3B,max:6B&base_model_relation=merge&sort=trending&search=bunnycore%2Fqwen
- https://huggingface.co/models?num_parameters=min:3B,max:6B&base_model_relation=merge&p=1&sort=trending&search=bunnycore%2Fqwen

## C. Burger assignment
- Buns + core: spark2_5 2560-hidden Group A first
- Patties: 2560-hidden donors only for passthrough
- Excluded from burger weights: 2048-hidden Qwen2.5-3B, 3136-hidden Nemotron-H, Omni multimodal, GGUF/MLX-only quants, 8B Llama, 2B MiniCPM
