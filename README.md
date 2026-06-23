# TakeMeter: r/nba Discourse Classifier

TakeMeter is a fine-tuned text classifier designed to evaluate the quality of discourse in the r/nba subreddit. It distinguishes between structured analysis, inflammatory hot takes, and emotional reactions.

## 1. Community & Labels

**Community:** r/nba
**Labels:**

- **analysis:** Structured arguments backed by data, film, or tactical observation.
- **hot_take:** Bold, opinionated claims stated without supporting evidence.
- **reaction:** Immediate emotional responses, memes, or hype with no argumentative structure.

## 2. Evaluation Results

| Model                   | Overall Accuracy | Analysis F1 | Hot_Take F1 | Reaction F1 |
| :---------------------- | :--------------- | :---------- | :---------- | :---------- |
| Zero-Shot (Baseline)    | 1.00             | 1.00        | 1.00        | 1.00        |
| Fine-Tuned (DistilBERT) | 0.77             | 0.90        | 0.72        | 0.67        |

### Confusion Matrix (Fine-Tuned Model)

| True \ Pred  | Analysis | Hot_Take | Reaction |
| :----------- | :------: | :------: | :------: |
| **Analysis** |    9     |    1     |    0     |
| **Hot_Take** |    0     |    9     |    1     |
| **Reaction** |    0     |    5     |    5     |

## 3. Failure Analysis

The model exhibits a systematic bias where it misclassifies short, emotional `reaction` posts as `hot_takes`.

- **Example:** "Wow, absolute silence in the arena. You can hear a pin drop."
- **Analysis:** My intent for `hot_take` was unsupported argumentation, but the model learned that "any emotional opinion" = `hot_take`. It over-indexed on tone rather than the presence of an argument.

## 4. Sample Classifications

| Text                              | Label    | Prediction | Confidence |
| :-------------------------------- | :------- | :--------- | :--------- |
| "Tatum shot 5-of-6..."            | analysis | analysis   | 0.94       |
| "He is flexing down 20 points..." | reaction | hot_take   | 0.37       |
| "LeBron is actively ruining..."   | hot_take | analysis   | 0.36       |

## 5. AI Usage

1. **Label stress-testing:** Used Claude to generate ambiguous r/nba posts to refine my decision rules.
2. **Failure analysis:** Used an LLM to identify the pattern that the model was conflating "emotional tone" with "hot takes."
