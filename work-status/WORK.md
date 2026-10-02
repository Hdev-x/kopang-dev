# 개인 코팡 작업 계획

> 갱신: 2026-10-02 · Task·Gate 상태 정본. 현재 진입점은 [CURRENT](./CURRENT.md), 작성 규칙은 [운영 규칙](./README.md).
> `WORK.md`는 WYBU에 있던 동일 파일명이 아니라 `work/.../plan.md` 역할을 코팡에 단순화한 계획 파일이다.

## 운영규칙 전체 대조·보완

- 상태: 완료 (로컬 문서 적용). 목표: 부분 적용을 보완해 필요한 작업·Git·문서·검증 규칙을 정확히 이어가기.
- 포함: 원본 연결 규칙 대조, 필요한 코팡 운영문서·template·상태 수정, 완전성·참조·범위 검증.
- 제외: 앱 소스 이동/리팩터링, 실제 branch 생성·commit/push/PR/merge, WYBU/원팀 수정, CI/권한/Runtime 적용.
- 완료 조건: 원본 운영규칙의 반영/수정/제외와 이유가 [대조표](../docs/WYBU-운영규칙-대조.md)에 있고 Task·Gate 증거와 문서 상태가 일치.

### Task

- [x] 통과 · AGENTS와 연결 작업·Git·문서 규칙/양식의 실제 원본 대조.
- [x] 통과 · 코팡에 WORK·운영/Git 규칙·PR/Issue 양식과 기존 상태 문서 반영.
- [x] 통과 · 대조표 완전성, 링크·상태·기존 코드/문서·개인/원본 Git 상태 보존 검증.

### Gate

- [x] 통과 · 원본 범위의 모든 규칙에 적용성 분류·반영 위치·이유가 있고, 관련 링크·문서 정합성·변경 범위 검사와 독립 검토 완료.
- 증거: 2026-10-02, 개인 main 기준 `183600eeb3250ad61053037e3ca9e3c82dc6dd9e`의 문서 working tree, WYBU main `4a172b08e177cde8c85f97d471de7e20a47ffbb3`. [외부 적용 검증](</Users/han/Documents/Codex/2026-10-02/task-2/operations-complete/verification.json>)에 변경 파일 해시·원본 inventory·검증 결과. 이 자료는 다른 clone에 없을 수 있어 실제 Git/문서로 재확인한다.
- 한계: build/lint·브라우저·API·DB·ML 실행, remote CI/보호/merge 설정은 검증하지 않음. commit·GitHub 반영 전이며 검사 통과가 앱 실행 정상이나 실행 승인까지 뜻하지 않음.

## 앱 경로 이전의 실행 계획·검증 설계

- 상태: 완료 (실행 범위·검증 설계). 후속 실행 결과는 아래 앱 경로 이전 구획에서 관리한다.
- 목표: `frontend→apps/web`, `backend→apps/backend`, `ml→apps/ml`의 작은 실행/검증/복구 단위 구체화.
- 포함: [구조 계획](../docs/개인-리팩터링-구조-계획.md) 6–7절 기준 실제 참조 경로·명령·baseline·환경·복구 방법 조사/계획.
- 이 계획 단계의 제외: 파일 이동·기능/URL/디자인/DB/모델 계약 변경·실제 Git 전달·운영 DB/결제 실행. 실제 파일 이동·로컬 커밋은 아래의 별도 승인된 실행 범위다.
- 완료 조건: 앱별 이전 대상/참조·검증 명령/입력/기존 실패·복구·중단 조건과 실행 승인 범위 제시. 미확인 환경은 통과로 쓰지 않음.

### Task

