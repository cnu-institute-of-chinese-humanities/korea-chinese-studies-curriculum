# 한국 대학의 중국학 유관 학과 교과과정 데이터셋

> 한국 4년제 대학 78곳의 중국학 유관 학과·전공·트랙 94개와 그 2025학년도 교과목 4,012건, 교원 435명, 교육목표 88건을 개체–관계 구조(지식그래프)로 정리한 데이터셋

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
<!-- Zenodo 연동 후 아래 배지의 {DOI} 를 발급받은 값으로 교체 -->
<!-- [![DOI](https://zenodo.org/badge/DOI/{DOI}.svg)](https://doi.org/{DOI}) -->

## 개요

한국 대학에서 중국학이 어떤 조직 단위(학과·전공·트랙)로 존재하고, 각 단위가 어떤 교과목을 어떤 구성으로 개설하며, 어떤 전공 배경의 교원이 무엇을 가르치는지를 한눈에 볼 수 있도록 만든 자료입니다. 대학·캠퍼스·단과대학·학부·학과·전공·트랙·교육목표·교과목·교원을 **개체(노드)**로, 소속·개설·담당 등을 **관계(엣지)**로 표현합니다. 교과과정 비교, 교육과정 네트워크 분석, 지역별 분포 지도, 교과목 개요 텍스트 분석 등에 쓸 수 있습니다.

- **대상 교육과정**: 2025학년도 (단년도)
- **자료 유형**: 조직·교과목 메타데이터, 교육목표·교과목 개요 원문, 개체 간 관계(엣지리스트), 캠퍼스 좌표
- **규모**: 개체 4,894건 · 관계 5,393건 (시트 11개, 10,287행)
- **언어**: 한국어 (일부 교과목 개요에 중국어 병기)
- **커버리지**: 78개 대학 전부에서 교과목 수집. 개설 단위 94개 중 91개에 교과목 연결 (나머지 3개는 하위 전공·트랙에 교과목이 붙어 있음)

## 데이터 구성

| 경로 | 내용 | 형식 |
|---|---|---|
| `data/raw/korea_chinese_studies_curriculum_2025.xlsx` | 원본 (시트 11개). **수정하지 않음** | xlsx |
| `data/processed/csv/*.csv` | 개체 10종 + 관계 1종 | CSV (UTF-8, LF) |
| `data/processed/json/*.json` | 같은 내용. 다중값은 배열, 결측은 null | JSON |
| `data/processed/graph.json` | 노드 4,894 · 엣지 5,393 통합 그래프 | JSON |
| `data/processed/campus.geojson` | 캠퍼스 81개 지점 | GeoJSON |
| `data/processed/_columns.json` | 열 정의·결측률 (기계 판독용) | JSON |

| 파일 | 행 | 내용 |
|---|---:|---|
| `university` | 78 | 대학 (설립 주체, 인가·개교 연도) |
| `campus` | 81 | 캠퍼스 (권역, 위경도) |
| `college` · `faculty` | 80 · 26 | 단과대학 · 학부 |
| `department` · `major` · `track` | 58 · 33 · 3 | 학과 · 전공 · 트랙 (계열, 개설 연도, 홈페이지) |
| `edugoal` | 88 | 교육목표 원문과 출처 |
| `course` | 4,012 | 교과목 (학년·학기·학점, 이수 구분, 분류, 개요, 출처) |
| `professor` | 435 | 교원 (전공 대분류·세부 전공). **성명은 익명화** |
| `edge` | 5,393 | 관계: `offers` 4,012 · `teaches` 576 · `belongsTo` 435 · `hasPart` 282 · `hasContent` 88 |

각 변수의 정의·자료형·결측·주의 사항은 **[`docs/codebook.md`](docs/codebook.md)** 를 참조하십시오.
수집 절차, 익명화 처리, 제3자 저작물의 권리 상태는 **[`docs/provenance.md`](docs/provenance.md)** 에 기술되어 있습니다.

### 쓰기 전에 꼭 볼 것

- **교과목이 붙는 단위가 대학마다 다릅니다.** 학과로만 세면 서강대·한신대·호서대가 0으로 잡힙니다. `hasPart` 관계로 전공·트랙까지 내려가십시오.
- **`grade`·`semester`·`credit`은 자료형이 섞여 있습니다.** `3~4`·`계절`·`P` 같은 값이 있어 그냥 평균을 내면 오류가 나거나 조용히 빠집니다.
- **교원 성명은 전원 `○○○`입니다.** 개체 구분은 `id`(`Prof001`)로 하십시오.
- **교육목표(`content`)와 교과목 개요(`description`)는 각 대학의 저작물**입니다. 이 저장소의 라이선스가 적용되지 않습니다.

## 재현 방법

`data/raw/` 에서 `data/processed/` 를 다시 생성하려면:

```bash
# Python 3.9 이상, openpyxl 필요
pip install openpyxl
python scripts/preprocess.py
```

스크립트는 교원 이름이 가려지지 않은 값이 하나라도 있으면 실행을 중단합니다.

## 인용

이 데이터를 사용하실 경우 다음과 같이 인용해 주십시오.

> 중국인문연구소. (2026). *한국 대학의 중국학 유관 학과 교과과정 데이터셋* (Version 1.0.0) [Data set]. https://github.com/cnu-institute-of-chinese-humanities/korea-chinese-studies-curriculum

<!-- Zenodo DOI 발급 후 위 URL을 https://doi.org/{DOI} 로 교체 -->

GitHub 우측 상단의 **Cite this repository** 버튼으로 BibTeX·APA 형식을 받으실 수 있습니다.
(형식 정의는 [`CITATION.cff`](CITATION.cff) 에 있습니다.)

## 라이선스

- **데이터** (`data/`, `docs/`, `figures/`): [CC BY 4.0](LICENSE) — 출처를 밝히면 자유롭게 사용·재배포·변형 가능
- **코드** (`scripts/`): [MIT](scripts/LICENSE)
- **예외**: 교육목표 원문(`edugoal.content`)과 교과목 개요(`course.description`, `course.previousDescription`)는 각 대학이 작성한 **제3자 저작물**로, 출처를 밝히고 인용한 것입니다. 위 라이선스가 적용되지 않으며 권리는 각 대학에 있습니다. 자세한 사항은 [`docs/provenance.md`](docs/provenance.md)의 '제3자 자료 및 권리 상태'를 보십시오.

## 버전 이력

주요 변경 사항은 [`CHANGELOG.md`](CHANGELOG.md) 를 참조하십시오.
과거 버전은 [Releases](../../releases) 에서 내려받으실 수 있으며, **기존 릴리스는 삭제되지 않습니다.**

## 문의·이의제기

- 기관: 중국인문연구소
- 이메일: instituteofchinesehumanitie@gmail.com
- 오류 제보·문의: [Issues](../../issues)
- **수록 내용에 대한 이의제기·삭제 요청**: 자료의 권리자(대학·학과)나 교원 본인은 위 이메일 또는 Issues로 연락해 주십시오. 사실 확인 뒤 다음 릴리스에서 해당 항목을 제거하고 변경 이력에 기록합니다.

## 관련 저장소

- [`data-guidelines`](https://github.com/cnu-institute-of-chinese-humanities/data-guidelines) — 연구소의 데이터 공개 지침, 익명화 기준, 공개 전 체크리스트
- [`dataset-template`](https://github.com/cnu-institute-of-chinese-humanities/dataset-template) — 이 저장소가 따른 데이터셋 템플릿

## 관련 논문

(준비 중)
