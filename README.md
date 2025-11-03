Hangman Solver using Hidden Markov Models and Reinforcement Learning Overview This project implements an AI-powered Hangman solver that combines: A Hidden Markov Model (HMM) for probabilistic letter prediction, and A Reinforcement Learning (RL) agent (Q-learning / DQN) for optimal guessing strategies. The system learns to play Hangman by predicting the most likely next letters and balancing exploration vs. exploitation through experience-based rewards.

Features Custom Gymnasium-compatible Hangman environment ProbabilisticOracle (HMM) for character-level sequence modeling Reinforcement Learning agent trained via Q-learning / DQN Curriculum learning — short → medium → long words Evaluation system with final hackathon scoring metric Detailed Analysis_Report.pdf and visual training graphs

Project Structure Hangman-RL-HMM │ ├── corpus.txt # Training word dataset ├── test.txt # Evaluation dataset │ ├── probabilistic_oracle.py # HMM-based letter prediction model ├── hangman_env.py # Custom Hangman Gym environment ├── train_rl_agent.py # DQN training script ├── evaluate.py # Model evaluation + scoring │ ├── Analysis_Report.pdf # Final academic report ├── requirements.txt # Dependencies └── README.md # This file

Installation 1️. Clone the repo: git clone https://github.com//Hangman-RL-HMM.git cd Hangman-RL-HMM

2️. Install dependencies: pip install -r requirements.txt

For progress bar support: pip install stable-baselines3[extra]

Training the Agent Train the DQN agent using: python train_rl_agent.py

This will: Create a Hangman environment Train for multiple episodes using curriculum learning Save the model as dqn_hybrid_hangman_final.zip Training progress and logs are stored in: ./hangman_tb_logs/

Evaluation Run evaluation on the test dataset: python evaluate.py

RL Design Summary ComponentDescriptionState Vector[Masked word + guessed letters + lives left + HMM probability vector]Actions26 English letters (A–Z)Rewards+5 for correct, -20 for wrong, -30 for repeated, +100 win, -100 lossExplorationEpsilon-greedy (ε starts at 0.9 and decays by 0.9995)AlgorithmTabular Q-learning / DQNCurriculumShort → Medium → Long words

HMM Strategy The HMM learns character transition probabilities (P(letter_n | letter_{n-1})) from the corpus, helping the RL agent guess letters more intelligently. This probabilistic information acts as a prior for the RL state space.

Results Summary Training stabilized after several thousand episodes. Curriculum learning improved convergence speed. The final agent achieved a high win rate with minimal repeated guesses. For full analysis, see Analysis_Report.pdf.

Future Improvements Replace tabular Q-learning with Deep Q-Network (DQN) for better generalization. Incorporate Transformer-based letter modeling (e.g., BERT). Add parallel environment evaluation for faster training. Experiment with transfer learning from language embeddings.