- [x] 통과 · 앱 내부 상대 import/config·정적 자산은 보존, 최상위 명령/문서와 ML 루트 상대 경로 4건을 목록화. root Node/CI/monorepo 참조 없음.
- [x] 통과 · Node 25.9.0/npm 11.12.1·npm ci, Gradle wrapper 8.14.5/JDK 21, Python 3.14.4/기존 고정 requirements와 안전한 합성 fixture로 기준 확인. 실제 환경값/DB는 사용하지 않음.
- [x] 통과 · 문서 기준 커밋→별도 worktree→앱 전체 이동→필수 경로 수정→동일 검사·파일 대조 순서. 원본/primary 앱은 유지되며 복구 기준은 `9ec5237`; 새 실패 시 해당 작업공간 변경을 재검토하고 사용자 변경을 덮어쓰지 않음.
- [x] 통과 · 세 앱 이동·필수 참조 수정·baseline/후 검증·로컬 커밋의 사용자 실행 승인 확인 (2026-10-02 11:31:22Z `ㄱㄱ`). 원격 전달·기능 리팩터링 제외.

### Gate

- [x] 통과 · 실제 참조·기준 결과·한계·복구 기준과 사용자 실행 승인 확인. 실행 검증 결과는 아래 구획에 남김.
- 근거: `9ec5237`의 928 tracked 파일(앱 900개), 독립 경로 조사와 이동 직전 baseline. 누락된 application-dev/model/아카이브를 실제 환경 검증으로 간주하지 않음.

장기 목표의 나머지 프론트 경계·반응형 통합 방향은 구조 계획에 남긴다. 아직 조사하지 않은 미래 기능의 추측 Task·별도 roadmap을 만들지 않는다.

## 앱 경로 이전 및 로컬 검증

- 상태: 완료 (로컬 앱 이동·경로 수정·비교 검증). 결과는 당시 `refactor/app-paths` worktree에서 작성했으며 로컬 commit/HEAD는 Git 실제 상태로 확인한다. 목표: 세 앱 최상위 위치를 옮기고 기존 계약 보존.
- 포함: 작성한 문서 기준 커밋, 작업 branch/worktree, 앱별 폴더 이동·필수 경로/명령/문서 참조, baseline/후 비교, 상태 기록, 로컬 결과 커밋.
- 제외: 기능/스타일/PC·mobile 통합, 운영/원팀 DB·결제 실행, 원본 팀/WYBU/펫케어 변경, push·PR·merge/main 병합·CI 보호 설정.
- 승인 근거: 위 계획과 문서 커밋+폴더 이동 안내 후 사용자 `ㄱㄱ` (2026-10-02 11:31:22Z). 이력 확인 요청으로 잠시 중단했으며 사용자 `그냥 그대로 진행` (11:45:40Z)로 같은 범위를 재개. 원본 365개 이력 유지.

### Task

- [x] 통과 · 문서 범위·secret 확인, 기준 커밋 `9ec5237`, 별도 `refactor/app-paths` worktree 준비.
- [x] 확인 완료 · baseline: frontend build/type 통과, lint 기존 52 errors·6 warnings; Backend assemble/testClasses 통과; ML 합성 240행 학습·HTTP/결측/피처/위험 경계 통과; 비로그인 /login·/web/login 렌더 확인. Backend runtime·DB/결제는 미검증.
- [x] 통과 · frontend 602개→apps/web, backend 277개→apps/backend, ML 21개→apps/ml; 실행 경로 문자열 4건과 필요한 명령·설명·문서 링크만 수정.
- [x] 통과 · 전후 build/type·Backend package/test compile·합성 ML/HTTP·로그인 화면 비교, 파일/mode/AST/Route·diff·비밀정보 확인. 기존 lint 실패는 동일하고 아래 한계에 명시.
- [x] 통과 · 검증/한계와 다음 행동 기록. commit·원격 반영 상태는 반복 상태 체크 대신 Git으로 확인하며, 승인된 전달 범위는 로컬 커밋까지다.

### Gate

