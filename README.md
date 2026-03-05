# ✈️Air Route Demand Analysis(ICN 2022-2025)

## 🏠프로젝트 제목
항공 노선 수요 분석 프로젝트

## 📌프로젝트 개요
코로나 이후 여객 수요가 빠르게 회복되며, 항공 산업의 구조적 변화가 가속화되었다.
본 프로젝트는 **인천국제공항 출·도착 기준(2022.07~2025.06)** 공공 항공 데이터를 활용하여:

- 년·월별 여객 수요 추세
- 시즌(동·하절기) 인기 노선·여행지
- 항공사 시장 점유율 구조
- 환승 공항·항공사 패턴
- 탑승률(Proxy) 영향 요인(LGBM + SHAP)
  
까지 종합 분석하는 프로젝트이다.
  
## 🔍분석 프로세스
### 1) 데이터 전처리 - '01_air_route_preprocessing.ipynb'
  - Raw 데이터 로딩 및 병합
  - 컬럼명 통일 및 불필요 데이터 제거
  - 결측치 점검 및 타입 변환
  - 파생변수 생성(총여객(명), 항공화물(kg), 평균탑승객(명/편)_proxy)
  - 공항 코드 매핑
  - 여객/화물 데이터 분리 및 저장
   
### 2) 탐색적 분석 및 모델링 - '02_air_route_analysis.ipynb'
  - 년·월별 총여객 추세 시각화
  - 시즌 기반 인기 노선 및 여행지 분석
  - 항공사 시장 점유율 비교
  - 환승 공항·항공사 TOP10 분석
  - LGBM 기반 탑승률(Proxy) 예측 모델링
  - SHAP 기반 영향 요인 분석

## 💡주요 분석 결과
✔ 년도·월별 수요 추이
- 2022~2023 회복 속도 매우 빠름
- 2024~2025년은 회복 안정화 국면으로 진입
- 7·8·10월(하계), 12·1월(동계) 강한 peak
- 2·9·11월은 수요 감소 구간
  
✔ 시즌별 인기 노선/여행지
- 전반적으로 일본(도쿄, 오사카, 후쿠오카) 강세
- 홍콩, 태국도 지속적 상위권
- 2024 하계 중국(상하이) 수요 부상
- 2024~2025 베트남 지역 수요 이동(호치민 → 나트랑)

✔ 항공사 시장 점유율
- 인천 출·도착 국내 항공사 비중 65%↑
- 2022~2024 대비, 이스타항공(ZE) 점유율 크게 상승
- 중국 항공사 점유율 2024~2025 상승 추세

✔ 환승패턴
- 아시아태평양 기준, 환승객 다수 공항: MNL, SGN, BKK, NRT, PVG
- 동남아·중국 공항: 허브 기능(환승비율↑)
- 일본·홍콩·싱가포르: 목적지 기능(환승비율↓)
- DL/UA/AC(북미 항공사)와 OM(몽골항공) ICN에서 환승객 규모가 상대적으로 크게 나타남
  
✔ 탑승률(proxy) 예측 모델
- 주요 영향 요인
  1. 운항(편)
  2. 총여객(명)
  3. 수하물(kg)
  4. 지역
- 총여객↑ + 운항편수↓ → 탑승률(proxy)↑
- 장거리 노선의 탑승률 상대적으로 높음
  
## 🧰기술 스택
- Python
- 데이터: pandas, glob, numpy, datetime
- 시각화: matplotlib, plotly
- 모델링: sklearn, LightGBM
- 해석: shap
  
## 📂폴더 구조
```
AIR_ROUTE_ANALYSIS/
├── data/ # raw 데이터, 전처리 완료 데이터, test데이터 모델링
│ ├── 노선별 항공사별 항공운송실적(2022년 전체).csv
│ ├── 노선별 항공사별 항공운송실적(2023년 전체).csv
│ ├── 노선별 항공사별 항공운송실적(2024년 전체).csv
│ ├── 노선별 항공사별 항공운송실적(2025년 01~07).csv
│ ├── 국토교통부_세계공항_정보_20241231.csv
│ ├── passenger_analysis.csv
│ └── pred_result.csv
│
├── notebooks/ # 전처리, 분석 코드
│ ├── 01_air_route_preprocessing.ipynb
│ └── 02_air_route_analysis.ipynb
│
├── results/ # 분석 결과 시각화
│ ├── 01_monthly_total_passenger_trend.png
│ ├── 02_monthly_growth_rate.png
│ ├── 03_peak_season_top10_destinations.png
│ ├── 04_nonpeak_top10_destinations.png
│ ├── 05_airline_market_share_by_year.png
│ ├── 06_top10_airports_transit_APAC.png
│ ├── 07_top10_airlines_transit.png
│ ├── 08_top10_airlines_transit_excluding_Korean_carriers.png
│ ├── 09_load_factor_shap_structure.png
│ └── 10_load_factor_feature_importance.png
│
└── README.md
```

## ⚠한계점
- 실제 좌석 공급량(ASK) 데이터 부재 → 정확한 탑승률(Load Factor) 계산 불가 → 편당 평균 탑승객을 proxy 지표로 활용하여 탑승률 구조를 간접적으로 분석
- 여정 정보 부재 → 환승 패턴이 어떤 지역 간 이동(ex: 유럽-동남아-ICN, ICN-APAC-북미)에 의해 발생했는지 확인 어려움
- 노선 공급계획(신규취항/감편) 데이터 부재 → 수요·공급 구조를 온전히 해석하기 어려움







