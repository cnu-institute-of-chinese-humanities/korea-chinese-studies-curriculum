# 한국 대학의 중국학 유관 학과 교과과정 데이터셋

> 한국 4년제 대학 78곳의 중국학 유관 학과·전공·트랙 94개와 그 2025학년도 교과목 4,012건, 교원 435명, 교육목표 88건을 개체–관계 구조(지식그래프)로 정리한 데이터셋

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
<!-- Zenodo 연동 후 아래 배지의 {DOI} 를 발급받은 값으로 교체 -->
<!-- [![DOI](https://zenodo.org/badge/DOI/{DOI}.svg)](https://doi.org/{DOI}) -->

## 소개 🔖

한국의 4년제 대학 78곳에 있는 중국학 유관 학과·전공·트랙 94개가 2025학년도에 어떤 교과목을 개설하고, 어떤 전공 배경의 교원이 무엇을 가르치며, 각 조직이 어떤 교육목표를 내걸고 있는지를 한자리에 모은 자료입니다.
대학·캠퍼스·단과대학·학과·전공·교과목·교원을 **개체**로, 소속·개설·담당을 **관계**로 엮은 지식그래프 형태라서, 표로도 볼 수 있고 연결망으로도 볼 수 있습니다.
교과과정 비교, 교육과정 연결망 분석, 지역별 분포 지도, 교과목 개요 텍스트 분석에 바로 쓸 수 있도록 CSV·JSON·그래프·GeoJSON 네 가지 형식으로 제공합니다.
교원 성명은 익명화되어 있으며, 교육목표와 교과목 개요 원문은 각 대학의 문장을 출처를 밝혀 인용한 것입니다.

| 개체 4,894건 | 관계 5,393건 | 대학 78 · 개설 단위 94 | 교과목 4,012 · 교원 435 · 교육목표 88 |
|---|---|---|---|

## 저자 👨‍🏫

- 정선한 · 홍승현 · 유인태 — 전남대학교 중어중문학과
- 문의: 중국인문연구소 (Institute of Chinese Humanities), instituteofchinesehumanitie@gmail.com

## 폴더 설명 📁

- `data/raw/` — 원본 엑셀 파일(시트 11개). 수정하지 않습니다.
- `data/processed/` — 원본에서 만든 분석용 파일. `csv/`는 엑셀·SPSS·R용, `json/`은 프로그래밍용, `graph.json`은 Gephi·networkx 등 연결망 도구용, `campus.geojson`은 지도용입니다.
- `docs/` — 변수 정의서(`codebook.md`)와 수집·권리 내역(`provenance.md`). **데이터를 쓰기 전에 코드북을 먼저 읽어 주십시오.**
- `scripts/` — 원본에서 `data/processed/`를 다시 만드는 전처리 스크립트
- `figures/` — 시각화 결과 (준비 중)

## 논문 📝

이 데이터셋의 편찬 과정과 분석 결과는 아래 논문에 실려 있습니다. 데이터를 인용하실 때는 이 논문을 함께 인용해 주십시오.

- 정선한·홍승현·유인태 (2026). 「지식그래프로 보는 한국 대학의 중국 유관 교육 — 2025학년도 교육과정 시맨틱 데이터 편찬과 분석」. 『중국인문과학』 93, 279–325. https://doi.org/10.35955/JCH.2026.08.93.279
- Jeong, S., Hong, S., & Ryu, I. T. (2026). China-related education at Korean universities through a knowledge graph: Compilation and analysis of semantic curriculum data for the 2025 academic year. *Journal of Chinese Humanities*, 93, 279–325. https://doi.org/10.35955/JCH.2026.08.93.279

---

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

> 정선한, 홍승현, 유인태. (2026). *한국 대학의 중국학 유관 학과 교과과정 데이터셋* (Version 1.0.0) [Data set]. 중국인문연구소. https://github.com/cnu-institute-of-chinese-humanities/korea-chinese-studies-curriculum

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

