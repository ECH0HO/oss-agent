# ossweek9 - 박스오피스 1위 조회

## 무엇을 하는 코드인가
영화진흥위원회(KOBIS) 오픈 API로 특정 날짜의 일별 박스오피스 1위 영화 제목을 가져와 출력합니다.

## 설치
```
pip install -r requirements.txt
```
그리고 같은 폴더에 `secret.py`를 만들고 KOBIS API 키를 넣습니다.
```python
API_KEY = "발급받은_키"
```

## 실행
```
python main.py
```
조회 날짜를 바꾸려면 `main.py`의 `"20260824"`를 원하는 8자리 날짜로 수정하세요.
