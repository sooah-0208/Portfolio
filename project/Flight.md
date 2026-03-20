# ✈️ Flight Data Analysis & Interactive Visualization
> **항공사·운송기·운항 정보를 연동한 데이터 ETL 및 인사이트 시각화 프로젝트**

---

## 📌 1. Project Overview (개요)
다양한 항공 운항 관련 공공 데이터를 수집하고, **ETL(Extract, Transform, Load)** 프로세스를 통해 정규화된 데이터베이스를 구축한 후 **Streamlit**을 통해 시각화 대시보드를 구현한 프로젝트입니다.

### ✨ Key Goals
* **데이터 파이프라인 구축:** 항공사 코드, 공항 코드 등 파편화된 데이터를 정제하여 RDBMS 적재
* **인사이트 도출:** 항공사별 운항 리스크와 노선 전략을 제안하기 위한 통계 분석
* **공간 정보 시각화:** Pydeck을 활용하여 노선별 운항 경로 및 밀집도 시각화

---

## 🛠️ 2. Tech Stack (기술 스택)
* **Language:** Python
* **Dashboard:** Streamlit (웹 프레임워크), Pydeck (공간 정보 시각화), Altair (통계 차트)
* **Data Processing:** Pandas (Data Cleaning), SQLAlchemy (DB Connection)
* **Database:** MySQL (`db_to_air` - 비행, 운송기, 항공사 테이블 정규화)

---

## 🏗️ 3. Database Schema (데이터 구조)
데이터 무결성과 쿼리 효율성을 위해 3개의 주요 테이블로 정규화하였습니다.
* **항공사(Airline):** 항공사 IATA/ICAO 코드 및 정식 명칭 관리
* **운반대(Carrier):** 비행기 기종별 수송 능력 및 제원 데이터
* **비행(Flight):** 실제 운항 기록 (출발/도착지 좌표, 시간, 사용 운반대 연동)

---

## 🚀 4. Main Features (주요 기능)
| 기능 | 설명 |
| :--- | :--- |
| **ETL 자동화** | Python을 이용해 원천 데이터를 정제 후 `db_to_air` 스키마에 자동 적재 |
| **인터랙티브 대시보드** | Streamlit 기반의 실시간 항공 데이터 필터링 및 조회 기능 |
| **비행 경로 시각화** | Pydeck의 `ArcLayer` 등을 활용한 출발-도착지 간 항공 노선 시각화 |
| **데이터 분석 차트** | Altair를 활용한 항공사별 운항 효율성 및 리스크 분석 그래프 제공 |

---
[설명](map.png)
---

## ⚠️ 5. Troubleshooting & Lessons Learned (시행착오 및 회고)

### 🔗 기술적 해결: 데이터 관계 설정 및 정규화
* **Issue:** 초기 단일 테이블 구조에서 데이터 중복과 속도 저하 발생.
* **Solution:** 1~3차 정규화를 통해 테이블을 분리하고 외래 키(FK)를 설정하여 무결성 확보.
* **Optimization:** 수만 건의 기록 적재 시 `chunksize` 조절 및 **Bulk Insert**로 속도 약 5배 개선.

### 💡 프로젝트 관리 회고 (Lessons Learned)
이번 프로젝트를 통해 기술적 역량 외에도 **팀 협업과 주제 선정의 중요성**을 깊이 깨달았습니다.
* **주제 선정의 명확화:** 초기 주제 설정이 모호하여 시각화 양식의 통일성이 부족했던 점을 파악했습니다. 향후 명확한 페르소나와 목적을 설정하고 접근할 예정입니다.
* **소통 및 중간보고:** 팀원 간 역할 분담을 위해 **1시간 단위의 타임별 중간보고**와 회차별 파트 분배의 필요성을 절감했습니다.
* **일정 관리:** 분석과 구현에 치중하여 발표 준비 시간이 부족했던 점을 보완하기 위해, 차기 WBS 수립 시 **발표 준비 및 리허설 단계**를 명시적으로 포함할 계획입니다.

---

## 📅 6. Project Timeline (WBS)
* **Phase 1:** 항공 운항 API 및 CSV 데이터 수집
* **Phase 2:** MySQL 스키마 설계 및 데이터 정규화 적재
* **Phase 3:** Streamlit & Pydeck을 이용한 데이터 시각화 구현
* **Phase 4 (Next Step):** 주제별 인사이트 도출 및 발표 리포트 작성
