# Correlation between Confidence Measurements

This repository contains the code for the paper [When Linguistic and Internal Confidence Diverge in Large Language Models](https://arxiv.org/abs/2608.28382), accepted to **Findings of the Association for Computational Linguistics: EMNLP 2026**.

Our work studies the relationship between linguistic confidence and internal confidence in large language models across classification and generation tasks, using logits-based confidence and semantic entropy as internal confidence proxies.

## Authors

**Hefan Zhang<sup>1</sup>, Bingquan Zhang<sup>1</sup>, Ming Cheng<sup>1</sup>, Saeed Hassanpour<sup>1</sup>, Weicheng Ma<sup>2</sup>, Soroush Vosoughi<sup>1</sup>**

<sup>1</sup>Dartmouth College<br>
<sup>2</sup>Oakland University

## Repository Maintainer

**This codebase was primarily developed and maintained by Hefan Zhang.**<br>
For code-related questions, please contact: [hefan.zhang.gr@dartmouth.edu](mailto:hefan.zhang.gr@dartmouth.edu)

## Classification tasks
Codes for classification tasks can be found in ```/classification_tasks```.

Use ```base_confidence_extraction.py``` to get the logits-based and linguistic confidence results for base models, for example:

```bash
python base_confidence_extraction.py \
  --model_id Qwen/Qwen2.5-14B \        # Hugging Face model name
  --prompt_file prompts_base_new_56.json \      # Prompt file under /new_models_data/{task}/, new_56, 45 for Prompt 1, 2
  --task CoLA \                                 # Task name (folder name)
  --token hf_xxx_your_token \          # (Optional) Hugging Face access token
  --align_logits_hint                           # (Optional) Append a note asking model to align confidence with logits
```
Use ```instruct_confidence_extraction.py``` to get the logits-based and linguistic confidence results for instruction-tuned models, for example:
```bash
python instruct_confidence_extraction.py \
  --model_id Qwen/Qwen2.5-14B-Instruct \
  --prompt_file prompts_instruct_2.json \
  --task CoLA \
  --token hf_xxx_your_token \
  --align_logits_hint
```
Use ```base_without_conf.py``` to get only logits-based confidence results for base models, whose prompt doesn't have the requirement for linguistic confidence. For example:
```bash
python base_without_conf.py \
  --model_id meta-llama/Llama-2-13b-hf \        
  --prompt_file prompts_base_withoutConfidence.json \  
  --task CoLA \                            
  --token hf_xxx_your_token           
```
Use ```instruct_without_conf.py``` to get only logits-based confidence results for instruction-tuned models, whose prompt doesn't have the requirement for linguistic confidence. For example:
```bash
python instruct_without_conf.py \
  --model_id Qwen/Qwen2.5-14B-Instruct \   
  --prompt_file prompts_instruct_withoutConfidence.json \ 
  --task CoLA \                          
  --token hf_xxx_your_token                  
```
Run ```results_analysis.py``` to get the results.

## Generation tasks
Codes for generation tasks can be found in ```/generation_tasks```.

Use ```parse_coqa.py``` and ```parse_triviaqa.py``` to preprocess the datasets.

Use ```model_pipeline``` to get all results.

After that, use ```result_analysis.ipynb``` to analyze the correlation of semantic uncertainty and linguistic confidence.

## Citation

If you use this code or find our work helpful in your research, please cite our paper:

```bibtex
@misc{zhang2026linguisticinternalconfidencediverge,
  title         = {When Linguistic and Internal Confidence Diverge in Large Language Models},
  author        = {Hefan Zhang and Bingquan Zhang and Ming Cheng and Saeed Hassanpour and Weicheng Ma and Soroush Vosoughi},
  year          = {2026},
  eprint        = {2608.28382},
  archivePrefix = {arXiv},
  primaryClass  = {cs.CL},
  doi           = {10.48550/arXiv.2608.28382},
  url           = {https://arxiv.org/abs/2608.28382},
  note          = {Accepted to Findings of the Association for Computational Linguistics: EMNLP 2026}
}
```
