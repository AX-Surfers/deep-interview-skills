# deep-interview 스킬 모음

Claude에게 애매한 아이디어를 던지면, 한 번에 질문 하나씩 던지면서 "진짜 뭘 원하는지" 명확하게 만들어주는 스킬입니다. 질문이 다 끝나면 정리된 기획서(스펙 문서)를 파일로 남겨줍니다. 코드부터 짜기 전에, 요구사항부터 확실히 하고 싶을 때 씁니다.

## 이게 뭐하는 건가요?

"검색 기능 넣고 싶어" 같은 막연한 요청을 그대로 던지면 Claude가 엉뚱한 걸 만들 수 있습니다. 이 스킬을 쓰면:

1. Claude가 한 번에 질문 하나씩 물어봄 (여러 개 동시에 안 물어봄)
2. 답할 때마다 "지금 얼마나 명확해졌는지" 점수로 보여줌
3. 충분히 명확해지면 질문을 멈추고, 정리된 문서(기획서)를 파일로 저장
4. 그 다음 "지금 바로 만들지 / 계획서만 남길지" 물어봄

## 두 가지 버전, 뭘 써야 하나요?

| | deep-interview (정식) | deep-interview-lite (경량) |
|---|---|---|
| 언제 쓰나 | 기능이 여러 개 엮인 큰 작업 (예: 접수 시스템 + 검토 화면 + 리포트 export) | 결과물 하나 짜리 간단한 작업 (예: 검색 기능 하나 추가) |
| 질문 강도 | 더 꼼꼼함, 항목별로 따로 점검 | 가볍고 빠름 |
| 추천 대상 | 큰 프로젝트, 여러 기능을 한 번에 기획할 때 | 대부분의 일상적인 요청 |

뭘 써야 할지 모르겠으면 **deep-interview-lite**부터 써보세요. 더 간단하고 빠릅니다.

## 설치 방법 (컴퓨터에 처음 설치하는 분들 기준)

### 1단계. 터미널 앱 열기

- **Mac**: 화면 오른쪽 위 돋보기(Spotlight) 클릭 → "터미널" 입력 → Enter
- 까만 화면이 뜨면 성공입니다.

### 2단계. 아래 명령어를 순서대로 복사해서 터미널에 붙여넣고 Enter

한 줄씩 복사 → 터미널에 붙여넣기(Cmd+V) → Enter, 이걸 5번 반복하면 됩니다.

```bash
git clone https://github.com/AX-Surfers/deep-interview-skills.git
cd deep-interview-skills
mkdir -p ~/.claude/skills
cp -r deep-interview ~/.claude/skills/deep-interview
cp -r deep-interview-lite ~/.claude/skills/deep-interview-lite
```

이 명령어들이 하는 일:
1. 이 저장소를 내 컴퓨터로 다운로드
2. 다운로드한 폴더로 이동
3. Claude Code가 스킬을 찾는 폴더가 없으면 새로 만들기
4. 두 스킬을 그 폴더 안에 복사해서 넣기

### 3단계. 설치됐는지 확인

Claude Code를 새로 켜고(이미 켜져 있었다면 껐다 다시 켜기), 대화창에 아래처럼 슬래시(`/`)를 입력해보세요.

```
/deep-interview
```

목록에 `deep-interview`, `deep-interview-lite`가 뜨면 설치 성공입니다.

## 사용법

대화창에 이렇게 입력하면 시작됩니다:

```
/deep-interview 할인쿠폰 기능 만들고 싶어
```

또는 간단한 작업이면:

```
/deep-interview-lite 검색 기능 추가하고 싶어
```

그러면 Claude가 질문을 하나씩 던집니다. 편하게 아는 대로 답하면 됩니다. 질문이 끝나면 자동으로 기획서 파일을 만들어주고, "지금 바로 구현할지 / 계획만 남길지" 물어봅니다.

## 자주 묻는 질문

**Q. 명령어 쳤는데 "git: command not found" 라고 떠요.**
A. Mac에 git이 아직 안 깔려 있는 경우입니다. 터미널에 `git`이라고만 쳐보세요. Xcode Command Line Tools 설치 창이 뜨면 "설치" 눌러서 진행한 뒤, 위 2단계 명령어를 다시 실행하면 됩니다.

**Q. 이미 설치했는데 또 설치해도 되나요?**
A. 네, 덮어써질 뿐 문제 없습니다.

**Q. 스킬을 지우고 싶어요.**
A. 터미널에 아래처럼 입력하면 삭제됩니다.
```bash
rm -rf ~/.claude/skills/deep-interview ~/.claude/skills/deep-interview-lite
```
