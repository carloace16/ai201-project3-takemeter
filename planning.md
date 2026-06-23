# TakeMeter Planning Document

## 1. Community

I chose the `r/nba` subreddit. The discourse there is incredibly varied, ranging from highly detailed statistical breakdowns of games to pure emotional rants and bold, controversial claims. It’s perfect for a classification task because the difference between a "good take" and a "bad take" actually has a clear, definable structure here.

## 2. Labels

- **analysis**: A post that makes a structured argument backed by specific statistics, film breakdowns, or tactical observations. The focus is on proving a point with verifiable evidence.
  - _Example 1:_ "The Timberwolves' defensive rating drops from 108.2 to 115.4 when Gobert sits, proving he's the real anchor of the scheme, not Edwards."
  - _Example 2:_ "Boston consistently ran a high pick-and-roll in the 4th to force Luka to switch onto Tatum, exploiting his lateral movement."
- **hot_take**: A bold, confident, and controversial opinion stated without deep verifiable evidence. The claim might be true, but the user is just asserting it to spark a debate rather than proving it.
  - _Example 1:_ "SGA is a regular-season merchant who relies entirely on foul baiting and will never lead a team to the Finals."
  - _Example 2:_ "LeBron is actively ruining the Lakers' future by holding the front office hostage. Trade him now."
- **reaction**: An immediate emotional response, meme, or hype comment to a specific highlight or game result. Zero argument is being made.
  - _Example 1:_ "ANTHONY EDWARDS JUST ENDED JOHN COLLINS' WHOLE CAREER LMAOOOO."
  - _Example 2:_ "I'm literally sick to my stomach, I can't believe we just blew a 20-point lead again."

## 3. Hard Edge Cases

- **The Ambiguous Post:** "LeBron is wildly overrated in the clutch—his clutch free throw percentage is only 73% this year."
- **Decision Rule:** This sits on the boundary between `hot_take` and `analysis`. If a single stat is just cherry-picked as a weapon to push a hyper-emotional or inflammatory narrative, I will label it `hot_take`. If the post actually breaks down why the stat is happening (like bringing up 4th-quarter usage rates or fatigue), I will label it `analysis`.

## 4. Data Collection Plan

I will manually collect at least 200 public comments and posts from `r/nba` using game threads and post-game discussions. I'll paste the text into a CSV file with a `text` column and a `label` column. If I notice one label (like `reaction`) is taking up more than 70% of my dataset, I will intentionally search for deep-dive threads to balance out the `analysis` and `hot_take` examples.

## 5. Evaluation Metrics

Overall accuracy isn't enough because the dataset might be slightly imbalanced. I will also use **per-class F1-score** and a **confusion matrix**. The confusion matrix is critical because it will tell me exactly which labels the model is mixing up (e.g., if it constantly confuses `analysis` with `hot_take`).

## 6. Definition of Success

For this classifier to be genuinely useful as a community tool, I want to see an overall accuracy of at least 75%, and a per-class F1-score of over 0.70 for all three labels. If the fine-tuned model consistently beats a zero-shot LLM baseline, I'll consider that a major success.

## 7. AI Tool Plan

- **Label stress-testing:** Before I label all 200 posts, I will feed my definitions to an LLM and ask it to generate 5 edge-case posts to see if my rules hold up.
- **Annotation assistance:** I will manually label all the data myself to ensure high quality and stay close to the data, rather than relying on an LLM to pre-label.
- **Failure analysis:** Once I have my wrong predictions from the model, I will paste them into an LLM and ask it to help me identify any hidden patterns in why the model got them wrong (e.g., struggling with sarcasm).
