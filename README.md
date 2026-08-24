# 밥;도 - 부산 돼지국밥 맛집 추천

<p align="center">부산 공공데이터 활용 프로젝트 · 리뷰 텍스트 · 이미지 유사도 · 맛집 추천</p>

> 부산 공공데이터, 리뷰 텍스트, 음식 이미지 유사도를 결합해 유명 맛집과 비슷한 숨은 돼지국밥집을 추천하는 데이터 서비스 프로젝트입니다.

[![Python](https://img.shields.io/badge/Python-Data%20Pipeline-3776AB?logo=python&logoColor=white)](requirements.txt)
[![LangChain](https://img.shields.io/badge/LangChain-Review%20Labeling-1C3C3C)](notebooks)
[![CLIP](https://img.shields.io/badge/CLIP-Image%20Similarity-4B8BBE)](notebooks)
[![Portfolio](https://img.shields.io/badge/Portfolio-Public%20Data-2ea44f)](data/README.md)

## 개요

밥;도는 부산의 대표 음식인 돼지국밥을 중심으로, 공공데이터와 네이버 리뷰/음식 이미지를 분석해 유명 맛집과 유사한 숨은 맛집을 추천하는 서비스 기획 및 데이터 분석 프로젝트입니다.

단순 평점 기반 추천이 아니라, 리뷰에서 드러나는 음식점 특징과 음식 사진의 시각적 유사도를 함께 사용해 “내가 좋아한 국밥집과 비슷한 가게”를 찾는 흐름을 설계했습니다.

## 문제 정의

부산을 방문하거나 지역 맛집을 찾는 사용자는 이미 유명한 가게 위주의 정보에 노출되기 쉽습니다. 이 프로젝트는 공공데이터로 후보 음식점을 만들고, 리뷰 텍스트와 이미지 유사도를 결합해 유명 맛집과 비슷한 숨은 가게를 찾는 추천 흐름을 제안했습니다.

## 내 역할

팀 프로젝트 산출물이며, 이 저장소는 단독 제작물로 소개하지 않습니다. 공개 가능한 기여 범위는 다음과 같습니다.

- 부산 공공데이터 기반 돼지국밥 음식점 후보군 수집/전처리
- 네이버 리뷰와 이미지 크롤링 pipeline 구성
- Gemini API와 LangChain 기반 리뷰 특징 라벨링
- CLIP embedding 기반 국밥 이미지 유사도 분석
- 추천 서비스 UX 흐름과 화면 산출물 정리
- raw/crawled data와 대용량 이미지 자료의 공개 제외 처리

## 기술적 의사결정

| 영역 | 선택 | 이유 |
| --- | --- | --- |
| 후보군 구성 | 부산 공공데이터 | 지역성과 공신력 있는 초기 음식점 pool을 만들기 위함입니다. |
| 리뷰 분석 | Gemini API, LangChain | 리뷰에서 맛, 양, 분위기, 웨이팅 등 특징을 구조화하기 위함입니다. |
| 이미지 분석 | CLIP embedding | 음식 사진의 시각적 유사도를 텍스트 feature와 함께 활용하기 위함입니다. |
| 추천 | Cosine similarity, FAISS | 유명 맛집과 유사한 후보를 빠르게 찾기 위한 구성입니다. |
| 공개 정책 | small sample / docs 중심 | 리뷰와 이미지 크롤링 데이터의 재배포 리스크를 줄이기 위함입니다. |

## 추천 파이프라인

```mermaid
flowchart TD
    raw["부산 공공데이터"] --> candidates["돼지국밥 후보군"]
    reviews["크롤링 리뷰"] --> labels["LLM 특징 라벨링"]
    images["음식 이미지"] --> embeddings["CLIP embedding"]
    candidates --> merged["음식점 feature table"]
    labels --> merged
    embeddings --> similarity["유사도 계산"]
    merged --> similarity
    similarity --> topn["유사 맛집 추천"]
```

## Figma 화면 시안

<p align="center">
  <img src="reports/similar_gukbap_search.png" alt="유사 국밥집 탐색 Figma 시안" width="40%" />
  <img src="reports/my_gukbap_search.png" alt="취향 기반 국밥 탐색 Figma 시안" width="40%" />
</p>

화면은 추천 흐름을 검토하기 위해 만든 Figma 시안입니다. 저장소에는 데이터 분석과 추천 PoC를 담았으며, 별도 production 앱은 포함하지 않습니다.

[Figma 시안 보기](https://www.figma.com/design/J18MP1ViHTA5qKEUTFFIEt/Untitled?node-id=0-1&p=f&t=TBIj4cpfDHfGXVAY-0)

## 재현 가능성

```powershell
pip install -r requirements.txt
$env:GOOGLE_API_KEY="your-api-key"
```

Gemini API를 사용하는 notebook은 환경 변수가 필요합니다. API key는 코드나 notebook에 직접 저장하지 않습니다.

공개 checkout에서는 notebook 흐름과 reports 산출물을 검토할 수 있습니다. raw review, raw image, 대용량 crawling result는 공개하지 않습니다.

## 공개/비공개 경계

- 공개: 공공데이터 기반 후보군, notebook workflow, Figma 화면 시안
- 제외: 대용량 크롤링 이미지, 재배포 권한이 불명확한 raw review, 비밀값·제출 문서
- 검증: `python scripts/verify_portfolio.py`로 필수 문서와 대용량 tracked 파일을 확인합니다.

## 한계

- 추천 결과는 크롤링 시점과 리뷰 수집 범위에 영향을 받습니다.
- 리뷰/이미지 데이터의 재배포 권한을 항상 별도로 확인해야 합니다.
- 서비스 구현은 PoC/기획 단계이며 production app은 포함되어 있지 않습니다.

## 이용 안내

이 저장소는 포트폴리오·학습 기록 열람을 위해 공개합니다. 코드·문서·이미지의 재사용, 수정, 배포는 사전 문의가 필요합니다.
