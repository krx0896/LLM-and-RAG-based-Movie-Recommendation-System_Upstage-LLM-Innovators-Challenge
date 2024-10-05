# LLM & RAG 기반 영화 추천 시스템

![시스템 프레임워크](/image/프레임워크.png)

## 프로젝트 개요

이 프로젝트는 [명품인재×업스테이지] LLM Innovators Challenge에서 진행된 영화 추천 시스템입니다. 사용자의 쿼리를 바탕으로, LLM과 RAG(Retrieval-Augmented Generation)를 활용하여 9,300여 편의 영화 데이터에서 사용자의 취향에 맞는 영화를 추천합니다.

- **대회명**: [명품인재×업스테이지] LLM Innovators Challenge
- **참여자**: 고려대학교 산업경영공학과 김윤성
- **참여 기간**: 2024년 9월 20일 ~ 2024년 10월 6일

## 시스템 프레임워크 설명

본 시스템은 LLM을 활용하여 사용자의 질의를 처리하고, Pinecone 벡터 스토어에서 영화 데이터를 검색하여 가장 적합한 영화를 추천하는 시스템입니다. LLM의 할루시네이션 문제를 보완하기 위해 실시간 데이터 검색이 가능한 RAG 구조를 사용하여 신뢰성 있는 추천 결과를 제공합니다.

## 설치 방법

1. **Python 환경 설정**  
   아래의 파이썬 패키지를 설치합니다:
   ```bash
   pip install -r requirements.txt
요구되는 주요 패키지:

upstage-api
pinecone-client
langchain
tqdm
API Key 설정
Upstage에서 API Key를 발급받고, 환경 변수에 설정합니다.
Pinecone에서 API Key를 발급받고, 환경 변수에 설정합니다.
bash
코드 복사
export MY_UPSTAGE_API_KEY='your-upstage-api-key'
export MY_PINECONE_API_KEY='your-pinecone-api-key'
사용 방법
벡터 스토어에 데이터 업로드 Pinecone에 영화 데이터를 업로드하여 벡터 스토어를 설정합니다:

python
코드 복사
# 벡터 스토어에 영화 설명 및 메타데이터를 업로드합니다.
vectorstore.upsert(vectors=batch)
영화 추천 요청 사용자는 간단한 질의를 통해 영화 추천을 받을 수 있습니다:

python
코드 복사
query = "마법사가 나오는 판타지 영화 추천해줘"
results = vectorstore.similarity_search(query, k=5)
추천 결과 출력

python
코드 복사
for result in results:
    print(f"Title: {result.metadata['Title']}")
    print(f"Description: {result.metadata['Description']}")
데이터 소스
영화 데이터는 약 9,300편의 영화 설명 및 메타데이터를 포함하고 있습니다.
데이터는 **Kaggle IMDb Movie Dataset**에서 가져왔습니다.

데모 영상
프로젝트의 데모 영상은 아래 링크에서 확인할 수 있습니다:
데모 영상 유튜브 링크

추천 결과 예시
쿼리: "가슴이 웅장해지는 역사적 배경을 담은 뮤지컬 영화 추천해줘"
추천 결과:

사운드 오브 뮤직 - 1930년대 오스트리아에서 한 젊은 수녀가 해군 장교의 일곱 자녀의 가정교사가 되는 이야기.
레 미제라블 - 19세기 프랑스에서 한 가난한 남자가 빵을 훔쳐 체포된 이야기.
왕과 나 - 1956년에 제작된 뮤지컬 영화로, 마거릿 랜든의 소설을 원작으로 한 작품.
위대한 쇼맨 - 세상을 즐겁게 하는 꿈을 꾸며 자신의 가족을 만들어가는 한 비전가의 이야기.
라 만차의 사나이 - 돈키호테가 동료 죄수들을 위해 연극을 펼치는 이야기를 담은 영화.
인터페이스 사진

markdown
코드 복사

### 주의사항:
1. 이미지 경로(`./path_to_framework_image.png`, `./path_to_interface_image.png`)는 실제 프로젝트 디렉토리에서 이미지 파일을 저장한 위치로 바꿔주세요.
2. 유튜브 데모 영상의 링크도 실제 URL로 교체해주세요.

이 README 마크다운 파일을 통해 깃허브에 프로젝트 정보를 명확하게 설명할 수 있습니다.
