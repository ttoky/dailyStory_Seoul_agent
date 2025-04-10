# dailyStory_Seoul_agent

서울시 세출예산 데이터를 기반으로 LLM을 활용해 매일 새로운 이야기를 생성하고, X.com 계정(@news_seoulCity)에 게시하는 AI 에이전트입니다. 공공 데이터를 시민들에게 더 흥미롭게 전달하는 것을 목표로 합니다. 이 프로젝트는 [nonFictioningFiction](https://bit.ly/4hmcZa7) 시리즈 작업의 번외편인 [nonFictioningFiction_side stories](https://bit.ly/3R9bCRn) 중 하나입니다.

An AI agent that generates fictional stories daily using an LLM based on Seoul Metropolitan Government's expenditure budget data and posts them to the X.com account @news_seoulCity. It aims to make public data more engaging for citizens.This project is part of the [nonFictioningFiction](https://bit.ly/4hmcZa7) series and is specifically one of the [nonFictioningFiction_side stories](https://bit.ly/3R9bCRn).

********************************
[KR]
## 1. 데이터 소스 (Data Source)
이 프로젝트는 **서울시 열린데이터광장**에서 제공하는 **'세출운용사업 및 예산정보'** Open API를 주요 데이터 소스로 사용합니다. 데이터는 **XML 형식**으로 제공되며, 정기적으로 최신 예산 정보를 가져와 활용합니다. (API 사용을 위해서는 서울시 열린데이터광장에서 발급받은 인증키가 필요합니다.)
* **데이터셋 상세 정보 및 명세:** [서울 열린데이터 광장 - 세출운용사업 및 예산정보](https://data.seoul.go.kr/dataList/OA-13269/S/1/datasetView.do)

## 2. 핵심 기술 (Core Technology)

### 기능 (Functionality)
1.  서울시 Open API로부터 최신 세출예산 데이터를 매일 1회 파싱.
2.  파싱한 데이터 (XML형식) 사업명, 예산액, 날짜등 추출.
3.  추출된 정보를 바탕으로 언어 모델(LLM, 현재 gpt4-o 사용 중)에게 전달.
4.  LLM API로 주어진 정부에 기반한 짧은 소설(이야기) 텍스트를 생성.
5.  생성된 소설 텍스트를 X.com(트위터) API를 통해 지정된 계정에 자동 게시 (일 1회)
6.  개발된 에이전트는 사용자와 해당 게시물에 대한 대화 및 소설을 이어나갈 수 있음.

### 구조 (Architecture)

에이전트 모듈
* **데이터 수집기 (Data Fetcher):** Open API 호출 담당
* **XML 파서 (XML Parser):** 데이터 추출 담당
* **스토리 생성기 (Story Generator):** 프롬프트 생성 및 LLM 연동 담당
* **X.com 포스터 (X.com Poster):** 트윗 게시 담당

### 주요 사용 라이브러리 (Key Libraries)
* `requests`: 서울시 Open API 호출
* `xml.etree.ElementTree` (또는 `lxml`): XML 데이터 파싱
* `openai`, `google-generativeai` 등: LLM API 연동 라이브러리
* `tweepy`: X.com(트위터) API 연동
* `python-dotenv`: API 키 등 민감 정보 관리

## 3. 주요 기능 (Key Features)
* **자동 데이터 수집:** 서울시 세출예산 데이터를 정기적으로 자동 수집 및 처리.
* **AI 스토리 생성:** 추출된 예산 정보를 바탕으로 LLM을 활용하여 매일 새로운 이야기를 자동으로 생성.
* **자동 X.com 게시:** 생성된 스토리를 X.com 계정 [@news_seoulCity](https://x.com/news_seoulCity)에 자동으로 게시하여 공유합니다.
* **(개발 예정) 채팅 기능:** 사용자와 상호작용할 수 있는 채팅 에이전트로 확장.

## 4. 현재 상태 (Current Status)
현재 (2025년 4월 10일 기준), 서울시 예산 데이터를 기반으로 스토리를 생성하여 X.com 계정 [@news_seoulCity](https://x.com/news_seoulCity)에 자동으로 게시하는 핵심 기능은 **정상적으로 작동** 중.
사용자와 상호작용하는 채팅 에이전트 기능은 현재 **개발 계획 단계**.

## 5. 사용 방법 (Usage)
**TBA**

********************************
[EN]

## 1. Data Source
The primary data source for this project is the **'Expenditure Project and Budget Information' Open API** provided by the **Seoul Open Data Plaza**. The data is supplied in **XML format**, and the agent regularly fetches the latest budget information. (An API key issued by the Seoul Open Data Plaza is required for access.)
* **Dataset Details and Specification:** [Seoul Open Data Plaza - Expenditure Project and Budget Information](https://data.seoul.go.kr/dataList/OA-13269/S/1/datasetView.do)

## 2. Core Technology
### Functionality
1.  Parses the latest expenditure budget data from the Seoul Open API once daily.
2.  Extracts key information such as project name, budget amount, date, etc., from the parsed data (XML format).
3.  Passes the extracted information to a Large Language Model (LLM, currently using gpt4-o).
4.  Generates short fictional story texts based on the given information via the LLM API.
5.  Automatically posts the generated story text to the designated account via the X.com (Twitter) API (once daily).
6.  The developed agent can engage in conversations with users about the posts and continue the stories.

### Architecture
Agent Modules:
* **Data Fetcher:** Handles Open API calls.
* **XML Parser:** Responsible for data extraction.
* **Story Generator:** Manages prompt generation and LLM interaction.
* **X.com Poster:** Handles posting tweets.

### Key Libraries Used
* `requests`: For calling the Seoul Open API.
* `xml.etree.ElementTree` (or `lxml`): For parsing XML data.
* `openai`, `google-generativeai`, etc.: LLM API interaction library.
* `tweepy`: For interacting with the X.com (Twitter) API.
* `python-dotenv`: For managing sensitive information like API keys.

## 3. Key Features
* **Automated Data Fetching:** Regularly collects and processes Seoul's expenditure budget data automatically.
* **AI Story Generation:** Automatically generates new stories daily using an LLM based on extracted budget information.
* **Automated X.com Posting:** Shares the generated stories by automatically posting them to the X.com account [@news_seoulCity](https://x.com/news_seoulCity).
* **(Planned) Chat Functionality:** Expand into a chat agent capable of interacting with users.

## 4. Current Status
As of April 10, 2025, the core functionality of generating stories based on Seoul's budget data and automatically posting them to the X.com account [@news_seoulCity](https://x.com/news_seoulCity) is **operational**.
The interactive chat agent feature is currently in the **planning and development stage**.

## 5. Usage
**TBA**

