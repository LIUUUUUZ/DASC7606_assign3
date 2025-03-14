# HKU-DASC7606-A3
HKU DASC-7606 Assignment 3 NLP: Majority Voting in Large Language Models

This codebase is only for HKU DASC 7606 (2024-2025) course. Please don't upload your answers or this codebase to any public platforms. All rights reserved.

## 1 Introduction

### 1.1 Large Language Models and Enhanced Reliability
Large language models, such as GPT-3 and its successors, have revolutionized natural language processing by enabling sophisticated text generation and understanding. A prominent technique used to enhance the reliability of these models is majority voting. This method aggregates predictions to improve accuracy and robustness in decision-making, capitalizing on the extensive pre-training of these models to produce consistent outputs without additional fine-tuning.

### 1.2 Multi-choice Question Answering
Multiple-choice question answering is crucial for evaluating the reasoning capabilities of large language models. It involves providing a question with several possible answers, only one of which is correct. This task demonstrates a model's ability to comprehend and apply its pre-trained knowledge to new scenarios, particularly through datasets like the AI2 Reasoning Challenge (ARC), which tests a broad range of reasoning skills.

### 1.3 What Will You Learn from This Assignment?
In this assignment, you will:

- Understand the architecture of **large language models** by deploying a 1 billion parameter model.
- Explore **majority voting** techniques to enhance model predictions.
- Implement the generation of rationales (chain-of-thought) prior to deriving final answers.

## 2 Setup

### 2.1 Working Remotely on HKU GPU Farm (Recommended)
Follow the provided quickstart guide to set up your environment on the HKU GPU Farm for efficient experiments.

### 2.2 Working Locally
Ensure you have the necessary GPU resources and software (e.g., CUDA, cuDNN) installed for optimal performance.

### 2.3 Creating Python Environments

**Installing Python**: The code has been verified with Python version 3.10.9.

**Virtual Environment**: Use Anaconda for managing dependencies:

```bash
conda create -n nlp_env python=3.10.9
conda activate nlp_env
```

Install the following packages:

```bash
pip install torch==1.13
pip install transformers==4.44.2
pip install huggingface_hub==0.26.2
```

## 3 Working on the Assignment

### 3.1 Basis of Majority Voting

Majority voting enhances model reliability by aggregating predictions from multiple runs. This technique ensures more robust outcomes, leveraging the consensus from repeated model executions.

**Example:**

- Run 1 Prediction: 12
- Run 2 Prediction: 12
- Run 3 Prediction: 10

**Final Answer (via Majority Voting):** 12

### 3.2 Task Description

The task involves generating a rationale (chain-of-thought) before deriving the final answer for multiple-choice questions.

**Example:**

Question: George wants to warm his hands quickly by rubbing them. Which skin surface will produce the most heat?

Choices: (A) dry palms (B) wet palms (C) palms covered with oil (D) palms covered with lotion

Rationale: Rubbing dry palms generates the most friction and thus the most heat.

Answer: A

### 3.3 Get Code

The codebase structure:

```
project/
│
├── data/
│   ├── test.jsonl
│   ├── validation.jsonl
│   └── train.jsonl
│
├── modeling_llama.py
├── tokenization_llama_fast.py
├── tokenization_llama.py
├── configuration_llama.py
├── mcqa.py
│
└── README.md
```

Run experiments using:

```bash
python mcqa.py --input_file "data/test.jsonl" --output_file "predictions/test.jsonl" --model_path "models/Llama-3.2-1B-Instruct" --num_forward_passes 8
```

Explanation of parameters:

- **input_file**: The path to the input JSONL file containing the test questions.
- **output_file**: Where the predictions will be saved in JSONL format.
- **model_path**: Specifies the path to the model.
- **num_forward_passes**: Sets the number of times to run forward passes for majority voting.

### 3.4 Assignment Tasks

**Task 1: Model Implementation**

Complete all sections marked with "`Write Your Code Here`" in `modeling_llama.py` to ensure the model processes inputs correctly and efficiently.

**Task 2: Implement Code for Majority Voting**

Develop the logic in `mcqa.py`, completing sections marked with "`Write Your Code Here`" to perform majority voting. This involves running multiple forward passes and aggregating results to determine the most likely answer.

