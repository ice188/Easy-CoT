# Easy-CoT: Automated and Diverse Chain-of-Thought Reasoning on Small Language Models

## Instruction
To run experiment on an unseen complex reasoning dataset (one that has question-answer data), follow these steps:

1. Produce base dataset using [Fine-tune-CoT](https://github.com/itsnamgyu/reasoning-teacher).
2. Run run_auto_cot() to produce the Easy-CoT dataset.
3. Run finetune_model() to tune gpt2-small on this generated dataset.
4. Use test_all() to evaluate the two baselines + Easy-CoT.

## Directories
### code/
The easy_cot.ipynb notebook has the following APIs are avaliable for use: 
- run_auto_cot(dataset, task, save_dir, *hyperparams): apply auto-cot on base dataset to generate easy_cot dataset corresponding to the task and dump in save_dir. Note that since the base dataset is the output of teacher model from Fine-tune-CoT.

- finetune_model(task, model_dir): fine-tune gpt2-small on Easy-CoT data of provided task, save the fine-tuned model in model_dir.
  
- test_all(task, model_dir): run two baselines (auto-cot and fine-tune-cot) and easy-cot experiment on the test set for task, output average accuracy over three runs for each. The fine-tuned-model should be in model_dir.

### easy_cot/
Contains our Easy-CoT dataset for five tasks. See details in paper. Each subdirectory of easy_cot has a name corresponding to the base dataset that it was generated from, and contains two files: data.json (containing output of fine-tune-cot applied on base dataset) and demos.json (containing output of auto-cot applied on data.json).

### finetuned_model/
All fine-tuned models from our experiment can be downloaded [here](https://drive.google.com/drive/folders/1FnIW-2SayX6KT6YGN6IL_8gQyiLiFY23?usp=drive_link). There are five models in total, one for each base dataset.

### datasets/
Contains the five base datasets on complex reasoning tasks used to generate our easy_cot dataset.

- fine_tune_cot/: completed data generated by teacher model in fine-tune-cot, courtesy of [Ho et al.](https://github.com/itsnamgyu/reasoning-teacher)

- zero_shot_cot/: raw data for complex reasoning task benchmarks, courtesy of [Kojima et al.](https://github.com/kojima-takeshi188/zero_shot_cot/tree/main/dataset). Not directly used in our experiment but was used to produce the fine_tune_cot/ dataset

