# notes_before.md - ossweek9/tools.py 분석

## 파일 개요

`ossweek9/tools.py`는 **영화진흥위원회(KOBIS) 오픈 API**를 이용해 박스오피스 정보를 가져오는 도구 모음이다.

- 사용 라이브러리: `requests` (HTTP 요청)
- API 키: `secret.py`의 `API_KEY`를 import 해서 사용
- 호출 주소 (`BASE_URL`): KOBIS 일별 박스오피스 조회 API
  `https://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json`

## 함수 목록

현재 파일에는 함수가 **1개** 있다.

### `get_boxoffice_rank_1(date)`

특정 날짜의 일별 박스오피스 **1위 영화 제목**을 알려준다.

| 구분 | 내용 |
|------|------|
| 입력 | `date` (문자열) - 8자리 날짜, 예: `"20260824"` |
| 출력 | (문자열) 1위 영화 제목, 예: `"오디세이"` |

**동작 순서**

1. `key`(API 키)와 `targetDt`(조회 날짜)를 파라미터로 만든다.
2. `requests.get()`으로 KOBIS API에 요청한다. (타임아웃 10초)
3. 응답을 JSON으로 변환한다.
4. `data["boxOfficeResult"]["dailyBoxOfficeList"]`에서 영화 목록을 꺼낸다.
5. 목록의 첫 번째 항목(`movies[0]`)의 `movieNm`(영화 제목)을 돌려준다.

## 참고 / 한계

- 1위 영화의 **제목만** 돌려준다. 관객 수, 매출액, 2위 이하 순위 등은 제공하지 않는다.
- 예외 처리가 없다. 날짜 형식이 틀리거나, 네트워크 오류가 나거나, 결과 목록이 비어 있으면 에러가 발생할 수 있다.
- `secret.py` 파일(API 키)이 없으면 import 단계에서 실패한다.
