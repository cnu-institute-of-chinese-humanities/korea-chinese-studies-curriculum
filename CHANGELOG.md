# 변경 이력

형식은 [Keep a Changelog](https://keepachangelog.com/ko/1.1.0/)를,
버전 번호는 [유의적 버전](https://semver.org/lang/ko/)을 따릅니다.

데이터셋에서 각 자리의 의미는 다음과 같습니다.

- **MAJOR** (`2.0.0`) — 변수 삭제·이름 변경, 표본 구성 변경 등 **기존 분석 코드가 깨지는** 변경
- **MINOR** (`1.1.0`) — 관측치·변수 추가처럼 **하위 호환되는** 확장
- **PATCH** (`1.0.1`) — 오탈자·인코딩·개별 값 오류 수정

## [Unreleased]

## [1.0.0] - 2026-09-03

### 추가됨
- 최초 공개. 한국 4년제 대학 78곳의 중국학 유관 학과·전공·트랙 94개, 2025학년도 교과목 4,012건, 교원 435명, 교육목표 88건, 관계 5,393건
- 원본 xlsx(`data/raw/`)와 전처리 산출물(`data/processed/`: CSV·JSON·graph.json·campus.geojson·_columns.json)
- 코드북(`docs/codebook.md`), 수집 내역·권리 상태(`docs/provenance.md`)
- 전처리 스크립트(`scripts/preprocess.py`). 교원 이름이 가려지지 않은 값이 있으면 실행을 중단하는 검사 포함

### 익명화
- 교원 성명 435건과 관계 데이터의 교원 이름 1,011건을 성씨 없이 `○○○`으로 통일. 처리 전 파일은 저장소에 포함되지 않음
