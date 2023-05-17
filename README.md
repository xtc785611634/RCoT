# RCOT: Detecting and Rectifying Factual Inconsistency by Reversing Chain-Of-Thought

## Method
“RCoT, a novel method for detecting and rectifying condition hallucination, overlooking and question misinterpretation in CoT“

Large language Models (LLMs) have achieved promising performance on arithmetic reasoning tasks by incorporating step-by-step chain-of-thought (CoT) prompting. However, LLMs face challenges in maintaining factual consistency during reasoning, exhibiting tendencies to overlook, misinterpret and hallucinate over given conditions.Existing methods on improving factual consistency using interative refinement are largely limited to coarse-grained feedbacks, e.g., correct or not, which fail to accurately locate errors in complex arithmetic reasoning tasks. we propose RCOT, a novel method to improve factual consistency in generated solutions. RCoT instructs a LLM to reconstruct the input problem based on its self-generated step-by-step solution from chain-of-thought prompting. The reconstructed problem is then compared with the original problem by fine-grained condition decomposition, which reveals potential factual inconsistencies in the original solution. RCoT then construct a fine-grained feedback based on the identified erros from the comparison and provide it to the LLM to perform self-revison on the intial solution. Experimental results demonstrate significant improvements over standard CoT by 5.0\%, 4.1\%, 3.1\%, 2.8\%, 1.8\%, and 1.1\% on Date, AQuA, GSM8K, SVAMP, AddSub, and SingleEq, respectively.



The illustration of active-prompt is shown in the figure below.


## Requirements
`pip install openai`

Put your `OpenAI API KEY` to the `API_KEY` variable of `utils.py`.


## Quick Start
For a quick start, you can directly run inference with RCoT(proposed in the paper).

```shell
python inference.py --dataset="gsm8k" --model="gpt-3.5-turbo" --method="zero_shot_cot" --random_seed=99 --multipath=1 --temperature=0 --api_time_interval=0.5 --test_size=256 --shot=0 --flag="gpt"
```

## Important arguments
   * `--dataset`: The name of a dataset. `choices = [gsm8k, svamp, aqua, asdiv, singleeq, addsub, Date]`.
   * `--model`: GPT-3 model. `choices = [gpt-3.5-turbo]`.
   * `--method`: zero-shot-cot or few-shot-cot.
   * `--test_size`: number of test questions.
   * `--api_time_interval`: the time interval when requesting GPT-3 API. Suggested interval is larger than 1 second.