- [x] 통과 · 이번 경로 이전 Gate: 앱 900파일 누락·mode 변경 없음; frontend UI/styles/assets/config/package/lock과 Backend 전체 byte 보존; ML 9개 Python은 경로 정규화·docstring 제외 후 AST 동일; 기존 실패 대비 새 실패 없음; 새 broken link 없음; 전체 diff·secret 검사 통과. API/DB의 실제 동작은 아래 미검증으로 유지.
- 증거: 문서 기준 `9ec5237`의 이동 직전/후 SHA256·mode 대조와 독립 검토. [외부 경로 이전 검증](</Users/han/Documents/Codex/2026-10-02/task-2/app-relocation/verification.json>)에 검사 명령·전후 결과·화면/로그 해시·실제 Git 상태를 기록하며, 다른 clone에는 없을 수 있음.
- 안전 조건: Backend compile은 DB 없이, SpringBootTest/배치·ML seed/demo는 실제환경 없이 실행하지 않음. ML 입력은 합성 fixture만, 실제 모델/DB 상태를 정상으로 주장하지 않음.


### 검증 결과와 다음 행동

| 검사 | 이동 전 → 이동 후 | 한계 |
|---|---|---|
| Frontend `npm run build` (tsc 포함) | 통과 → 통과; CSS/JS 산출물 이름·hash 동일 | 기존 500kB 이상 chunk 경고 유지 |
| Frontend `npm run lint` | 실패 → 동일 실패; 52 errors·6 warnings, 앱 경로 정규화 후 출력 완전 동일 | 기존 React hooks/purity·타입 등의 오류는 이번 경로 이전에서 수정하지 않음 |
| Backend wrapper `assemble testClasses` | 통과 → `clean assemble testClasses` 통과 | Spring context·기존 @SpringBootTest·API·DB·스케줄 배치는 실행하지 않음 |
| ML 구문·학습·서빙 | 9개 Python 구문 통과; 합성 240행 학습 및 실제 로컬 `/health`, `/predict/churn` HTTP의 전후 결과 동일 | 입력/모델 파일 경로를 검사한 뒤 audit fixture·외부 임시 모델로 대체. 실제 학습 데이터·운영 모델·DB 연동 증명이 아님 |
| ML 피처·빈 요청·결측·위험 경계 | 14개 피처 순서, empty 결과, null/미입력 기본값, 0.4/0.7 위험 경계 보존 | seed/demo/공유 DB 명령은 실행하지 않음 |
| 대표 화면 | 비로그인 `/login`, `/web/login`, 1280×720 렌더; 두 DOM snapshot·PNG SHA256 전후 동일, 확인 중 console error/warn 없음 | 로그인 제출·OAuth·결제·가입/상품 조회 이력 쓰기·전체 화면/반응형 기능 검증은 하지 않음. 외부 SDK 개별 통신은 검증하지 않음 |
| 보존·문서 | 928 tracked 파일 매핑 보존, AppRouter 101개 Route byte 동일, 새 상대 링크 누락 없음 | root/ML README의 docs/_ 링크 3개, Web TODO의 API 초안·ML _ 아카이브는 이전부터 미존재. 임의 대체/생성하지 않음 |

- 당시 앱 이전 검증 작업공간: `/Users/han/Documents/Codex/2026-10-02/task-2/kopang-app-paths`, branch `refactor/app-paths`. 현재 작업 위치는 [CURRENT](./CURRENT.md)를 참조한다. 당시 앱 이전 worktree는 PR #1 merge 뒤 정리했다. 당시 primary `/Users/han/dev/projects/personal/kopang-refactored`의 main은 문서 기준 `9ec5237`이었고 앱 배치는 기존대로였다.
- 비밀정보: 실제 환경값·토큰·model·의존성·build/검증 산출물은 커밋하지 않음. 학습/API/DB 환경이 필요한 후속 기능은 개인 검증 입력·안전한 서비스부터 확보한다.
- 당시 다음 행동: 기존 lint 실패와 개인 Backend/ML 실행 환경 중 후속 범위 결정. 앱 이전 당시 원격 전달은 제외였으며, 이후 승인된 GitHub 전달은 아래 별도 구획에서 관리한다.


## 수동 worktree의 dev 위치 변경

