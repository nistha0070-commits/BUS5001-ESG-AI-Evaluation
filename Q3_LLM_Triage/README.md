# BUS5001 Q3 – ESG Message Triage Using a Large Language Model

## Project Overview

This project investigates the use of a Large Language Model (LLM) to classify employee Environmental, Social and Governance (ESG) messages for operational triage. It compares an instruction-following language model with a simple rule-based classifier and evaluates classification accuracy, JSON output quality and operational safety.

## Technologies Used

- Google Colab and Python
- Hugging Face Transformers
- Qwen2.5-0.5B-Instruct
- Pandas
- JSON validation
- Microsoft Azure (proposed architecture only)

## Methodology

Three simulated ESG employee messages were developed to represent a water leak near electrical equipment, recycling contamination and an accessibility barrier.

A keyword-based classifier was implemented as a baseline. The Hugging Face model was then tested using a structured prompt requesting issue category, urgency, sentiment, follow-up requirements, recommended team, escalation status and reasoning.

The outputs were compared against manually defined reference labels. Additional checks evaluated JSON validity, schema compliance and consistency with a predefined safety-escalation policy.

## Experimental Results

| Metric | Rule-Based | Hugging Face LLM |
|---|---|---|
| Issue category accuracy | 100% | 66.67% |
| Urgency accuracy | 100% | 66.67% |
| Follow-up accuracy | 100% | 0% |

All three LLM responses were syntactically valid JSON, but none passed the complete schema validation. None passed the defined safety-consistency rule.

The post-processing layer flagged all three messages for human review and blocked automatic routing.

## Key Findings

The LLM correctly identified two of the three incident categories but misclassified recycling contamination as water waste. It also failed to recommend follow-up for all three cases.

The experiment demonstrates that valid structured output does not necessarily imply accurate or safe operational decisions.

The rule-based classifier performed better on this small dataset, although the rules were tailored to the scenarios. The three-message sample is insufficient for generalising performance to real-world use.

## Proposed Azure Architecture

A potential production system could use Azure Logic Apps and Azure Functions for message collection and validation, Azure OpenAI for classification, and Azure Monitor and controlled storage for operational monitoring and auditing.

Messages failing validation or involving elevated safety risks would be directed to appropriate human reviewers before operational routing.

This Azure architecture is conceptual and was not deployed during the experiment.

## Responsible AI Considerations

The proposed solution includes data minimisation, restricted access, human oversight, deterministic safety checks and auditability. Real employee messages should not be submitted to external models without appropriate organisational authorisation and privacy controls.

## Limitations

The experiment used only three simulated messages and a relatively small language model. Results may vary with larger models, alternative prompts, different messages and operating conditions. The baseline was designed around known test scenarios, limiting the fairness of the comparison.

## Reproducibility

The Jupyter Notebook contains the experimental code, prompts, model configuration, baseline classifier and evaluation. CSV files preserve the classification outputs and validation results.

The model was tested locally within the Google Colab runtime using Hugging Face Transformers. No production Azure deployment or automated ticket submission was performed.
