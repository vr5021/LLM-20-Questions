[English](README.md) | [한국어](README.ko.md)

# [LLM-20-Questions](https://kaggle.com/competitions/llm-20-questions)

## Overview
In this simulation competition, you must create a language model capable of playing the game 20 Questions. Teams will be paired in 2 vs 2 player matchups and race to deduce the secret word first.
Each team will consist of one guesser LLM, responsible for asking questions and making guesses, and one answerer LLM, responsible for responding with "yes" or "no" answers. Through strategic questioning and answering, the goal is for the guesser to correctly identify the secret word in as few rounds as possible.        
        
We selected the LLaMA 3.1B Instruct model because it demonstrated strong performance across many open-source agent implementations.      
Initially, we thought we could win first prize by obtaining a complete dictionary of all the keywords used in the competition. However, we decided not to pursue this strategy due to the difficulty of acquiring a comprehensive list of keywords and because it did not align with the intended purpose of the competition.      
     
Instead, we created a small set of mapping questions to keywords using the GPT function-calling API. A rough version of this can be found in keywords_gpt_analysis.ipynb.
Using this set, each question is chosen based on its ability to evenly divide the remaining keyword candidates, ensuring maximum information gain.
When no informative questions that can divide keywords remain, the model autonomously generates new questions and answers based on a prompt including the accumulated game history.

## 20 Questions Rules
The game will proceed in rounds, with 20 total rounds. At the start of each round, the two questioners will each submit a question trying to guess the target word, and then submit their guess for what the target word is.
The goal is for each team's questioner to guess the target word in as few rounds as possible based on the information provided by the answering agent.

## Preparation
This repository was copied from a Kaggle notebook designed to run in the Kaggle environment. To execute the code without errors, it must be run within the Kaggle environment with the appropriate settings.       
We used Hugging Face to download open-source LLMs such as LLaMA, Qwen, and Gemma. To do this, you’ll need to sign up for Hugging Face and obtain an HF token.     
You can find a detailed guide [here](https://hunseop2772.tistory.com/372).   

## Citation
Zoe Mongan, Luke Sernau, Will Lifferth, Bovard Doerschuk-Tiberi, Ryan Holbrook, Will Cukierski, and Addison Howard. LLM 20 Questions. 

## Certification
![image](https://github.com/user-attachments/assets/514de31a-d1c2-4b56-a7f0-17e70053f24d)
