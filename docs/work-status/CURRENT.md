# 개인 코팡 현재 작업

> 갱신: 2026-10-02 · 현재 단계: 운영문서 기준 커밋·앱 경로 이전과 로컬 검증 진행 중.

- 작업 공간: `/Users/han/dev/projects/personal/kopang-refactored`
- 원격: [Hdev-x/kopang-refactored](https://github.com/Hdev-x/kopang-refactored) · 비공개 · 기본 브랜치 main.
- 작업/Task/Gate 정본: [WORK](./WORK.md)의 다음 앱 경로 계획. 구조·검증 기준은 [목표 구조·이전 계획](../개인-리팩터링-구조-계획.md) 6–7절. 활성 운영은 [상태 규칙](./README.md)·[Git 규칙](../git-workflow.md).
- 합의: [DECISIONS](./DECISIONS.md) · 필요한 미결: [OPEN-QUESTIONS](./OPEN-QUESTIONS.md).
- 현재 실제 앱 경로: 아직 `frontend/`, `backend/`, `ml/`. 별도 `refactor/app-paths` branch/worktree에서 세 폴더 이동과 필요한 경로 참조만 수정한다.
- 승인: 2026-10-02 11:31:22Z 사용자의 `ㄱㄱ`는 운영문서 로컬 기준 커밋→작업 branch에서 세 앱 이동·필요 경로 수정→전후 검증→로컬 커밋을 포함한다. push·PR·merge/main 병합·CI/보호 설정·기능/스타일 통합은 제외.
- 다음 행동 하나: 작성한 운영 문서만 로컬 기준 커밋으로 고정하고 별도 작업공간에서 baseline을 확보한다. 검증 차단/실패는 WORK에 사실대로 기록한다.

## 완료한 기반과 근거

| 결과 | 확인한 근거·한계 |
|---|---|
| 비공개 개인 저장소 생성·안전 이전 | 2026-10-02 이전 검사에서 원본 main의 커밋 365개·작성자 5명·tracked 파일 916개를 이력 재작성 없이 보존. 원본 develop과 main의 코드 tree가 같으며 추가 팀 merge 이력까지 보존. 원본의 untracked/ignored·로컬 환경설정은 이관하지 않음. 이력·blob·Office 내부 텍스트 비밀정보 검사에서 실제 credential/운영 덤프를 발견하지 않음. 검사는 당시 이전 범위에 대한 결과이며 미래 변경 전체를 보증하지 않음. |
| 이전 기준과 원격 | main `183600eeb3250ad61053037e3ca9e3c82dc6dd9e`, tree `e32672b909c06264b4c66137cb7279a047978362`. 이번 적용 전 GitHub의 소유자 Hdev-x·비공개·기본 main 및 같은 main SHA를 읽기 전용으로 재확인. |
| 목표 구조와 적용 근거 문서 | 구조 계획과 운영 제안 작성 완료. root README에 문서 링크, `frontend/design/README.md`에 원팀 자료와 개인 목표 구분 추가. 이번 적용에서 이전 문서 내용을 보존하고 운영 적용 상태·다음 단계만 정리. |
| 운영규칙 전체 보완 | 초기 최소 AGENTS/상태 파일에 WORK·작업 운영 정본·Git lifecycle·PR/Issue 양식을 보완. 원본→반영 위치→그대로/수정/제외와 이유는 [대조표](../WYBU-운영규칙-대조.md), 완료 Task/Gate·검증 한계는 WORK 한 곳에서 관리. HANDOFF·Worklog는 실제 필요가 없어 생성하지 않음. |

이전 감사 자료: [이전 결과](</Users/han/Documents/Codex/2026-10-02/task-2/migration-audit/migration-report.md>), [이전 검증](</Users/han/Documents/Codex/2026-10-02/task-2/migration-audit/migration-verification.json>). 최초 최소 운영 검증: [검증 기록](</Users/han/Documents/Codex/2026-10-02/task-2/operations-setup/verification.json>). 전체 보완 검증은 WORK에서 연결한다. 이 자료는 이 컴퓨터의 외부 감사 기록이며 저장소에 포함되지 않는다. 없으면 실제 Git과 관련 코드로 재확인하고 자료가 존재한다고 가정하지 않는다.

## 운영규칙 적용 당시 상태 (이전 기록)

- 개인 branch는 main, HEAD는 위 이전 기준 그대로다. branch·refs·index·Git 설정을 바꾸지 않았고 commit·push하지 않았다.
- 기존 미커밋 문서 4개를 보존했다: `README.md`, `frontend/design/README.md`, `docs/개인-리팩터링-구조-계획.md`, `docs/개인-작업맥락-운영-제안.md`.
- 초기 AGENTS/상태 파일과 README·구조 계획·운영 제안의 적용 상태를 보완했다. 추가 운영 경로는 WORK·이 폴더 README·Git 규칙·WYBU 대조표와 .github PR/Issue Markdown 양식이다. 디자인 README는 이번에도 추가 변경하지 않았다. 로컬 문서 변경은 아직 GitHub에 반영되지 않았다.
- 앱 소스·실제 폴더 배치·원본 팀 저장소·외부 팀 worklog는 수정하지 않았다. 재개 시에는 이 snapshot과 실제 dirty 상태를 다시 비교한다.
- build/lint·브라우저·API·DB·ML 실행 검증은 수행하지 않았다. remote CI/보호·merge 설정도 미확인. 다음 계획에서 환경과 기존 실패 기준부터 확인하며 현재 상태를 실행 정상으로 표시하지 않는다.

## 다음 계획에서 확인할 범위

앱별로 시작 명령·import/config·정적 자산·문서/CI 참조·ML 입출력 상대 경로를 목록화하고, 기준 확보→이전→앱별 검증→복구 방법을 정한다. 기존 구조 계획의 CSS 정리는 후보이며 실행 순서나 구체적 변경을 이번 운영 적용으로 승인한 것이 아니다. 기능·URL·디자인·DB·ML 계약 변경과 묶지 않는다. 검증 환경 관련 질문은 OPEN-QUESTIONS에서 필요한 것부터 확인한다.
