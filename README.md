# 🎬 Three Sons Movie Cinema

> HTML · CSS · Vanilla JavaScript 프론트엔드와 GCP 클라우드 서버 + MySQL 데이터베이스로 구현한 영화관 예매 웹 사이트

---

## 📌 프로젝트 개요

**Three Sons Movie Cinema**는 실제 영화관 예매 시스템을 모사한 클라우드 기반 웹 프로젝트입니다.  
HTML · CSS · 순수 JavaScript로 제작한 프론트엔드를 **GCP(Google Cloud Platform) VM 인스턴스**에 배포하고,  
**MySQL** 데이터베이스를 연동하여 회원 정보·예매 데이터를 관리합니다.

> ⚠️ **참고**: GCP VM 인스턴스는 현재 종료된 상태로 외부 접속이 불가합니다.

---

## 🎥 실행 영상


https://github.com/user-attachments/assets/700d8a17-e9bb-481f-917b-7d46a8fc3bba



---

## 🛠 기술 스택

### 프론트엔드
| 구분 | 기술 |
|------|------|
| 마크업 | HTML5 |
| 스타일 | Vanilla CSS |
| 동작 | Vanilla JavaScript (ES6+) |
| 데이터 전달 | URL Query Parameter (`URLSearchParams`) |
| 미디어 | MP4 동영상, JPG/PNG 이미지 |

### 백엔드 · 인프라
| 구분 | 기술 |
|------|------|
| 클라우드 | GCP (Google Cloud Platform) VM 인스턴스 |
| 웹 서버 | Apache / Tomcat (포트 8080) |
| 데이터베이스 | MySQL (GCP VM 터미널에서 직접 쿼리 작성) |
| 배포 방식 | GCP VM SSH 접속 후 직접 배포 |

---

## 📁 프로젝트 구조

```
Cloud/
├── index.html              # 메인 홈 페이지 (영화 목록 + 배경 동영상)
├── index.css
│
├── showingmoive.html       # 상영 중인 영화 목록
├── showingmoive.css
│
├── reservation.html        # 영화 예매 (영화 · 날짜 · 시간 선택)
├── reservation.css
│
├── seat.html               # 인원 및 좌석 선택
├── seat_style.css
│
├── pay.html                # 결제 정보 확인 및 결제 수단 선택
├── pay.css
│
├── food_combo.html         # 매점 - 콤보
├── food_popcon.html        # 매점 - 팝콘
├── food_drink.html         # 매점 - 음료
├── food_snack.html         # 매점 - 간식
├── food.css
│
├── suggest.html            # 영화 추천 (장르·연령·별점·키워드 필터)
├── suggest_style.css
│
├── login.html              # 로그인 페이지
├── login.css
│
├── newClient.html          # 회원가입 페이지
├── newClient.css
│
├── View_details/           # 영화별 상세 정보 페이지 (14편)
│   ├── all.css
│   ├── glady.html          # 글래디에이터
│   ├── wikid.html          # 위키드
│   ├── chungsul.html       # 청설
│   ├── four.html           # 사흘
│   ├── hidden.html         # 히든페이스
│   ├── fire.html           # 소방관
│   ├── conan.html          # 명탐정 코난
│   ├── guical.html         # 귀멸의 칼날
│   ├── caerol.html         # 캐롤
│   ├── notebook.html       # 노트북
│   ├── manlove.html        # 남자가 사랑할 때
│   ├── vaetaerang.html     # 베테랑 2
│   ├── gisaeng.html        # 기생충
│   └── ...
│
└── image/                  # 이미지 및 동영상 에셋
    ├── *.jpg / *.png
    └── *.mp4
```

---

## ☁️ 시스템 아키텍처