**Task 3: Predict Outputs for the Test Set**

Use the completed codebase to generate predictions for the ARC test set. Ensure the model is correctly configured and outputs are saved appropriately.

**Task 4: Write a Report**

Prepare a comprehensive report, focusing on:

- Hyper-parameter Tuning and Formats of Prompts: Explore the impact of parameters like temperature and num_forward_passes on the validation set, reporting its accuracy.
- **Test Set Accuracy**: Clearly report the accuracy on the test set in your final report.

### 3.5 Files to Submit

If your student ID is 30300xxxxx, then the file should be organized as follows:

```
30300xxxxx.zip
|-report.pdf
|-src
|   |-README.md
|   |-your code
|-model_predictions.jsonl
```

1. **Final Report**: `report.pdf` (up to 2 pages)

2. **Codes**: Include all your code files within the `src` directory along with a `README.md` describing modifications.

3. **Model Predictions**: `model_predictions.jsonl`—this should be the `output_file` generated by running the `mcqa.py` script on the test set.

### 3.6 When to Submit?

The deadline is Dec. 8 (23:59)

Late submission policy:

- 10% penalty within 1 day late.
- 20% penalty within 2 days late.
- 50% penalty within 7 days late.
- 100% penalty after 7 days late.

## 4 Marking Scheme

Submissions will be evaluated based on two main criteria: model performance on the ARC-Challenge-test dataset (80%) and the quality of the report (20%).

### 1. **Performance (80%)**

Marks will be awarded based on the accuracy achieved on the test set:
- **50% and above**: Full marks
- **48-50%**: 90% of the marks
- **46-48%**: 80% of the marks
- **42-46%**: 70% of the marks
- **38-42%**: 60% of the marks
- **30-38%**: 50% of the marks
- **Below 30%**: No marks

### 2. **Final Report (20%)**

Marks for the report will primarily be based on the depth and quality of the experiments and analysis:
- **Rich experiments and detailed analysis**: 90-100% of the marks
- **Basic analysis**: 70-90% of the marks
- **Insufficient or minimal analysis**: Less than 70% of the marks



### File modifications:      

    In file mcqa.py:        

    Line 183: majority_pred = vote_counts.most_common(1)["Write Your Code Here"]["Write Your Code Here"] -> majority_pred = vote_counts.most_common(1)[0][0]        

    In file modeling_llama.py:

    Line 287, 288: 
    self.up_proj = nn.Linear("Write Your Code Here", self.intermediate_size, bias=config.mlp_bias)
    self.down_proj = nn.Linear(self.intermediate_size, "Write Your Code Here", bias=config.mlp_bias)  
    -> 
    self.up_proj = nn.Linear(self.hidden_size, self.intermediate_size, bias=config.mlp_bias)     
    self.down_proj = nn.Linear(self.intermediate_size, self.hidden_size, bias=config.mlp_bias)     

    Line 356, 357, 358:
    self.q_proj = nn.Linear("Write Your Code Here", self.num_heads * self.head_dim, bias=config.attention_bias)
    self.k_proj = nn.Linear("Write Your Code Here", self.num_key_value_heads * self.head_dim, bias=config.attention_bias)
    self.v_proj = nn.Linear("Write Your Code Here", self.num_key_value_heads * self.head_dim, bias=config.attention_bias)
    ->
    self.q_proj = nn.Linear(self.hidden_size, self.num_heads * self.head_dim, bias=config.attention_bias)
    self.k_proj = nn.Linear(self.hidden_size, self.num_key_value_heads * self.head_dim, bias=config.attention_bias)
    self.v_proj = nn.Linear(self.hidden_size, self.num_key_value_heads * self.head_dim, bias=config.attention_bias)    

    Line 424: attn_weights = torch.matmul("Write Your Code Here", "Write Your Code Here") / math.sqrt(self.head_dim) -> attn_weights = torch.matmul(query_states, key_states) / math.sqrt(self.head_dim)

    Line 745: hidden_states = "Write Your Code Here" + hidden_states -> hidden_states = residual + hidden_states

 
        
        
    
