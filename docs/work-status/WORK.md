# 개인 코팡 작업 계획

> 갱신: 2026-10-02 · Task·Gate 상태 정본. 현재 진입점은 [CURRENT](./CURRENT.md), 작성 규칙은 [운영 규칙](./README.md).
> `WORK.md`는 WYBU에 있던 동일 파일명이 아니라 `work/.../plan.md` 역할을 코팡에 단순화한 계획 파일이다.

## 운영규칙 전체 대조·보완

- 상태: 완료 (로컬 문서 적용). 목표: 부분 적용을 보완해 필요한 작업·Git·문서·검증 규칙을 정확히 이어가기.
- 포함: 원본 연결 규칙 대조, 필요한 코팡 운영문서·template·상태 수정, 완전성·참조·범위 검증.
- 제외: 앱 소스 이동/리팩터링, 실제 branch 생성·commit/push/PR/merge, WYBU/원팀 수정, CI/권한/Runtime 적용.
- 완료 조건: 원본 운영규칙의 반영/수정/제외와 이유가 [대조표](../WYBU-운영규칙-대조.md)에 있고 Task·Gate 증거와 문서 상태가 일치.

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
- 포함: [구조 계획](../개인-리팩터링-구조-계획.md) 6–7절 기준 실제 참조 경로·명령·baseline·환경·복구 방법 조사/계획.
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

- 상태: 완료 (로컬 앱 이동·경로 수정·비교 검증). 결과는 `refactor/app-paths` worktree에 있으며 로컬 commit/HEAD는 Git 실제 상태로 확인한다. 목표: 세 앱 최상위 위치를 옮기고 기존 계약 보존.
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

- 당시 앱 이전 검증 작업공간: `/Users/han/Documents/Codex/2026-10-02/task-2/kopang-app-paths`, branch `refactor/app-paths`. 현재 dev 위치는 [CURRENT](./CURRENT.md)를 참조한다. 당시 primary `/Users/han/dev/projects/personal/kopang-refactored`의 main은 문서 기준 `9ec5237`이었고 앱 배치는 기존대로였다.
- 비밀정보: 실제 환경값·토큰·model·의존성·build/검증 산출물은 커밋하지 않음. 학습/API/DB 환경이 필요한 후속 기능은 개인 검증 입력·안전한 서비스부터 확보한다.
- 다음 행동 하나: 기존 lint 실패와 개인 Backend/ML 실행 환경 중 먼저 다룰 후속 범위를 결정한다. push·PR·merge는 이번 승인 범위에 포함되지 않는다.


## 수동 worktree의 dev 위치 변경

- 상태: 완료 (로컬 위치 이동·문서 경로 갱신). 사용자 요청에 따라 기존 worktree를 재사용했고 새 branch·commit·push·merge·앱 변경은 하지 않음.
- 적용 관례: WYBU 실제 worktree 및 AGENTS/git-workflow의 `/Users/han/dev/worktrees/<project>/<type>/<task>` 배치. 코팡의 현재 위치는 `/Users/han/dev/worktrees/kopang-refactored/refactor/app-paths`이며 branch `refactor/app-paths`·HEAD `43addd0`을 보존한다.
- 방법: 시작 clean·실행 앱 프로세스 없음·목적지 충돌 없음 확인 후 Git worktree move. 과거 위치와 외부 감사 자료는 당시 기록으로 보존하며 감사 폴더를 옮기지 않음.
- 검증: 이동 전후 tracked 928개 SHA256/mode 동일, 의존성/생성물 포함 244,953개 파일의 inode·size·mode·symlink 동일, old 위치 소멸·new toplevel·Git 연결/backlink·worktree 등록 확인. 새 위치에서 Vite 8.1.0/Node 25.9.0, Gradle wrapper 8.14.5/JDK 21 버전 명령, ML 9개 AST와 root CSV/서빙 module 및 web bin 링크 확인. 앱 소스가 동일해 이전 build/lint/ML/화면 검사를 반복하지 않았고 실제 API/DB/모델 미검증은 그대로다.
- 위치 변경 종료 당시: CURRENT·WORK의 위치 기록만 unstaged dirty로 보존했다. 추가 commit/push는 해당 위치 요청에 포함되지 않았고 primary main `9ec5237`과 원본 팀/WYBU/펫케어를 수정하지 않았다. 최신 로컬 main 병합 요청에서 `4e72323`으로 관련 문서 커밋을 정리했다.
- 근거: [외부 worktree 위치 검증](</Users/han/Documents/Codex/2026-10-02/task-2/worktree-relocation/verification.json>). 기존 app-relocation 등 외부 evidence의 경로와 링크는 유지한다.


## 앱·위치 결과의 로컬 main 반영

