# 밥;도 (Bap;do)

> 부산 공공데이터와 리뷰/이미지 분석을 결합한 돼지국밥 맛집 추천 프로젝트<br>
> 2025 부산광역시 공공빅데이터 활용 창업경진대회

## Overview

밥;도는 부산의 대표 음식인 **돼지국밥**을 중심으로, 공공데이터와 네이버 리뷰/음식 이미지를 분석해 유명 맛집과 유사한 숨은 맛집을 추천하는 서비스 기획 및 데이터 분석 프로젝트입니다.

핵심 아이디어는 단순 평점 기반 추천이 아니라, 리뷰에서 드러나는 음식점의 특징과 음식 사진의 시각적 유사도를 함께 반영하는 것입니다.

## Portfolio Review Notes

### Problem

부산을 방문하거나 지역 맛집을 찾는 사용자는 유명 맛집에 집중된 정보만 접하기 쉽습니다. 이 프로젝트는 부산 공공데이터로 돼지국밥 후보군을 만들고, 리뷰 텍스트와 음식 이미지 유사도를 함께 사용해 "유명 맛집과 비슷한 숨은 가게"를 찾는 추천 흐름을 설계했습니다.

### Role and Ownership

이 저장소는 팀 프로젝트 산출물입니다. 로컬 git 이력에는 `Eunjae Lee`, `scnelMG`, `Park Mingyu`의 커밋이 함께 남아 있으므로 단독 제작물로 소개하지 않습니다. 아래 `My Contribution` 섹션은 이 포트폴리오에서 설명 가능한 기여 범위만 적은 것이며, 서비스 기획과 산출물은 팀 결과물로 보아야 합니다.

### Public Data and Safety

현재 저장소에는 작은 CSV와 데모 이미지가 포함되어 있지만, 공개 전에는 데이터 재배포 범위를 다시 확인해야 합니다. 특히 `data/raw/`의 공공데이터 출처별 이용 조건과 `data/reviews/`의 크롤링 리뷰 CSV 재배포 가능성은 별도 검토가 필요합니다. 대용량 크롤링 이미지, API 키, 제출 서류, 개인정보가 들어갈 수 있는 문서는 저장소에 포함하지 않습니다.

### Reproduce / Inspect

완전 재현보다는 공개 가능한 산출물 검토에 초점을 둡니다. 리뷰 수집, 라벨링, 이미지 유사도 분석 흐름은 `notebooks/`에서 단계별로 확인할 수 있고, 데모 화면은 `reports/`에서 확인할 수 있습니다. Gemini API를 사용하는 노트북은 `GOOGLE_API_KEY` 환경변수가 필요하며 키 값을 코드나 노트북에 직접 저장하지 않습니다.

### Limitations and Public Status

추천 결과는 크롤링 시점, 공개 데이터 품질, 리뷰 수집 범위, 이미지 수집 가능 여부에 영향을 받습니다. 또한 데이터 재배포와 공동 저작권 검토가 끝나기 전까지는 이 저장소를 그대로 push-ready로 보지 않고, 포트폴리오 후보로만 다룹니다.

## Key Features

- 부산 공공데이터 기반 음식점 후보군 구축
- 네이버 블로그/스마트스토어 리뷰 크롤링 및 수집 현황 관리
- Gemini API와 LangChain 기반 돼지국밥 특징 라벨링
- CLIP 임베딩 기반 국밥 이미지 유사도 계산
- 텍스트 특징과 이미지 특징을 결합한 유사 맛집 추천 파이프라인
- 서비스 화면, 대시보드, Figma 시안으로 사용자 경험 구체화

## Tech Stack

| Area | Tools |
| --- | --- |
| Data Collection | Python, Selenium, BeautifulSoup |
| Data Processing | Pandas, Polars |
| NLP / Labeling | LangChain, Gemini API |
| Vision | CLIP, image embeddings |
| Recommendation | Cosine Similarity, FAISS |
| Design | Figma, dashboard mockups |

## Repository Structure

