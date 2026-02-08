# 🏥 RxHCC — 보험 청구 무결성 AI 검증 시스템

> 보험 청구(Claims)의 진단코드(ICD), 약물코드(NDC), 위험조정계수(HCC)의
> 정합성을 AI 규칙 엔진으로 실시간 검증하는 시스템

[![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat&logo=streamlit&logoColor=white)](https://streamlit.io)
[![Python](https://img.shields.io/badge/Python-3.9+-blue?style=flat&logo=python)](https://python.org)
[![LangGraph](https://img.shields.io/badge/LangGraph-Enabled-green?style=flat)](https://langchain-ai.github.io/langgraph/)

## 🎯 주요 기능

| 기능 | 설명 |
|------|------|
| 🔍 **실시간 검사** | ICD/NDC 코드를 입력하여 즉시 검증 |
| 📋 **배치 데모** | 사전 시나리오 및 합성 데이터 대량 검증 |
| 📊 **데이터 미리보기** | 검증 결과 필터링, 상세 조회, CSV 다운로드 |
| 📖 **규칙 사전** | 등록된 모든 검증 규칙 조회 |
| 📈 **분석 대시보드** | 심각도 분포, Provider별 위반, 월별 추이 |

## 🏗️ 아키텍처

```
사용자 입력
    ↓
[Streamlit UI]
    ↓
[LangGraph Workflow]
    ┌───────────────────┐
    │  1. Parse Claim   │
    │  2. Rule Engine   │ ← engine/rules.py (중앙 규칙)
    │  3. Risk Scoring  │
    │  4. Escalation    │
    └───────────────────┘
    ↓
[검증 결과 + 리스크 등급]
```

## 🚀 빠른 시작

```bash
# 클론
git clone https://github.com/sechan9999/RxHCC.git
cd RxHCC

# 의존성 설치
pip install -r requirements.txt

# 앱 실행
streamlit run app/integrity_app.py
```

## 📋 검증 규칙

### 1. ICD-NDC 매핑 검증
진단코드에 맞는 약물이 처방되었는지 확인

### 2. ICD 코드 충돌 감지
- E10(1형) + E11(2형) 동시 진단 → **CRITICAL**
- E11 + Z86.39(당뇨 과거력) 동시 → **WARNING**

### 3. GLP-1 오남용 감지
- 적응증(E11/E66) 없이 GLP-1 처방 → **CRITICAL**
- 1형 당뇨(E10)에 GLP-1 → **CRITICAL**

### 4. HCC Upcoding 감지
- HCC 코드를 뒷받침하는 ICD 코드 부족 → **CRITICAL**

## 🧪 테스트

```bash
pytest tests/test_rules.py -v
```

## 📁 프로젝트 구조

```
RxHCC/
├── app/
│   └── integrity_app.py        # Streamlit 대시보드
├── engine/
│   ├── rules.py                # 규칙 엔진 (핵심)
│   ├── langgraph_integrity.py  # LangGraph 워크플로우
│   └── sagemaker_replication.py # 데이터 생성 & 배치 검증
├── data/
│   └── scenarios.json          # 시나리오 데이터 (예시)
├── tests/
│   └── test_rules.py           # 유닛 테스트
└── requirements.txt
```

## 🛣️ 로드맵

- [ ] OpenAI/Claude API 연동하여 자연어 검증 리포트 생성
- [ ] 실제 CMS HCC 매핑 테이블 통합
- [ ] SageMaker Processing Job 실제 구현
- [ ] 사용자 인증 및 감사 로그
- [ ] Docker 컨테이너화 및 배포

## 📜 라이선스

MIT License
