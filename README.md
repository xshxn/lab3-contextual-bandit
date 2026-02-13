# Lab 3: Contextual Bandits for News Recommendation

This project implements a Contextual Bandit system to recommend news articles to users based on their demographic and behavioral data. The system learns to map user contexts to preferred news categories (Entertainment, Education, Tech, Crime) to maximize user engagement (reward).

## ?? Approach and Design Decisions

### 1. User Context Classification
Instead of treating all users the same, we classify users into distinct "contexts" or clusters provided in the dataset (User1, User2, User3).
- **Model used**: XGBoost Classifier (XGBClassifier).
- **Features**: User demographics (age, income, location) and behavior (clicks, purchase amount, etc.).
- **Outcome**: The classifier predicts the user type, which determines the set of arms (news categories) available for that specific context.

### 2. Contextual Bandit Algorithms
We implemented and compared three standard multi-armed bandit algorithms to handle the exploration-exploitation trade-off within each context:
- **Epsilon-Greedy**: Explores random arms with probability $\epsilon$ and exploits the best known arm with probability -\epsilon$.
- **Upper Confidence Bound (UCB)**: Selects arms based on an optimistic estimate of their value (mean reward + confidence interval), automatically reducing exploration as confidence grows.
- **SoftMax**: Selects arms probabilistically based on their estimated values using a Boltzmann distribution.

### 3. Arms and Rewards
- **Arms**: There are 12 total arms, representing combinations of 3 user contexts $\times$ 4 news categories.
- **Reward**: Obtained from a custom sampler module initialized with student roll number (126).

## ?? Key Results and Observations

### Algorithm Performance
- **UCB (C=1.0)** performed best overall, showing stable convergence and high final average rewards. It balanced exploration and exploitation effectively for this specific reward distribution.
- **Epsilon-Greedy ($\epsilon$=0.1)** was a strong contender, offering robust performance with a simple mechanism. Lower values ($\epsilon$=0.01) were too slow to learn, while higher values exploited too little.
- **SoftMax ($\tau$=1.0)** provided a middle ground but required careful tuning.

### Recommendations
The final system generates recommendations for the test dataset (	est_users.csv).
- **Output**: 	test_user_recommendations.csv containing predicted user context, recommended category, arm index, and expected reward for 2000 test users.

