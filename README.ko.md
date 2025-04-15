[English](README.md) | [한국어](README.ko.md)
# [LLM-20-Questions](https://kaggle.com/competitions/llm-20-questions)

## 개요

이 시뮬레이션 대회에서는 **20 Questions 게임을 플레이할 수 있는 언어 모델을 만드는 것**이 목표입니다.  
참가 팀은 2 vs 2 형식으로 매치되며, **상대 팀보다 먼저 비밀 단어를 추론**하는 것이 승리 조건입니다.

각 팀은 다음 두 가지 역할의 LLM으로 구성됩니다:

- 질문자(Guesser): 질문을 던지고 정답 단어를 추측하는 역할
- 답변자(Answerer): 질문에 대해 "yes" 또는 "no"로 응답하는 역할

전략적인 질문과 응답을 통해, 가능한 적은 라운드 안에 정답을 맞히는 것이 목표입니다.

## 모델 및 초기 전략

우리는 많은 오픈소스 에이전트 중 대체로 높은 성능을 보인 -LLaMA 3.1B Instruct 모델을 선택했습니다.

초기에는 대회에 사용되는 키워드 전체 목록을 확보하여 모든 단어를 사전에 알고 있는 방식으로 우승을 노려보았지만 키워드 전체 목록을 확보하는 것이 현실적으로 어렵고 대회의 의도와 맞지 않는다고 판단하여 이 전략은 사용하지 않기로 결정했습니다.

## 핵심 전략

대신 GPT function-calling API를 활용해 구할 수 있는 한계 내에서 질문-키워드 매핑 데이터셋을 생성했습니다. 그 초안은 `keywords_gpt_analysis.ipynb` 파일에서 확인할 수 있습니다.

이 데이터셋을 기반으로
- 질문 선택:  
  - 각 질문은 현재 남아있는 키워드들을 최대한 균등하게 분리할 수 있는지를 기준으로 선택됩니다.  
  - 이는 정보 이득(information gain)을 최대화하기 위한 목적입니다.  
  - 질문의 균형성(`b`)이 0에 가까운 경우(모두 동일한 응답인 경우)는 제외됩니다.

- 키워드 필터링:  
  - 매 질문과 응답 후, 가능한 키워드 후보군을 rule-based 방식으로 필터링합니다.  
  - 이 과정을 통해 점점 키워드 후보가 줄어들고, 모델이 더 빠르게 추론할 수 있습니다.

- 질문 고갈 시:  
  - 더 이상 정보성이 있는 질문이 남아있지 않으면 지금까지의 게임 히스토리를 포함한 프롬프트를 활용해 모델이 자율적으로 질문과 답변을 생성합니다.


## 20 Questions 게임 규칙

- 게임은 총 20 라운드로 구성됩니다.
- 매 라운드마다 질문자는 질문을 제출하고, 이어서 정답 단어를 추측합니다.
- 답변자는 각 질문에 "yes" 또는 "no"로 응답합니다.
- 최종 목표는 가능한 적은 수의 질문으로 정답 단어를 맞히는 것입니다.

## 실행 환경

이 레포지토리는 Kaggle 노트북 환경을 기반으로 작성되었습니다.  
따라서 Kaggle 환경에서 실행해야 오류 없이 작동합니다.
Hugging Face에서 LLaMA, Qwen, Gemma 등 오픈소스 LLM을 다운로드했습니다.
이를 위해서는 Hugging Face 회원가입 및 HF Token 발급이 필요합니다.
자세한 사용 방법은 아래 가이드를 참고하세요: [Hugging Face 토큰 가이드](https://hunseop2772.tistory.com/372)

## 인용

Zoe Mongan, Luke Sernau, Will Lifferth, Bovard Doerschuk-Tiberi, Ryan Holbrook, Will Cukierski, and Addison Howard.  
LLM 20 Questions
## 증명서
![image](https://github.com/user-attachments/assets/514de31a-d1c2-4b56-a7f0-17e70053f24d)
