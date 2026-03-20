# 🚇 Seoul Metro Spatial Analysis & Insights
> **FastAPI와 PySpark를 활용한 지하철 역세권 분석 및 유동인구 시각화 서비스**

---

## 📌 1. Project Overview (개요)
서울시 지하철 공공 데이터를 기반으로 **역별 실시간 위치 정보**와 **주변 편의시설(카테고리별)** 정보를 결합한 인터랙티브 지도 서비스입니다. 특히 시간대별/요일별 유동인구 데이터를 PySpark로 가공하여 역세권의 특성을 분석하는 데 중점을 두었습니다.

### ✨ Key Goals
* **데이터 정합성 확보:** 파편화된 지하철 좌표 데이터와 요약 데이터를 정교하게 매칭
* **대용량 처리 파이프라인:** PySpark를 이용한 시간대별 유동인구 통계 연산 및 MariaDB 적재
* **고성능 API 제공:** FastAPI를 통한 비동기 데이터 통신 및 React 시각화

---

## 🛠️ 2. Tech Stack (기술 스택)
* **Backend:** FastAPI, SQLAlchemy, Pydantic, MariaDB, MySQL Connector
* **Data Engineering:** PySpark (4.1.1), Pandas
* **Frontend:** React, `react-kakao-maps-sdk`, Axios, React Router v7
* **Styling:** CSS3 (Dashboard, Maps 레이아웃 최적화)

---

## 🏗️ 3. System Architecture (시스템 구조)
```mermaid
graph LR
    A[공공데이터 API/SHP] --> B[PySpark ETL]
    B --> C[(MariaDB / MySQL)]
    C --> D[FastAPI Server]
    D --> E[React Dashboard]
```

---

## 🚀 4. Main Features (주요 기능)
* **통합 대시보드:** React 기반의 직관적인 지하철 데이터 시각화 인터페이스
* **역별 호선 통합 분석:** 서로 다른 호선에 속한 동일 역명을 그룹화하여 전체 통계 산출
* **카테고리 기반 장소 탐색:** Kakao API 연동을 통한 역 주변 15종 편의시설 실시간 필터링
* **스마트 라우팅:** React Router를 활용한 페이지 전환 및 지도 중심점 이동 관리

---

## ⚠️ 5. Troubleshooting & Challenges (시행착오 및 문제 해결)

### 🧩 1. 데이터 불일치 및 결측치 처리 (Data Integrity)
* **Problem:** 위/경도 좌표 데이터와 전체 지하철 요약 데이터 간의 불일치(특정 역의 좌표 누락) 발생.
* **Solution:** 전체 리스트를 기준으로 하되, 좌표가 없는 데이터는 **공공데이터 API 추가 호출** 또는 **법정동 중심점 좌표**를 활용해 보정하여 데이터 손실 최소화.

### 🕒 2. 복잡한 유동인구 시각화 (Time-series Analysis)
* **Problem:** 평일/공휴일/주말 및 시간대별 이동 인구 분석 시, 기준 시간 구분이 모호하여 데이터 왜곡 우려.
* **Solution:** 출근/퇴근/일반 시간대로 세션을 정의하고, PySpark를 활용해 시간대별 가중치를 부여한 통계 모델 구축.

### 🚉 3. 환승역 통합 집계 (Multi-line Integration)
* **Problem:** 같은 이름의 역이 호선별로 분리되어 있어 전체 유동인구 합산 시 개별 역으로 집계됨.
* **Solution:** **역명(Station Name)을 기준**으로 GroupBy 연산을 수행하여 여러 호선의 데이터를 하나로 통합하는 전처리 로직 구현.

### 💻 4. React-Kakao-Maps SDK 연동 이슈
* **Problem:** 라이브러리 미인식 및 지도 렌더링 높이(`0px`) 문제.
* **Solution:** `react-kakao-maps-sdk` 설치 및 `libraries=services` 파라미터 추가 확인. CSS 클래스(`.kakaoMap`)에 명시적 높이값을 부여하여 해결.

---

## 📅 6. Project Timeline (WBS)
* **1단계 (Data):** API 확보 및 PySpark 기반 RDD/DataFrame 맵핑 작업
* **2단계 (Backend):** FastAPI 스키마 정의 및 MariaDB 연동 (Router 분리)
* **3단계 (Frontend):** React 구조 설계, Axios 통신 및 지도 컴포넌트 구현
* **4단계 (Insight):** 시간대별 통계 고도화 및 대시보드 UI 최종 최적화