![system architecture](https://github.com/user-attachments/assets/1b7edcf6-0020-4446-9865-37f3e4d41aac)

> **참고**: 서버 측 코드(DB 쿼리, 서버 설정 등)는 GCP VM 터미널에서 직접 작성·관리되었으며  
> 이 저장소에는 **프론트엔드(HTML/CSS/JS) 파일만** 포함되어 있습니다.

---

## 🔄 페이지 플로우

```
메인 (index.html)
    │
    ├── 영화 목록 (showingmoive.html) ──→ 상세보기 (View_details/*.html)
    │
    ├── 예매 (reservation.html)
    │       │  영화 · 날짜 · 시간 선택 후 URL 파라미터로 전달
    │       ↓
    │   좌석 선택 (seat.html)
    │       │  인원(일반/청소년/경로/우대) · 좌석(A~D, 1~5) 선택
    │       ↓
    │   결제 (pay.html)
    │       │  예매 정보 수신 및 결제 수단 선택
    │
    ├── 매점 (food_combo.html / food_popcon.html / food_drink.html / food_snack.html)
    │
    └── 추천 (suggest.html)
            장르 · 연령 · 별점 · 키워드 기반 영화 필터링
```

---

## 🗂 주요 기능 상세

### 1. 🏠 메인 페이지 (`index.html`)
- 배경 **자동 재생 동영상** (소방관 예고편)
- 현재 상영 인기 영화 5편을 카드 형태로 표시
- 각 카드에 **상세보기 / 예매하기** 오버레이 버튼

### 2. 🎥 영화 목록 (`showingmoive.html`)
- 상영 중인 영화 12편 그리드 표시
- 마우스 오버 시 영화 소개 문구 및 상세보기·예매하기 버튼 오버레이

### 3. 📅 예매 (`reservation.html`)
- **3단계 순차 선택**: 영화 → 날짜 → 시간/상영관
- 날짜 선택 시 2개월 달력(2024/11, 2024/12) 제공
- 상영관 1~7관, 시간대별 슬롯 선택
- 선택 완료 시 하단 요약 테이블 표시
- 모든 선택값은 **URL Query Parameter**로 다음 페이지에 전달

### 4. 💺 좌석 선택 (`seat.html`)
- 인원 구분: **일반 / 청소년 / 경로 / 우대** (각 최대 5명)
- 좌석 배치도: A~D행 × 1~5열 (총 20석)
- 선택 인원 수 초과 시 경고 알림
- 결제 버튼 클릭 시 기존 URL 파라미터를 유지하며 `pay.html`로 이동

### 5. 💳 결제 (`pay.html`)
- URL 파라미터에서 영화명, 등급 이미지, 날짜, 상영관, 인원, 좌석 정보를 읽어 화면에 동적 렌더링
- **결제 수단 선택**: 신용카드, 엘페이, 간편결제, 휴대폰, 카카오페이, 내통장결제
- 결제 약관 마스터 체크박스 (하위 체크박스 일괄 처리)

### 6. 🍿 매점 (`food_*.html`)
- **콤보 / 팝콘 / 음료 / 간식** 4개 카테고리 탭
- 상품별 이미지, 구성, 가격 표시

### 7. 🔍 영화 추천 (`suggest.html`)
- 19편의 영화 데이터 내장
- **장르** (액션/코미디/드라마/호러), **연령 제한** (전체/12세/15세/청불), **별점**, **키워드** 복합 필터링
- 결과를 포스터 이미지 + 제목 리스트로 표시

### 8. 🎬 영화 상세 (`View_details/*.html`)
- 14편의 영화별 독립 상세 페이지
- 공통 CSS(`all.css`)로 스타일 통일

---

---

## 🚀 실행 방법

별도의 설치·빌드 과정이 필요 없습니다.

```bash
# 1. 저장소 클론
git clone https://github.com/chikchok1/Cloud_Project.git

# 2. Cloud 폴더로 이동
cd Cloud_Project/Cloud

# 3. index.html을 브라우저로 열기
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

> **참고**: 동영상 배경 자동재생 및 일부 기능은 로컬 파일 직접 열기(`file://`)보다 로컬 웹서버 환경에서 더 안정적으로 동작합니다.  
> VS Code의 **Live Server** 확장 등을 사용하는 것을 권장합니다.

---

## 📝 라이선스

본 프로젝트는 학습 목적으로 제작된 클라우드 수업 과제입니다.  
일부 이미지 및 영화 정보는 공개된 자료를 참고하였습니다.