- 상태: 완료 (로컬 위치 이동·문서 경로 갱신). 사용자 요청에 따라 기존 worktree를 재사용했고 새 branch·commit·push·merge·앱 변경은 하지 않음.
- 적용 관례: WYBU 실제 worktree 및 AGENTS/git-workflow의 `/Users/han/dev/worktrees/<project>/<type>/<task>` 배치. 이동 당시 코팡 worktree 위치는 `/Users/han/dev/worktrees/kopang-refactored/refactor/app-paths`였으며 branch `refactor/app-paths`·HEAD `43addd0`을 보존한다.
- 방법: 시작 clean·실행 앱 프로세스 없음·목적지 충돌 없음 확인 후 Git worktree move. 과거 위치와 외부 감사 자료는 당시 기록으로 보존하며 감사 폴더를 옮기지 않음.
- 검증: 이동 전후 tracked 928개 SHA256/mode 동일, 의존성/생성물 포함 244,953개 파일의 inode·size·mode·symlink 동일, old 위치 소멸·new toplevel·Git 연결/backlink·worktree 등록 확인. 새 위치에서 Vite 8.1.0/Node 25.9.0, Gradle wrapper 8.14.5/JDK 21 버전 명령, ML 9개 AST와 root CSV/서빙 module 및 web bin 링크 확인. 앱 소스가 동일해 이전 build/lint/ML/화면 검사를 반복하지 않았고 실제 API/DB/모델 미검증은 그대로다.
- 위치 변경 종료 당시: CURRENT·WORK의 위치 기록만 unstaged dirty로 보존했다. 추가 commit/push는 해당 위치 요청에 포함되지 않았고 primary main `9ec5237`과 원본 팀/WYBU/펫케어를 수정하지 않았다. 최신 로컬 main 병합 요청에서 `4e72323`으로 관련 문서 커밋을 정리했다.
- 근거: [외부 worktree 위치 검증](</Users/han/Documents/Codex/2026-10-02/task-2/worktree-relocation/verification.json>). 기존 app-relocation 등 외부 evidence의 경로와 링크는 유지한다.


## 앱·위치 결과의 로컬 main 반영

- 상태: 완료 (당시 로컬 FF 실행 기록). assistant가 `머지까지 해줘` 요청을 로컬 main 반영으로 좁게 해석해 진행했다. 이후 사용자가 push·PR·Squash를 명시해 아래 원격 단계로 정정했다. 당시 원격 행동·삭제·기능 변경은 실행하지 않았다.
- 시작 상태: primary main `9ec5237` clean, branch `refactor/app-paths`의 `43addd0`에 CURRENT·WORK 위치 기록만 unstaged. main은 branch의 조상이고 충돌할 primary ignored 파일도 없음.
- 방법/실행: 관련 위치 문서 `4e72323` 커밋 후 `git merge --ff-only refactor/app-paths`로 main을 `9ec5237`에서 `4e72323`으로 갱신했다. 최신 실제 상태 문서 `2d3bec8`도 같은 branch에서 커밋해 fast-forward로 main에 포함했다. 해당 로컬 단계에서는 기존 커밋을 보존하고 별도 merge commit·Squash·rebase를 만들지 않았다. 원격 PR/Squash 기본 정책이나 보호 설정은 변경하지 않는다.
- 기준: 기존 build/type·Backend package/test compile·합성 ML HTTP·로그인 두 화면 검증과 앱 900개 SHA256/mode를 재확인한다. lint 기존 52 errors·6 warnings 및 실제 API/DB/결제/모델 미검증은 유지한다. 문서 링크·전체 diff·secret 확인과 실제 main/branch 상태 대조로 완료 판단.

- 완료 검증: main에 apps/web·apps/backend·apps/ml와 관련 기록 반영. 앱 900개 SHA256·mode는 `43addd0`과 같고 기본 앱 코드 변경 없음. 새 앱 검사를 반복하지 않고 소스 동일성에 따라 위 기존 build/type·Backend compile/package·합성 ML HTTP·로그인 비교 증거를 유지한다. 위치·완료 문서의 링크/diff/secret와 main·branch 결과 및 dirty 상태를 확인한다.
- 범위/한계: 기존 lint 52 errors·6 warnings, 실제 Spring context·API/DB·결제·운영 모델 미검증은 그대로다. 로컬 완료를 GitHub 반영으로 표시하지 않는다. 당시 원격은 main `183600ee`만 있었으며 해당 로컬 단계의 commit·상태는 아래 외부 근거에서 확인한다. worktree·branch와 필요한 ignored 의존성/생성물을 보존한다.
- 근거: [외부 로컬 main 반영 검증](</Users/han/Documents/Codex/2026-10-02/task-2/local-main-merge/verification.json>). 현재 상태·다음 행동은 CURRENT에서 관리한다.


