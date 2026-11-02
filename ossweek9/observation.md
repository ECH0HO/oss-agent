# Observation

## 1. Claude가 사용한 도구
bash - average_pandas.py
bash - average_plain.py
bash - check.py
bash - scores.csv
## 2. 샘플 파일 설명과 실제 코드 일치 여부
샘플 파일 4개 모두 Claude의 설명이 실제 코드와 일치했다(4개 모두 O)
## 3. tools.py 주석 유무에 따른 AI 설명 비교
두 파일의 코드는 같다. 차이는 docstring(주석)이 있느냐 없느냐뿐이다. 두 경우 모두 "이 파일만 읽고, 각 함수가 무엇을 받고 무엇을 돌려주는지 설명해 줘. 다른 파일은 열지 말고, 파일은 고치지 마"라는 같은 질문을 했다.

## 주석이 있을 때 (tools.py)
Claude는 get_boxoffice_rank_1(date) 함수가 `"20260824"` 같은 8자리 날짜 문자열을 받는다고 설명했다. 돌려주는 값은 그날 박스오피스 1위 영화 제목이며, 예로 `"오디세이"`를 들었다. 이 내용은 docstring에 적힌 "받는 것 / 돌려주는 것" 문장을 거의 그대로 옮긴 것이다. 동작 순서(KOBIS API 요청 → dailyBoxOfficeList 추출 → 첫 항목의 movieNm 반환)와 예외 처리가 없다는 점도 함께 짚었다. 설명이 짧고 단정적이었으며, 추측하는 표현은 없었다.

## 주석이 없을 때 (tools_nodoc.py)
Claude는 같은 함수를 코드만 보고 설명했다. 받는 값 date에 대해서는 "KOBIS API의 targetDt로 그대로 넘어가며, KOBIS API는 보통 YYYYMMDD 형식의 문자열을 받는다"고 했다. 즉 코드가 아니라 API에 대한 배경지식으로 형식을 추론했고, "코드에는 형식을 검사하는 부분이 없다"는 단서도 달았다. 돌려주는 값은 1위 영화 제목(movieNm)이라고 맞게 설명했다. 다만 구체적인 예시를 들지 못하고 `"어떤 영화 제목"`이라고만 썼다. 대신 예외가 나는 경우(네트워크 오류, KeyError, IndexError)와 HTTP 상태 코드를 확인하지 않는 점을 더 자세히 설명했고, docstring이 없다는 사실도 지적했다.

## 비교 및 차이점
두 경우 모두 함수가 무엇을 받고 무엇을 돌려주는지는 정확하게 설명했다. 코드가 짧고 변수 이름(targetDt, movieNm)이 의미를 잘 드러내서 주석이 없어도 핵심은 파악할 수 있었다.
## 4. README.md에서 발견한 오류
- secret.py가 .gitignore에 등록되어 저장소에 올라가지 않는다는 점이 적혀 있지 않다.
- 날짜에 데이터가 없거나 API 키가 틀리면 KeyError나 IndexError로 프로그램이 멈춘다는 점이 빠져 있다.