작성: Claude Code / 확인: (이름)

# boxoffice — KOBIS 박스오피스 조회 스킬

## 하는 일
날짜를 주고 그날의 1위 영화나 특정 영화의 관객 수를 물으면, 영화진흥위원회(KOBIS) 일별 박스오피스에서 찾아 알려 준다.

## 들어 있는 파일
- .claude/skills/boxoffice/SKILL.md
- .claude/skills/boxoffice/scripts/boxoffice.py
- .claude/skills/boxoffice/LICENSE

## 필요한 것
- week12 폴더의 `tools.py` (KOBIS 요청 함수)와 `secret.py` (API 키)
- Python 3와 `requests` 패키지 (`pip install requests`)

## 설치
1. `boxoffice` 폴더를 `week12/.claude/skills/` 아래에 둔다.
2. week12 폴더에서 Claude Code 를 실행한다.
3. "20261114 박스오피스 1위 영화는?"처럼 묻는다. 직접 실행할 때는 아래 명령을 쓴다.

```
python .claude/skills/boxoffice/scripts/boxoffice.py rank 20261114
python .claude/skills/boxoffice/scripts/boxoffice.py audience 20261114 "영화 제목"
```

## 바깥으로 요청하는 곳
- `https://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json`

## 키
- 키는 week12 폴더의 `secret.py` 에 `API_KEY` 로 둔다.
- `secret.py` 는 `.gitignore` 에 들어 있다. 각자 KOBIS 에서 키를 받아 만든다.

## 권한
- `allowed-tools`가 기재되어 있지 않다.
- 스크립트를 실행할 때마다 Claude Code 가 Bash(python) 실행 허락을 묻는다.

## 라이선스
- MIT 라이선스이다.