## GitHub 전달과 Squash merge

- 상태: 내용·검증 정리 완료. [PR #1](https://github.com/Hdev-x/kopang-refactored/pull/1)을 Draft로 생성했고, Ready·merge·Squash SHA의 최신 상태는 PR/Git에서 확인한다. 이 구획의 Task는 내용/검증 Gate이며 실제 Git lifecycle 완료를 추정하지 않는다.
- 최신 승인: 사용자 `푸쉬 피알 스쿼시 머지로 해야지`가 앞선 assistant의 local-only 해석을 대체한다. 작업 branch push→Draft PR→내용/검증 검토→Ready→Squash merge→로컬 main 동기화→이번 remote/local branch·worktree 안전 정리까지 진행한다. 원격 main 직접 push·force push·보호/검사 우회·운영 DB/결제 실행은 하지 않는다.
- 전달 기준: 실제 원격 main `183600ee` (원본 365개 이력). PR에는 운영규칙/상태/PR·Issue 양식과 앱 900파일 최상위 이전·필수 경로·위치 기록을 함께 설명한다. 기존 로컬 main FF와 최종 작업 이력은 외부 Git bundle로, worktree 전체 파일·필요한 ignored 생성물은 외부 archive로 복구 가능하게 보존한다. 종료 후 이번 작업용 backup/remote/local branch·worktree는 남기지 않는다.
- GitHub 확인: 인증 Hdev-x, 비공개 저장소, push 권한 및 Squash 허용. main 조회의 protected=false. branch rules API는 현재 비공개 플랜의 403으로 조회 불가이므로 규칙 없음으로 쓰지 않는다. 실제 PR 검사·merge 조건은 PR/GitHub의 응답을 따르며 admin bypass는 사용하지 않는다.

### Task·내용 Gate

- [x] 통과 · 실제 remote/auth/중복 PR·main ancestry·전달 범위 확인. local main 직접 업로드 없이 작업 branch를 사용한다.
- [x] 통과 · 최신 승인/기록과 PR 본문을 전체 diff·검증 결과·기존 실패·미검증에 맞춰 완성.
- [x] 통과 · Draft PR 내용의 전체 diff·비밀정보·앱 900개 보존·독립 코드/문서 검토 완료. 제출 직후 head `8c0b538`은 main `183600ee` 기준 914개 변경, mergeable/clean, check runs·commit statuses·리뷰·review thread 0개였다. 자동 검사 없음은 통과가 아니라 미등록으로 기록한다. 후속 상태 문서 변경은 앱 소스 동일성 및 새 diff/secret 검사로 확인한다.
- [x] 준비 완료 · 최신 head의 실제 검사/리뷰·native merge 조건과 부모의 최종 검토 Gate를 확인한 뒤 Ready·해당 SHA Squash를 진행한다. clean main의 기존 이력·최종 작업 branch를 외부 Git bundle로, worktree 전체를 외부 archive로 검증 보존한다. Squash tree와 최종 PR head·기존 local 변경 포함을 확인한 뒤 main을 origin/main에 동기화하고 이번 remote branch→Git worktree 제거→작업/임시 backup local branch만 정리한다. 실제 실행·SHA/tree·복구 자료·최종 refs는 Git/PR와 외부 근거가 정본이다.

- 기존 앱 검증: build/type·Backend package/test compile·합성 ML HTTP·로그인 두 화면 비교 통과. lint 52 errors·6 warnings는 동일한 기존 실패다. PR 최신 head의 앱 900개 SHA256/mode와 승인된 ML 경로 4곳 정규화 AST를 대조하며 소스가 같으면 앱 검사를 반복하지 않는다. 실제 API/DB/결제/운영 모델은 미검증이고 원격 required check 실패는 우회하지 않는다.

- 내용 Gate 근거: 원본 365개 커밋 누락 없음, 앱 900개 mode/매핑 보존 및 Web 599개·Backend 277개 blob 동일, ML 9개 승인 경로/docstring 정규화 AST 동일을 독립 검토했다. 상태 문서의 마지막 변경은 이 결과를 바꾸지 않는다. [외부 GitHub 전달 검증](</Users/han/Documents/Codex/2026-10-02/task-2/github-pr-merge/verification.json>)은 이 컴퓨터에서 실제 최신 head·검사·PR/merge·backup·local 결과를 확인하며 갱신한다. 다른 clone에서는 해당 PR/Git와 관련 코드로 재확인한다.

### 상세 운영 양식·형식 검사 보완

- 최신 사용자 재확인에 따라 WYBU의 상세 결과 card·변경 분류/중첩·이유 목록·검증 중첩과 PR checker·관련 테스트·단독 workflow를 보완한다. 원본 제품 `tests/*.test.mjs` 전체 실행은 제외하고 `tests/pr-check.test.mjs`만 실행한다. `refactor` type·WORK 링크·미검증 설명·4개 확인 항목은 코팡에 맞춘다.
- 초기 Draft에는 PR/work Issue 양식이 head에 있었고 base/main에는 기존 qa-bug만 있었다. 상세 형식/자동 검사 제외는 이번 보완으로 대체하며 qa-bug와 앱 900개는 보존한다.
- [x] 통과 · 원본 상세 양식·checker·관련 테스트·workflow와 Git 종료 규칙/본문을 일치시켰다. 제품 CI glob 제외·refactor/WORK/4개체크 적용, 기존 qa-bug·앱 소스 보존.
- [x] 통과 · 로컬 checker 테스트 8개·실제 Draft 본문/Ready 후보 형식 검사 통과. 현재 앱 900개/hash/mode·QA 양식 보존, 문서 링크/diff/secret·독립 양식 검토 완료. 실제 최신 head workflow 결과와 부모 최종 검토·Ready/merge/정리는 Git/PR·외부 근거로 확인하며 로컬 검증을 원격 성공으로 표시하지 않는다.


## 작업 상태 폴더 root 배치

- 상태: 완료 (최초 로컬 문서 위치·참조 수정과 검증 당시 기록). 기준: main `4bf73790a66145f7c548174af5a77d3a24cbc828`에서 만든 `docs/root-work-status` branch/worktree.
- 결과: `docs/work-status/`의 CURRENT·WORK·DECISIONS·OPEN-QUESTIONS·README 5개를 root `work-status/`로 이동했다. AGENTS·root README·구조 계획·운영 제안·WYBU 대조표의 관련 활성 참조와 이동 문서의 상대 링크를 맞추고, 옛 배치·Git 전달 기록은 당시 기록으로 표시했다.
- 펫케어: `/Users/han/dev/projects/team/petcare/work-status/`는 이미 root이며 별도 Git 저장소다. 활성 AGENTS·Planning Manifest·연결 문서가 존재하고 옛 `docs/work-status` 참조가 없어 경로 수정은 필요하지 않다. 기존 미커밋 3개는 수정하지 않는다.
- 검증 기준: 5개 새 위치·옛 폴더 소멸, 변경 문서 링크 누락 추가 없음·활성 옛 경로 없음·CURRENT/WORK/결정 정합, 문서만의 diff·staged 없음·HEAD 보존, 펫케어 dirty 파일 해시·Git 상태 보존. PR/Issue template·checker·관련 테스트·workflow에는 옛 경로가 없으므로 수정·테스트 반복을 하지 않는다.
- 검증 결과: 상태 5파일·mode 보존, 옛 폴더 소멸, 변경 문서 링크 214개 확인·추가 누락 0·활성 옛 경로 링크 0, 문서 범위·diff 검사 통과. root README의 기존 누락 ML 문서 링크 1개는 그대로다. 앱·PR/Issue 양식·checker·테스트·workflow·Git 문서는 변경하지 않았다. 작업 HEAD·unstaged 상태·primary main과 펫케어 HEAD/branch/dirty 3파일 SHA256을 보존했다.
- 근거: [외부 배치 검증](</Users/han/Documents/Codex/2026-10-02/task-2/work-status-layout/verification.json>)에 관찰 시점·변경 파일·링크·범위·보존 결과를 남긴다. 다른 clone에는 없는 로컬 자료다.
- 최초 로컬 단계 한계: 앱 build/API/DB/ML·대규모 이력/복구 archive 검사는 반복하지 않았다. 당시 commit·push·PR·merge는 제외였고 이후 사용자 요청으로 아래 Git 전달 범위를 승인받았다.


## root 배치·규칙 보완의 GitHub 전달

- 상태: 내용·로컬 검증 완료. 실제 원격 검사·Ready/merge·정리는 Git/PR의 최신 상태로 확인한다. 목표: 기존 root 이동 결과를 보존하고 필요한 운영규칙·양식 대조를 마친 한 결과를 PR·Squash로 전달한다. 기준 main `4bf73790a66145f7c548174af5a77d3a24cbc828`, 기존 `docs/root-work-status` branch/worktree 재사용.
- 승인: 사용자 “둘다 피알템플릿이라던지 규칙 잘 되어있는거지? 잘 되어있으면 pr 올리고 스커시머지까지 진행해줘” 및 worktree 규칙까지 꼼꼼히 대조 요청. 코팡 개인 저장소의 문서·양식·관련 검사 보완, commit/push·Draft/Ready·Squash·main 동기화·이번 branch/worktree 안전 정리를 포함한다. 보호/보안 설정 우회·원팀/WYBU 수정·앱 계약 변경은 제외한다.
- 대조 결과: 수동 dev/worktrees 경로·branch 대응과 CURRENT 실질 변경 시 Main 갱신 조건 2개 보완. Fast/Stage 단위·독립 Writer 작업환경·single Writer·충돌 처리·시작/종료 갱신·Squash 뒤 동기화/정리는 기존 규칙 유지. 상세 PR/Issue 양식·checker·focused 테스트·workflow 필수 누락 없음. 제품특화 제외 이유와 실제 파일 근거는 [WYBU 대조표](../docs/WYBU-운영규칙-대조.md)에 기록한다.
- Gate: 문서 이동 보존·상대 링크·활성 옛 경로·상태/합의 정합, 문서만의 전체 diff·민감정보, checker 테스트 8개와 실제 Draft/Ready 본문 형식, 실제 최신 head 자동 검사·review·native merge 조건을 확인한다. 로컬 Gate와 원격 merge 완료는 구분한다.
- 로컬 Gate 결과: 기존 이동 5파일·문서 범위·상태/승인·새 규칙 2개 독립 대조 통과. 링크 223개·추가 누락 0·활성 옛 경로 링크 0·diff/민감정보 검사 통과, checker 테스트 8/8 통과. 기존 root README 누락 ML 링크는 그대로며 앱·상세 template·Issue·checker·테스트·workflow는 변경하지 않았다. 최초 PR 제출 전에는 원격 check를 통과로 표시하지 않고 실제 최신 head 결과를 아래 외부 근거에서 확인한다.
- 근거: [외부 PR 전달 검증](</Users/han/Documents/Codex/2026-10-02/task-2/work-status-pr/verification.json>)에 최신 PR URL·head/base·검사·merge SHA·복구 자료·main 동기화·정리 결과를 남긴다. 다른 clone에는 없는 로컬 자료이므로 실제 Git/PR로 재확인한다.
- 한계·다음 행동: 앱 전체 build·이력/대형 archive 재검사는 반복하지 않는다. 기존 lint 실패와 실제 API/DB/결제/운영 모델 미검증은 앞선 앱 결과의 한계다. 새 기능 실행 정상이나 서버 required 보호를 이번 문서/형식 검사로 주장하지 않는다. 후속 개선 범위는 CURRENT에서 확인한다.