```text
.
├── data/
│   ├── raw/          # 부산 공공데이터 원본 CSV
│   ├── processed/    # 전처리, 라벨링, 수집 현황 결과 CSV
│   └── reviews/      # 크롤링한 블로그 리뷰 CSV
├── notebooks/        # 수집, 전처리, 라벨링, 이미지 유사도 분석 노트북
├── reports/          # 서비스 화면 및 분석 결과 이미지
├── LICENSE
└── README.md
```

## Data

이 repo에는 GitHub에서 확인하기 적절한 크기의 CSV 데이터만 포함했습니다.

- `data/raw`: 부산 음식점, 관광, 축제, 전시 등 공공데이터 원본
- `data/processed`: 돼지국밥 후보군, 유명 가게 목록, 라벨링 결과, 수집 현황
- `data/reviews`: 유명 가게 및 전체 후보 가게의 블로그 리뷰 크롤링 결과

크롤링 이미지 원본과 정제 이미지는 약 761MB 규모라 GitHub 일반 repo에는 포함하지 않았습니다. 대신 이미지 수집/정제/유사도 분석 과정은 `notebooks/`에 보존했습니다.

자세한 파일 목록은 [data/README.md](data/README.md)를 참고하세요.

## Notebook Workflow

| Step | Notebook | Description |
| --- | --- | --- |
| 1 | `bapdo-pork-soup-list.ipynb` | 공공데이터 기반 돼지국밥 음식점 후보군 생성 |
| 2 | `bapdo-review-crawling.ipynb` | 네이버 블로그 리뷰 수집 |
| 3 | `bapdo-review-langchain.ipynb` | 리뷰 기반 음식점 특징 라벨링 |
| 4 | `bapdo-review-summarizer.ipynb` | 리뷰 요약 및 라벨링 실험 |
| 5 | `bapdo-image-crawling.ipynb` | 음식점 이미지 수집 |
| 6 | `bapdo-image-similarity.ipynb` | CLIP 기반 이미지 유사도 분석 |
| 7 | `bapdo-naver-smartstore.ipynb` | 네이버 스마트스토어 리뷰 수집 실험 |

## Setup

```powershell
pip install -r requirements.txt
```

Gemini API를 사용하는 노트북은 실행 전에 환경변수를 설정해야 합니다.

```powershell
$env:GOOGLE_API_KEY="your-api-key"
```

## Recommendation Pipeline

```mermaid
flowchart TD
    raw["Public restaurant data"] --> candidates["Pork soup candidate list"]
    reviews["Crawled reviews"] --> labels["LLM feature labeling"]
    images["Crawled food images"] --> embeddings["CLIP image embeddings"]
    candidates --> merged["Restaurant feature table"]
    labels --> merged
    embeddings --> similarity["Similarity scoring"]
    merged --> similarity
    similarity --> topn["Top-N similar restaurant recommendations"]
```

## Service Flow

```mermaid
flowchart LR
    user["User"] --> query["Search or select favorite restaurant"]
    query --> analysis["Review and image feature analysis"]
    analysis --> recommend["Similarity-based recommendation"]
    recommend --> result["Hidden local restaurant list"]
    result --> user
```

## Demo Screens

<p align="center">
  <img src="reports/similar_gukbap_search.png" width="30%"/>
  <img src="reports/my_gukbap_search.png" width="30%"/>
  <img src="reports/dashboard.png" width="30%"/>
</p>

[Figma 시안 보기](https://www.figma.com/design/J18MP1ViHTA5qKEUTFFIEt/Untitled?node-id=0-1&p=f&t=TBIj4cpfDHfGXVAY-0)

## My Contribution

- 부산 공공데이터 기반 음식점 후보군 수집 및 전처리
- 네이버 리뷰/이미지 크롤링 파이프라인 구성
- Gemini API와 LangChain을 활용한 돼지국밥 특징 라벨링
- CLIP 기반 국밥 이미지 유사도 분석
- 추천 서비스 UX 흐름, 화면 설계, 데이터 산출물 정리

## Team

김태연, 박민규, 이은재, 홍예원
