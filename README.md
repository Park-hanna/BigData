# NLP - Chat Bot 

## 자연어 처리 이해와 실습
### 목적 지향 대화, 오픈 도메인 대화가 가능한 Chat Bot
<hr>
<h2> 1. 목적 지향 대화 시스템 실습</h2>
<br>
TEXT 
<br> -> NLU(Natural Language Understanding) 
<br> -> DM(Dialogue Management) : DST(Dialog State Tracker), Policy 
<br> -> NLG (Natural Language Generation) 
<br> -> TEXT ACTION

## 1) 자연어 이해 실습
### 1-1 Embedding
#### Model : Word2Vec / Setting : Skip gram, Window size 2

### 1-2 Intent Classification
#### Model : TextCNN 

### 1-3 Information Extraction
#### Model : Bi-LSTM CRF

### 1-4 OOD(Out of Domain) Classification
#### Model : Deep Averaging Network

### 1-5 NLU System Configuration
<img src = "/path/NLU System .png" width="550px" height="300px"></img><br/>
<br>
<hr>

## 2) 대화 관리 및 자연어 생성

### 2-1 NLG 실습
#### NLG Template File Composition

| Intent | Slot | Template |
|:---:|:---:|:---:|
| dust | DATE | {DATE} 서울의 미세먼지는 나쁨입니다. |
| restaurant | LOCATION | {LOCATION} 주변의 추천 식당은 ----입니다. |
| travel | LOCATION | {LOCATION}의 추천 관광지는 XXXX입니다. |
| weather | DATE | {DATE} 서울의 날씨는 흐림입니다. |

#### NLG System Configuration
Result -> NLG : Make Search Key -> Matching Template -> Filling NLG Slot -> Select Template -> 1-Best Template
<br>
#### Singleton Based Dialog System
TEXT -> NLU -> NLG -> TEXT

### 2-2 DM 실습
#### Conversation Flow Design
<img src = "/path/conversation flow design.png" width="550px" height="300px"></img><br/>

| START STATE | END STATE | CONDITION |
|:---:|:---:|:---:|
| DS_START | DS_REQ_USER_INPUT | PASS |
| DS_REQ_USER_INPUT | DS_ACR_DUST_API | EX_dust |
| DS_ACT_DUST_API | DS_ANS_DUST_DATE_NLG | EX_dust EX_DATE |
| DS_REQ_USER_INPUT | DS_ANS_DUST_LOCATION_NLG | EX_ood EX_LOCATION <br> prev_ans_state == DS_ANS_DUST_DATE_NLG |

#### DST Design - BFS (너비 우선 탐색)

#### DM System Design
<img src = "/path/dm design.png" width="550px" height="300px"></img><br/>

<hr>
<h2> 2. 오픈 도메인 대화 시스템 </h2>

### 생성 기반 방식 
TEXT -> ENCODER -> DECODER -> TEXT 
:: RNN / HRED / GPT / Meena / DialoGPT / Blender Bot

### 1-1 E2E Chat Bot 실습
#### 생성 기반 방식 모델 소개 : Transformer
<img src = "/path/transformer 1.png" width="550px" height="300px"></img><br/>
<img src = "/path/transformer 2.png" width="550px" height="300px"></img><br/>

### 1-2 System Composition
#### E2E Chat Bot System Composition
TEXT -> E2E {ENCODER -> DECODER} -> TEXT, Probability

<hr>
<h2> 3. 하이브리드 대화 시스템 </h2>

### 1-1 System Composition
TEXT -> 목적지향 대화 시스템 -> Ranking -> TEXT <br>
TEXT -> 생성기반 대화 시스템 -> Ranking -> TEXT
