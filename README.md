# 한능검 빈칸 훈련

한국사능력검정시험 심화 제71~80회 기출로 만든 빈칸 · O/X 훈련 앱입니다. 세법 빈칸 훈련(tax-cloze)과 같은 틀을 씁니다.

## 폴더

| 폴더 | 내용 |
|---|---|
| `app/` | 배포할 앱 전체 (`index.html`, `data/*.js`, `icons/`, `sw.js`, `manifest.webmanifest`) |
| `exams/` | 국사편찬위원회에서 받은 원본 문제지 · 정답표 PDF (`71_q.pdf`, `71_a.pdf` …) |
| `work/cards/71.txt` … `80.txt` | **카드 원본.** 고칠 때는 여기를 고칩니다 |
| `work/q71.txt` … | 문제지에서 뽑은 문항 · 선지 · 정답 (카드 작성용 참고) |
| `tools/` | 변환 스크립트 |
| `ref/` | 원래 세법 앱 (틀을 가져온 곳) |

## 카드 고치기 · 추가하기

`work/cards/<회차>.txt` 한 줄이 카드 한 장입니다. 칸은 `|` 로 나눕니다.

```
문항|단원|세부|함정|빈칸앞|정답|빈칸뒤|헷갈리는답|이유|종류|시험지단어|같은답|함정단어|시험지문장|메모
```

- 단원 id는 `tools/build.py` 위쪽 `SUBJECTS` 에 있습니다 (예: `gr_ext` = 고려 대외 관계).
- 종류: `O` 정답 선지 · `X` 옳지 않은 선지 · `L` 자료 속 단서.
- 같은 단원에서 정답이 같은 카드는 자동으로 '기출 N회'로 묶입니다.

고친 뒤 다시 만들기:

```
python -I tools/build.py work app
node tools/check_pairs.js app
```

헷갈리는 짝은 `app/data/pairs.js`, 용어 풀이 · 단원 배경은 `app/data/glossary.js` 를 직접 고칩니다.

## 로컬에서 보기

```
python -m http.server 8765 --directory app
```

브라우저에서 http://localhost:8765 를 엽니다.

## 배포 (GitHub Pages)

`app/` 폴더 내용을 새 저장소(예: `history-cloze`)에 올리고 Pages를 켜면 됩니다. 앱 안의 설치 안내 주소는 `https://dmswhd5-pixel.github.io/history-cloze/` 로 되어 있으니, 저장소 이름이 다르면 `tools/adapt_app.py` 의 `APP_URL` 을 바꾸고 다시 만드세요. 학습 기록은 `hancloze:` 로 시작하는 키로 저장되어 세법 앱 기록과 섞이지 않습니다.

## 저작권

문항 · 선지의 저작권은 국사편찬위원회에 있습니다. 개인 학습용으로 쓰고, 공개 배포할 때는 국사편찬위원회 시험자료실 안내를 확인하세요.
