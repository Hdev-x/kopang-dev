# 개인 코팡 현재 작업

> 갱신: 2026-10-02 · 현재 단계: 앱·운영문서 내용과 검증 정리 완료. Git 전달 상태는 PR/Git 실제 기록에서 확인.

- 개인 primary: `/Users/han/dev/projects/personal/kopang-refactored` (`main`, 앱·운영문서 결과 관리; 현재 HEAD/upstream은 Git에서 확인).
- 이번 결과 작업공간: `/Users/han/dev/worktrees/kopang-refactored/refactor/app-paths` (`refactor/app-paths`). 이전 결과와 필요한 의존성을 이 worktree에 보존한다. PR/merge와 현재 commit·branch 관계는 Git/GitHub에서 확인한다.
- 원격: [Hdev-x/kopang-refactored](https://github.com/Hdev-x/kopang-refactored) · 비공개 · 기본 브랜치 main.
- 작업/Task/Gate 정본: [WORK](./WORK.md)의 앱 경로 이전 결과와 GitHub 전달 내용 Gate. 구조·검증 기준은 [목표 구조·이전 계획](../개인-리팩터링-구조-계획.md) 6–7절. 활성 운영은 [상태 규칙](./README.md)·[Git 규칙](../git-workflow.md).
- 합의: [DECISIONS](./DECISIONS.md) · 필요한 미결: [OPEN-QUESTIONS](./OPEN-QUESTIONS.md).
- 현재 실제 앱 경로: `apps/web/`, `apps/backend/`, `apps/ml/`. 별도 `refactor/app-paths` branch/worktree에서 이동과 필수 경로 수정·전후 검증을 완료했다. 프론트 내부 경계·반응형 통합은 후속 범위다.
- 앱 이전 당시 승인: 2026-10-02 11:31:22Z 사용자의 `ㄱㄱ`는 운영문서 로컬 기준 커밋→작업 branch에서 세 앱 이동·필요 경로 수정→전후 검증→로컬 커밋을 포함한다. push·PR·merge/main 병합·CI/보호 설정·기능/스타일 통합은 제외.
- 결과/한계: build/type·Backend package/test compile·합성 ML/HTTP·로그인 화면 전후 비교 통과. lint 기존 52 errors·6 warnings는 동일하며 실제 API/DB/결제·운영 모델은 미검증. 자세한 Task/Gate·근거는 WORK. 원본 365개 이력은 유지했으며 11:45:40Z 재개 승인 범위도 같았다.
- worktree 위치: 사용자 요청으로 WYBU의 dev/worktrees/프로젝트/브랜치 배치에 맞춰 Git worktree move를 완료했다. 위치 이동 당시 branch `refactor/app-paths`·HEAD `43addd0` 보존. 위치 변경 당시 미커밋이었던 CURRENT·WORK는 관련 커밋 `4e72323`으로 정리했다. 위치 검증 근거는 WORK.
- 최신 승인: 사용자의 `푸쉬 피알 스쿼시 머지로 해야지` 정정에 따라 작업 branch push→Draft PR→검토→Ready→Squash merge를 진행한다. 앞선 assistant의 로컬 병합만 해석을 대체한다. 전달 기준은 main `183600ee`였으며 [PR #1](https://github.com/Hdev-x/kopang-refactored/pull/1)을 Draft로 생성했다. 현재 Ready/merge·Squash commit과 원격·로컬 상태는 해당 PR과 Git/WORK의 외부 근거에서 확인한다. 보호/검사 우회·force push·공유 이력 재작성·원본 팀/WYBU/펫케어 변경은 하지 않는다.
- 다음 행동 하나: 기존 lint 실패와 개인 Backend/ML 실행 환경 중 먼저 다룰 후속 범위를 결정한다. 새 작업은 이 PR의 실제 merge 결과와 최신 main을 확인한 뒤 별도 branch에서 시작한다. 이번 Git 전달은 승인 범위에서 Ready·Squash·안전한 local 동기화까지 진행하며, 최종 상태는 Git/PR에서 확인한다.

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

## 후속 변경에서 확인할 범위

앱 최상위 경로 이전의 명령·참조·baseline·비교·복구 기준은 WORK에서 완료했다. 실제 Backend runtime·API/DB·운영 모델·전체 기능 검증은 개인 환경과 입력을 확보한 뒤 진행한다. 기존 구조 계획의 CSS 정리는 후보이며 실행 순서나 구체적 변경을 이번 운영 적용으로 승인한 것이 아니다. 기능·URL·디자인·DB·ML 계약 변경과 묶지 않는다. 검증 환경 관련 질문은 OPEN-QUESTIONS에서 필요한 것부터 확인한다.
