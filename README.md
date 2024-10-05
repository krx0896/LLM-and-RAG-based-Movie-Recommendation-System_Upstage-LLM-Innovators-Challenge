## 📖 프로젝트 개요

이 프로젝트는 [명품인재×업스테이지] LLM Innovators Challenge에서 진행된 영화 추천 시스템입니다. 사용자의 쿼리를 바탕으로, LLM과 RAG(Retrieval-Augmented Generation)를 활용하여 9,300여 편의 영화 데이터에서 사용자의 취향에 맞는 영화를 추천합니다.

- **대회명**: [명품인재×업스테이지] LLM Innovators Challenge
- **참여 기간**: 2024년 9월 20일 ~ 2024년 10월 6일


## 🦴 시스템 프레임워크
- 본 시스템은 LLM을 활용하여 사용자의 질의를 처리하고, Pinecone 벡터 스토어에서 영화 데이터를 검색하여 가장 적합한 영화를 추천하는 시스템입니다. 실시간 데이터 검색이 가능한 RAG 구조를 사용하여 신뢰성 있는 추천 결과를 제공합니다.

![시스템 프레임워크](/image/프레임워크.png)

1. Prompt + Query
사용자가 추천받고 싶은 영화에 대한 쿼리를 입력합니다. 예를 들어, "가슴이 웅장해지는 역사적 배경을 담은 뮤지컬 영화 추천해줘"와 같은 질문을 던집니다.

2. Query (임베딩)
   사용자의 쿼리를 임베딩(벡터화)하여 시스템이 이해할 수 있는 형태로 변환합니다. 이 임베딩은 벡터 스토어에서 유사한 영화를 찾는 데 사용됩니다.

3. Movie Dataset
   영화 데이터셋에 미리 임베딩된 영화 정보를 저장해둔 공간입니다. 각 영화의 설명, 장르, 감독 등의 정보를 벡터화하여 저장합니다.

4. Pinecone Vector Store
   영화 데이터셋의 임베딩을 저장하는 Pinecone 벡터 스토어입니다. 사용자의 쿼리와 가장 유사한 영화를 찾기 위해 벡터 간의 유사도를 계산합니다.

5. Relevant Information for Enhanced Context
   벡터 스토어에서 검색된 영화들 중 상위 10개의 영화를 반환합니다. 이 정보는 향후 추천을 생성할 때 추가적인 컨텍스트로 사용됩니다.

6. User Metadata
   사용자의 나이, 선호하는 장르, 이미 본 영화 등의 메타데이터를 포함한 정보입니다. 이를 통해 사용자의 취향에 맞는 더 나은 영화를 추천할 수 있습니다.

7. Prompt + Query + Enhanced Context + User Metadata
   검색된 영화 정보, 사용자의 쿼리, 그리고 사용자 메타데이터를 결합하여 LLM에 전달할 컨텍스트를 강화합니다. 이를 통해 더욱 개인화된 추천을 생성할 수 있습니다.

8. Generated Movie Recommendations
   LLM을 통해 생성된 최종 영화 추천 목록이 사용자에게 전달됩니다. 추천된 영화 5편과 간단한 설명을 사용자에게 제공합니다.

## 🖥️ 코드 설명
1. **Python 환경 설정**  
   아래의 파이썬 패키지를 설치합니다:
   ```bash
   !pip install openai
   !pip install pinecone
   !pip install langchain
   !pip install langchain_community
   !pip install langchain_upstage

2. **API 사용**
- 벡터 스토어에 데이터 업로드 Pinecone에 영화 데이터를 업로드하여 벡터 스토어를 설정하기 위해 Pinecone에 API KEY를 발급 받아야합니다.
- LLM과 임베딩 모델을 사용하기 위해 Upstage API KEY를 발급받아야 합니다.
- 아래의 부분에 당신의 API KEY를 입력하세요
   ```bash
   export MY_UPSTAGE_API_KEY='your-upstage-api-key'
   export MY_PINECONE_API_KEY='your-pinecone-api-key'

3. **코드 시행**
- 데이터셋을 불러올 때 코드에서 본인의 path 경로를 넣어주세요.
- 데이터셋을 넣고 1번부터 13번 코드까지 순서대로 돌리시오.
- 만약 1~3의 과정을 끝맞췄다면 임베딩 된 데이터셋을 따로 저장(이전 단계가 시간이 오래 걸림) 후 이후로는 따로 저장한 데이터셋을 불러와 3.5단계부터 시행하면 됩니다.

## 🎞️ 데이터 소스
영화 데이터는 10,000편의 영화 설명 및 메타데이터를 포함하고 있습니다.
이 중 결측치를 제거한 9,300편의 영화만 사용하였습니다.
데이터는 **Kaggle IMDb Movie Dataset**에서 가져왔습니다.

[IMDb 데이터셋 다운로드 링크](https://www.kaggle.com/datasets/amanbarthwal/imdb-movies-data)

## 🎬 데모 영상
프로젝트의 데모 영상은 아래 링크에서 확인할 수 있습니다:
[데모 영상 유튜브 링크](https://youtu.be/cLDNgXLfgQU?si=jNMxtaVZ94VvPykl)

## 🎆 추천 결과 예시
쿼리: "가슴이 웅장해지는 역사적 배경을 담은 뮤지컬 영화 추천해줘"
추천 결과:

- 사운드 오브 뮤직 - 1930년대 오스트리아에서 한 젊은 수녀가 해군 장교의 일곱 자녀의 가정교사가 되는 이야기.
- 레 미제라블 - 19세기 프랑스에서 한 가난한 남자가 빵을 훔쳐 체포된 이야기.
- 왕과 나 - 1956년에 제작된 뮤지컬 영화로, 마거릿 랜든의 소설을 원작으로 한 작품.
- 위대한 쇼맨 - 세상을 즐겁게 하는 꿈을 꾸며 자신의 가족을 만들어가는 한 비전가의 이야기.
- 라 만차의 사나이 - 돈키호테가 동료 죄수들을 위해 연극을 펼치는 이야기를 담은 영화.

![시스템 프레임워크](/image/인터페이스.png)
