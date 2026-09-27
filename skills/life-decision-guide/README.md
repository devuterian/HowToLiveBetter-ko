# 인생 결정 skill(life-decision-guide)

AI 어시스턴트가 《가성비 인생 가이드》에 따라 구체적인 질문에 답하게 한다. 해야 하나, 할 만한가, 어떻게 고르나, 일이 터지면 뭘 먼저 하나, 어떤 돈을 받을 수 있나, 이렇게 하면 불법인가.

하는 일은 딱 하나다. **먼저 관련 항목을 본문에서 찾아낸 뒤, 책의 계산 방식대로 순서를 매겨 답한다.** 항목마다 제몇 장 몇 번에서 나왔는지 밝힌다. 못 찾으면 못 찾았다고 하고, 기억에 기대 숫자를 지어내지 않는다.

규칙은 전부 [SKILL.md](SKILL.md)에 있다. 두 도구가 같은 파일 하나를 함께 쓰고, 두 벌을 따로 관리하지 않는다.

## Claude Code에 설치하기

이 저장소 안에서 Claude Code를 열면 설치할 필요가 없다. `.claude/skills/life-decision-guide/`가 이미 이 규칙을 가리키고 있다.

어느 디렉터리에서든 쓰고 싶다면 개인 skill 디렉터리로 복사한다.

```bash
mkdir -p ~/.claude/skills/life-decision-guide && curl -fsSL -o ~/.claude/skills/life-decision-guide/SKILL.md "https://raw.githubusercontent.com/eternity4719/HowToLiveBetter/main/skills/life-decision-guide/SKILL.md"
```

그다음에는 "매일 출퇴근에 두 시간 쓰는 게 할 만한가", "친구가 보증을 서 달라는데 서명할까" 하고 그냥 물으면 작동한다. "life-decision-guide로 답해 줘"라고 명시적으로 말해도 된다.

## Codex에 설치하기

이 저장소 안에서 Codex를 열면 설치할 필요가 없다. 루트의 `AGENTS.md`가 이미 이걸 가리키고 있다.

어느 디렉터리에서든 쓰고 싶다면 Codex의 사용자 정의 프롬프트 디렉터리에 넣고, 이후 `/life-decision-guide`로 호출한다.

```bash
mkdir -p ~/.codex/prompts && curl -fsSL -o ~/.codex/prompts/life-decision-guide.md "https://raw.githubusercontent.com/eternity4719/HowToLiveBetter/main/skills/life-decision-guide/SKILL.md"
```

매번 슬래시 명령을 치지 않고 모든 세션에서 적용되게 하려면 `~/.codex/AGENTS.md`에 이 한 줄을 넣는다.

```markdown
인생 결정에 관한 질문(해야 하나, 할 만한가, 어떻게 고르나, 뭘 받을 수 있나, 불법인가)에 답할 때는 ~/.codex/prompts/life-decision-guide.md 대로 한다.
```

## 본문은 어디서 가져오나

로컬에 이 저장소가 있으면 로컬의 `book/`을 읽는다. 없으면 그때 가져온다.

```bash
git clone --depth 1 https://github.com/eternity4719/HowToLiveBetter.git "${TMPDIR:-/tmp}/hltb"
```

책 전체가 1.3 MB라서 얕은 클론 한 번에 몇 초면 된다. 네트워크로 못 가져오면 못 가져왔다고 사실대로 말하고, 본문을 다른 것으로 대신하지 않는다.

## 수정할 때 알아 둘 것

SKILL.md에는 본문을 따라 바뀌는 목록이나 수치를 하나도 남기지 않는다. 장 목록은 README의 "이 책이 답하려는 질문" 표를 읽고, 가성비 등급 계산법은 `index.html`의 `COST_W`와 `e.ratio` 두 줄을 읽는다. 그래서 장을 늘리거나 줄여도, 등급 규칙을 바꿔도 이 디렉터리는 건드릴 필요가 없다.
