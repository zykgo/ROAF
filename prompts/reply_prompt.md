# Reply Opposition-Scoring Prompt

### System Message

```text
You are an expert in analyzing replies in online debates. Return valid JSON only, without Markdown or additional explanations.
```

### User Message

```json
{
  "Task": "Determine whether each reply opposes, refutes, or challenges its parent post.",
  "Important restrictions": [
    "Use only the supplied topic, parent post, and reply text.",
    "Do not use stance labels, voting information, or dataset answers.",
    "Do not infer the author's true stance on the overall issue.",
    "Assess the local reply relation: whether the reply refutes the parent post.",
    "Do not assign an intuitive overall score. First rate five dimensions separately from 0 to 1; the program will calculate the weighted total."
  ],
  "Scoring requirements": [
    "Output a continuous decimal between 0 and 1 for each dimension; two decimal places are allowed, such as 0.13, 0.47, or 0.82.",
    "Do not restrict scores to fixed categories.",
    "Higher values indicate a more evident feature.",
    "Approximately 0.00 means almost absent; 0.25 means weak; 0.50 means moderate, uncertain, or ambiguous; 0.75 means evident; 1.00 means very explicit."
  ],
  "Five dimensions": {
    "direct_disagreement": {
      "Meaning": "Direct disagreement: whether the reply explicitly rejects the parent post's claim.",
      "High-score examples": [
        "You are wrong",
        "I disagree",
        "This is not true",
        "This claim is incorrect"
      ],
      "Low-score cases": [
        "Supplementary explanation only",
        "A question only",
        "No explicit rejection of the parent post"
      ]
    },
    "logic_or_evidence_challenge": {
      "Meaning": "Logical or evidential challenge: whether the reply questions the parent post's evidence, logic, assumptions, causal relations, or reasoning.",
      "High-score examples": [
        "You have no evidence",
        "This conclusion does not follow",
        "Your assumption does not hold",
        "This source does not support your claim"
      ],
      "Low-score cases": [
        "No discussion of evidence or logic",
        "Emotion only",
        "General remarks only"
      ]
    },
    "counter_claim": {
      "Meaning": "Counter-claim strength: whether the reply offers a conflicting alternative view or opposing claim.",
      "High-score examples": [
        "The parent says A causes B; the reply says A does not cause B",
        "The parent supports a view; the reply offers an opposing explanation",
        "But, however, actually, or on the contrary introduces a conflicting claim"
      ],
      "Low-score cases": [
        "No different view is proposed",
        "The reply merely continues the topic",
        "Neutral supplementary information only"
      ]
    },
    "targeted_response": {
      "Meaning": "Targeted response: whether the reply specifically addresses the parent post rather than making unrelated general remarks.",
      "High-score examples": [
        "Directly responds to a parent-post argument",
        "Refers to what you said or your view",
        "Responds to the parent's evidence, examples, or conclusions"
      ],
      "Low-score cases": [
        "An independent monologue",
        "Weak connection to the parent post",
        "General stance expression only"
      ]
    },
    "agreement_or_neutral": {
      "Meaning": "Agreement or neutrality: whether the reply resembles agreement, support, supplementation, neutral questioning, clarification, or unrelated content. Higher values indicate less refutation.",
      "High-score examples": [
        "I agree",
        "Yes, and",
        "You are right",
        "Neutral follow-up questions or supplementary explanation"
      ],
      "Low-score cases": [
        "Clear refutation",
        "Clear challenge",
        "Clearly opposing views"
      ]
    }
  },
  "Important decision rules": [
    "Do not assign high opposition scores solely because of intense language, sarcasm, or personal attacks. Opposition requires a challenge to the parent post's claims, evidence, or logic.",
    "Do not automatically assign high scores because words such as but, you, or not appear; determine whether they actually refute the parent post.",
    "Even without explicit expressions such as you are wrong, a clear challenge to the parent's logic may receive a high score on the relevant dimension.",
    "If the reply contains both agreement and refutation, reflect them separately in agreement_or_neutral and the refutation dimensions.",
    "If the text is too short, unrelated, or incomprehensible, assign low scores to refutation dimensions; agreement_or_neutral may be moderate or high as appropriate."
  ],
  "items": "{{items_json}}",
  "output_schema": {
    "scores": [
      {
        "id": "Same id as the input",
        "dimension_scores": {
          "direct_disagreement": 0.0,
          "logic_or_evidence_challenge": 0.0,
          "counter_claim": 0.0,
          "targeted_response": 0.0,
          "agreement_or_neutral": 0.0
        },
        "reason": "Brief explanation in Chinese"
      }
    ]
  }
}
```
