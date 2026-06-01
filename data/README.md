# Data

밥;도 프로젝트에서 사용한 CSV 데이터입니다. 개인정보가 포함될 수 있는 제출서류와 대용량 이미지 원본은 GitHub repo에서 제외했습니다.

## Directory Layout

```text
data/
├── raw/          # 부산 공공데이터 원본
├── processed/    # 전처리, 라벨링, 수집 현황 결과
└── reviews/      # 네이버 블로그 리뷰 크롤링 결과
```

## Raw Data

| File | Description |
| --- | --- |
| `raw/모범음식점 현황 조회.csv` | 부산 모범음식점 현황 |
| `raw/모범음식점 현황 조회 (1).csv` | 추가 수집된 부산 모범음식점 현황 |
| `raw/부산 착한가격업소 조회.csv` | 부산 착한가격업소 현황 |
| `raw/부산광역시 금정구_식품접객업현황_20240925.csv` | 금정구 식품접객업 현황 |
| `raw/부산광역시_동구_음식점현황.csv` | 동구 음식점 현황 |
| `raw/부산광역시_부산진구_일반음식점현황_20241008.csv` | 부산진구 일반음식점 현황 |
| `raw/부산광역시_수영구_모범음식점 현황.csv` | 수영구 모범음식점 현황 |
| `raw/부산도보여행 국문 정보.csv` | 부산 도보여행 관광 정보 |
| `raw/부산맛집 국문 정보.csv` | 부산맛집 국문 정보 |
| `raw/부산맛집 국문 정보 (1).csv` | 추가 수집된 부산맛집 국문 정보 |
| `raw/부산안심식당정보.csv` | 부산 안심식당 정보 |
| `raw/부산축제 국문 정보.csv` | 부산 축제 국문 정보 |
| `raw/전시 목록 조회.csv` | 부산 전시 목록 |
| `raw/택슐랭 선정 식당.csv` | 택슐랭 선정 식당 정보 |

## Processed Data

| File | Description |
| --- | --- |
| `processed/전체가게.csv` | 공공데이터에서 추출한 전체 돼지국밥 후보군 |
| `processed/유명가게.csv` | 기준점으로 사용한 유명 돼지국밥 가게 |
| `processed/맛집_전처리.csv` | 부산맛집 데이터 전처리 결과 |
| `processed/전체가게_수집현황.csv` | 전체 후보군 리뷰 수집 현황 |
| `processed/유명가게_수집현황.csv` | 유명 가게 리뷰 수집 현황 |
| `processed/전체가게_라벨링.csv` | 전체 후보군 리뷰 라벨링 결과 |
| `processed/유명가게_라벨링.csv` | 유명 가게 리뷰 라벨링 결과 |
| `processed/가게합본.csv` | 전체/유명 가게 라벨링 결과 통합본 |
| `processed/가게합본_사진수집현황.csv` | 통합 가게별 이미지 수집 현황 |
| `processed/restaurant_labels_output.csv` | 리뷰 라벨링 실험 출력 |

## Review Data

| Path | Description |
| --- | --- |
| `reviews/famous/` | 유명 돼지국밥 가게 블로그 리뷰 CSV |
| `reviews/all/` | 전체 후보 가게 블로그 리뷰 CSV |

## Excluded From Git

- `data/사진/`, `data/사진_정제/`: 크롤링 이미지 원본 및 정제본, 약 761MB
- `.env`: API 키 등 로컬 환경변수
- 제출 신청서, 동의서, 재학/휴학 증명서: 개인정보 및 제출용 문서
- `chromedriver-win64/`: 로컬 크롤링 실행 파일
