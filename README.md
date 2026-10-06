# GradeBook — Python 모듈 · 패키지 실습 (6주차)

학생 성적(평균, 학점)을 계산하는 같은 프로그램을 세 가지 구조로 작성하며  
**하나의 파일 → 모듈 분리 → 패키지 구조**로 확장하는 과정을 연습한 저장소입니다.

---

## 폴더 구조

```
weak06/
├─ gradebook.py            # 실습 1: 하나의 파일
├─ other_file.py           # __name__ 확인용 (import gradebook)
├─ project_root/           # 실습 2: 모듈 분리
│  ├─ main.py              #   실행 시작점
│  ├─ models.py            #   Student, GradeBook 클래스
│  └─ utils.py             #   mean, letter_grade 함수
└─ project_root_pkg/       # 실습 3: 패키지 구조
   ├─ gradebook/           #   패키지 루트
   │  ├─ __init__.py
   │  ├─ __main__.py       #   python -m gradebook 진입점
   │  ├─ cli.py            #   명령행 인터페이스
   │  ├─ models.py
   │  ├─ utils.py
   │  └─ io/
   │     ├─ __init__.py
   │     └─ csvio.py       #   CSV 입출력
   ├─ tests/
   │  └─ test_utils.py     #   unittest
   └─ students.csv         #   예제 데이터
```

---

## 실행 방법

### 실습 1 — 하나의 파일
```bash
python gradebook.py
```
```
전체 반 평균 점수: 80.0
Alice - 평균: 89.0, 학점: B
Bob - 평균: 71.0, 학점: C
```

`python other_file.py` 를 실행하면 아무것도 출력되지 않습니다.  
`import` 될 때는 `__name__` 이 `"__main__"` 이 아니므로 `main()` 이 실행되지 않기 때문입니다.

### 실습 2 — 모듈 분리
```bash
cd project_root
python main.py
```
같은 폴더 안에서는 파일명(확장자 제외)을 모듈 이름으로 바로 `import` 할 수 있습니다.

### 실습 3 — 패키지 구조
```bash
cd project_root_pkg
python -m gradebook
```
```
📘 GradeBook CLI 실행 중...

전체 반 평균 점수: 80.67

Alice: 평균=89.0, 학점=B
Bob: 평균=71.0, 학점=C
Charlie: 평균=87.3, 학점=B
Diana: 평균=95.0, 학점=A
Ethan: 평균=61.0, 학점=D
```
`students.csv` 가 없으면 기본 데이터(Alice, Bob)로 실행됩니다.

### 테스트
```bash
cd project_root_pkg
python -m unittest discover -s tests
```
```
..
----------------------------------------------------------------------
Ran 2 tests in 0.000s

OK
```

---

## 학점 기준

| 평균 | 학점 |
|---|---|
| 90 이상 | A |
| 80 이상 | B |
| 70 이상 | C |
| 60 이상 | D |
| 60 미만 | F |

---

## 개발 환경
- Python 3.13
- 외부 라이브러리 없음 (표준 라이브러리 `csv`, `unittest` 만 사용)