- 상태: 완료 (당시 로컬 FF 실행 기록). assistant가 `머지까지 해줘` 요청을 로컬 main 반영으로 좁게 해석해 진행했다. 이후 사용자가 push·PR·Squash를 명시해 아래 원격 단계로 정정했다. 당시 원격 행동·삭제·기능 변경은 실행하지 않았다.
- 시작 상태: primary main `9ec5237` clean, branch `refactor/app-paths`의 `43addd0`에 CURRENT·WORK 위치 기록만 unstaged. main은 branch의 조상이고 충돌할 primary ignored 파일도 없음.
- 방법/실행: 관련 위치 문서 `4e72323` 커밋 후 `git merge --ff-only refactor/app-paths`로 main을 `9ec5237`에서 `4e72323`으로 갱신했다. 최신 실제 상태 문서도 같은 branch에서 커밋해 fast-forward로 main에 포함한다. 기존 커밋은 그대로 보존하며 별도 merge commit·Squash·rebase를 만들지 않는다. 원격 PR/Squash 기본 정책이나 보호 설정은 변경하지 않는다.
- 기준: 기존 build/type·Backend package/test compile·합성 ML HTTP·로그인 두 화면 검증과 앱 900개 SHA256/mode를 재확인한다. lint 기존 52 errors·6 warnings 및 실제 API/DB/결제/모델 미검증은 유지한다. 문서 링크·전체 diff·secret 확인과 실제 main/branch 상태 대조로 완료 판단.

- 완료 검증: main에 apps/web·apps/backend·apps/ml와 관련 기록 반영. 앱 900개 SHA256·mode는 `43addd0`과 같고 기본 앱 코드 변경 없음. 새 앱 검사를 반복하지 않고 소스 동일성에 따라 위 기존 build/type·Backend compile/package·합성 ML HTTP·로그인 비교 증거를 유지한다. 위치·완료 문서의 링크/diff/secret와 main·branch 결과 및 dirty 상태를 확인한다.
- 범위/한계: 기존 lint 52 errors·6 warnings, 실제 Spring context·API/DB·결제·운영 모델 미검증은 그대로다. 로컬 완료를 GitHub 반영으로 표시하지 않는다. 당시 원격은 main `183600ee`만 있었으며 해당 로컬 단계의 commit·상태는 아래 외부 근거에서 확인한다. worktree·branch와 필요한 ignored 의존성/생성물을 보존한다.
- 근거: [외부 로컬 main 반영 검증](</Users/han/Documents/Codex/2026-10-02/task-2/local-main-merge/verification.json>). 현재 상태·다음 행동은 CURRENT에서 관리한다.


## GitHub 전달과 Squash merge

- 최신 승인: 사용자 `푸쉬 피알 스쿼시 머지로 해야지`가 앞선 assistant의 local-only 해석을 대체한다. 작업 branch push→Draft PR→내용/검증 검토→Ready→Squash merge와 안전한 로컬 main 동기화까지 진행한다. 원격 main 직접 push·force push·보호/검사 우회·운영 DB/결제 실행은 하지 않는다.
- 전달 기준: 실제 원격 main `183600ee` (원본 365개 이력). PR에는 운영규칙/상태/PR·Issue 양식과 앱 900파일 최상위 이전·필수 경로·위치 기록을 함께 설명한다. 기존 로컬 main FF 계열은 Squash 후 복구 가능한 backup과 해당 worktree branch로 보존한다.
- GitHub 확인: 인증 Hdev-x, 비공개 저장소, push 권한 및 Squash 허용. main 조회의 protected=false. branch rules API는 현재 비공개 플랜의 403으로 조회 불가이므로 규칙 없음으로 쓰지 않는다. 실제 PR 검사·merge 조건은 PR/GitHub의 응답을 따르며 admin bypass는 사용하지 않는다.

### Task·내용 Gate

- [x] 통과 · 실제 remote/auth/중복 PR·main ancestry·전달 범위 확인. local main 직접 업로드 없이 작업 branch를 사용한다.
- [ ] 진행 중 · 최신 승인/기록과 PR 본문을 실제 전체 diff·검증 한계에 맞춰 완성.
- [ ] 대기 · Draft PR 최신 head의 diff/범위·비밀정보·앱 보존·독립 검토·실제 자동검사/리뷰 상태 확인.
- [ ] 대기 · 내용 Gate 완료 후 Ready·Squash의 실제 상태/commit/tree와 local 동기화를 Git/GitHub에서 확인. Git lifecycle의 최종 상태는 저장소 문서에 추정 복제하지 않는다.

- 기존 앱 검증: build/type·Backend package/test compile·합성 ML HTTP·로그인 두 화면 비교 통과. lint 52 errors·6 warnings는 동일한 기존 실패다. PR 최신 head의 앱 900개 SHA256/mode와 승인된 ML 경로 4곳 정규화 AST를 대조하며 소스가 같으면 앱 검사를 반복하지 않는다. 실제 API/DB/결제/운영 모델은 미검증이고 원격 required check 실패는 우회하지 않는다.
