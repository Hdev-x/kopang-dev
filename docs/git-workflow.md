# 개인 코팡 Git 작업 규칙

> 채택: 2026-10-02 · 사용자 요청 범위와 상위 권한을 우선한다. 이 문서 채택은 Git 실행·원격 설정 변경 승인 자체가 아니다.

## 1. 승인과 초기 설정 경계

- 읽기/설명/조사는 Git 작업공간·기록·commit을 자동 생성하지 않는다.
- 파일 변경 요청: 필요한 branch/worktree 준비·로컬 변경·관련 검증까지. 단, 사용자가 특정 행동을 제외하면 그 제한 우선. commit은 `커밋까지`, push는 `푸시까지`처럼 그 행동을 포함한 요청이 있을 때만 진행한다.
- `PR까지`: 필요한 commit·push·PR 생성과 기존 검사 통과를 위한 구현·title/body 수정. merge·검사 삭제/우회/기준 완화는 제외.
- `merge까지`: PR 범위와 아래 merge Gate·Squash merge, 미반영 변경이 없는 해당 branch/worktree의 안전 정리. 타인의 branch 삭제·운영 데이터/Secret/Permission 변경·배포 승인을 포함하지 않는다.
- 이미 명확한 사용자 승인 범위는 반복 확인하지 않지만 대상·영향·권한이 달라지면 확인한다. force push·공유 history rebase/amend는 금지한다.
- 초기 운영 문서 적용 당시에는 main의 dirty 문서를 같은 위치에서 보존하는 한정 예외였고 branch 준비·commit/push/PR/merge·원격 Ruleset 설정을 실행하지 않았다. 이후 파일 변경에는 아래 작업 branch 정책을 적용한다. 기존 dirty 문서를 자동 stash·이동·삭제하지 않는다.

## 2. 결과와 작업공간

- 개인 기본 branch는 main. 장기 develop/영역 branch를 새로 만들지 않고, 한 검증 가능한 결과 또는 계획의 한 단계에 짧은 branch·worktree·PR 하나를 대응시킨다. Task별로 branch를 쪼개지 않는다.
- 새 결과는 실제 최신 origin/main을 확인하고 branch/worktree를 준비한다. main은 확인·최신화용이며 초기 설정 예외 뒤 직접 수정·직접 push하지 않는다. 원격 확인이 실패하면 최신이라고 주장하지 않는다. remote가 없는 경우에만 확인한 local main을 기준으로 한다.
- 첫 수정 전 status·HEAD·branch·worktree와 기존 dirty 파일을 확인한다. 같은 결과의 기존 적합한 worktree는 재사용한다. 새 작업은 기존 미커밋 문서와 겹치거나 기준에 포함되지 않는 규칙이 있으면 먼저 보존/이어가기 방법을 구체화한다. 현재 설정 문서를 포함하지 않은 깨끗한 origin/main worktree를 무작정 만들지 않는다.
- 파일을 바꾸는 간단 작업(Fast Path) 또는 계획의 한 단계(Stage)에는 branch·worktree·PR 하나를 대응시킨다. 수동 worktree는 `/Users/han/dev/worktrees/kopang-refactored/<type>/<task>`에 만들고 branch 이름을 경로에 그대로 대응시킨다. 예: `docs/root-work-status` → `/Users/han/dev/worktrees/kopang-refactored/docs/root-work-status`. 같은 결과의 적합한 기존 worktree는 재사용한다. Codex managed worktree는 해당 작업에서 사용자가 명시적으로 요청했을 때 만들고 도구가 반환한 등록 위치를 사용한다. 이미 같은 결과를 이어가는 managed worktree는 재사용하며 다른 worktree를 이동/재생성하지 않는다.
- 병렬 Writer는 작업공간을 분리하고 Main이 소유 파일·의존 순서를 지정한다. 동일 파일·worktree 동시 쓰기 금지, 공유 상태 문서는 Main 단일 Writer. 선행 결과가 필요하면 해당 PR이 merge된 최신 main에서 다음 결과를 시작한다.

## 3. Branch와 commit

- branch: `<type>/<short-task>`, lowercase kebab-case. type은 `feat`, `fix`, `refactor`, `docs`, `chore`. 목적이 읽히는 짧은 이름을 쓰며 원팀 `feature/*→develop`을 새 정책으로 적용하지 않는다.
- commit 승인 범위가 있으면 복구/검토하기 좋은 작은 결과 단위로 남긴다. 중간 commit의 엄격한 양식을 강제하지 않는다. 최종 PR 제목은 아래 형식을 따른다.
- commit 전 status와 staged diff를 직접 확인하고 현재 결과에 필요한 파일만 선택한다. 관련 없는 dirty·tracked/untracked 사용자 파일·비밀키·실제 환경값·개인정보·생성물은 포함하지 않는다.
- 로컬 완료·commit·push·merge는 별도 상태다. 공유한 이력을 재작성하지 않는다. Squash 뒤 main commit은 GitHub 기본 `<PR 제목> (#번호)`를 쓰고 PR 제목에 번호를 붙이거나 merge subject를 직접 덮어쓰지 않는다.
- push가 승인됐을 때 첫 push에 upstream을 설정하고 이후 같은 branch의 실제 upstream을 확인한다. 원격 백업만 목적이면 branch push로 충분하며 빈 commit·형식적인 Draft를 만들지 않는다.

## 4. Issue와 PR

- Issue는 선택이다. backlog·재현/범위 논의·담당/우선순위 공유·여러 PR 묶음이 실제 필요할 때 [.github 작업 양식](../.github/ISSUE_TEMPLATE/work.md)을 사용한다. Issue 생성은 그 외부 행동이 요청 범위에 있을 때만 한다.
- 계획 작업의 상태는 WORK가 정본이고 Issue는 요약/탐색이다. 작은 backlog는 Issue 자체로 충분하다. Task 상태를 Issue/WORK에 중복 복제하지 않는다. Issue 연결만을 위해 Work를 만들지 않는다.
- PR은 하나의 검증 가능한 결과만 포함한다. 제목: `feat|fix|refactor|docs|chore: 결과`. [활성 PR 양식](../.github/pull_request_template.md)의 요약·주요 변경·변경 이유·검증·확인을 작성한다.
- 요약은 `> **결과:** 내용` card로, 주요 변경은 굵은 분류와 중첩 목록으로, 변경 이유는 실제 최상위 목록으로 작성한다. 검증은 `실행한 명령 또는 확인 방법`·`결과` 아래 중첩 목록이며 두 항목 사이와 변경 분류 사이에 빈 줄을 유지한다. 달라진 동작·이유·범위·한계와 실제 검증 방법/결과를 구분한다. 계획 경로는 정확한 WORK 단계/Gate 링크, Issue가 있으면 Refs, 마지막 구현 PR이면 Closes를 연결한다. PR 번호를 제목에 수동 추가하지 않는다.
- 복잡한 분기/상태가 글보다 명확할 때만 표·text tree·Mermaid를 추가한다. 분류/목록/중첩이 이해를 돕는 만큼 사용하고 제목·결과는 간결한 한국어로 쓴다. 원본의 간결한 결과 중심 설명을 유지하되 제품 고유 WP ID는 강제하지 않는다.
- body-file로 제출할 때도 정확한 텍스트 파일과 양식을 사용한다. 올리기 전 전체 diff·의도하지 않은 파일·비밀정보와 실제 head/base를 확인한다.
- 한 세션에 구현·필요 검증을 마치면 Ready가 기본. 여러 세션/인계·다른 작업의 의존·조기 review·실제 CI 중간 검증 필요가 있으면 첫 의미 있는 commit 이후 Draft. Draft는 검증하지 않은 것을 완료로 채우지 않고 Ready 전 실제 결과와 확인 항목을 완성한다.

### PR 형식 자동검사

- [PR Check workflow](../.github/workflows/pr-check.yml)는 PR opened/edited/reopened/synchronize/ready_for_review/converted_to_draft 이벤트에서 실행한다. read-only contents 권한, pinned checkout, 2분 timeout, 동일 PR 실행 취소를 유지한다. WYBU 제품 `tests/*.test.mjs` 대신 [checker 테스트](../tests/pr-check.test.mjs)만 실행하고 [형식 검사](../scripts/pr-check.mjs)로 실제 이벤트 title/body/draft를 검사한다.
- Draft는 제목·heading·요약 card·목록 여백을, Ready는 실제 내용·분류/중첩·이유 목록·검증·4개 확인 항목 완료까지 검사한다. `refactor`는 코팡 허용 type으로 추가했다.
- 이 검사는 작성 사실·소스 정상·WORK 관계·secret·승인을 증명하지 않는다. 등록/실행·실패/통과는 최신 PR head에서 직접 확인한다. 로컬 파일 추가만으로 자동 검사 성공이나 required 보호를 주장하지 않는다.

## 5. 검증과 merge Gate

Ready PR 제출·Ready 전환·merge 전 다음을 실제로 확인한다. 중간 Draft 제출은 이 완료 Gate와 구분하고 실제 진행·미검증·허용 범위·현재 diff/비밀정보를 확인해 미완료 상태를 그대로 알린다.

1. base는 main, head와 변경 범위는 의도한 작업 branch/결과.
2. Ready이며 WORK의 필요한 Task/Gate와 실제 구현·검증이 끝남. 로컬 Gate와 GitHub merge 상태를 혼동하지 않음.
3. 전체 diff와 시크릿 포함 여부, 관련 없는 변경 없음.
4. 해당 변경의 기존 build/test/lint·필요 수동 검증 결과. 기존 실패·미검증·접근 한계를 명시하고 그 영향이 Gate 통과를 막는지 판정.
5. PR 이벤트 자동검사는 최초 PR 제출 뒤 결과를 확인하고 merge 전 의도한 최신 head에서 모두 통과해야 한다. 최초 제출 전 아직 실행될 수 없는 원격 검사를 기다리지 않으며 기존 PR의 Ready 전환에서는 현재 검사 상태/남은 조건을 알린다. 형식 검사 통과가 실제 동작·승인·관계·보안 검증을 대신하지 않음.
6. 미해결 review 의견 없음. 혼자 운영하는 현재 단계에는 존재하지 않는 타인 review를 받았다고 주장하거나 자동 approval하지 않음. 정기 협업자가 생기면 작성자 외 승인과 보호 기준을 별도 설정.
7. 실제 merge 단계에서만 사용자 merge 승인 범위와 remote의 실제 권한/merge 설정을 확인한다. PR까지 요청의 Ready 제출에 merge 승인을 요구하지 않는다. 상태 문서·template 채택만으로 merge를 실행하지 않음.

승인과 Gate가 충족되면 Squash merge, 기본 제목 사용. merge 뒤 정확한 PR/commit과 실제 반영을 확인하며 같은 branch는 재사용하지 않는다. 추가 수정은 최신 main의 새 fix/refactor 등 branch로 시작한다. 운영 영향이 큰 회귀는 승인 범위에서 revert로 먼저 복구하고 별도 수정 PR로 처리한다. 자동 배포·운영 변경 승인은 포함하지 않는다.

## 6. 충돌과 안전 정리

- 다른 작업 변경이 필요하거나 충돌이 생기면 승인된 작업 branch에서 최신 main을 merge해 다시 검증한다. dirty 파일을 보호하고 충돌을 임의 ours/theirs로 덮어쓰지 않는다. rebase/force push로 공유 이력을 바꾸지 않는다.
- worktree는 파일을 분리할 뿐 코드 충돌을 막지 않는다. 작은 결과·명확한 소유권·빠른 검증으로 충돌 범위를 줄인다.
- merge 승인에 포함된 정리는 정확한 PR merge와 미커밋·미전송·미반영 변경 없음부터 확인한다. 관련 없는 작업이나 보존/복구 여부가 불확실한 파일이 있으면 정리를 멈추고 보존한다. 이번 작업의 필요한 ignored 자료는 외부 archive 보존·복구 검증이 끝난 경우에만 해당 작업공간과 함께 제거한다.
- Squash commit tree가 최종 PR head와 같고 기존 local 변경이 모두 반영됐는지 확인한다. 필요한 파일과 복구용 Git bundle·worktree archive는 저장소 밖에 보존하고 primary main을 origin/main과 안전하게 동기화한다. 이번 결과만 정리한 종료 상태는 main/origin/main 동일·clean·작업 refs/worktree 제거로 확인하며 backup branch는 최종 작업 목록에 남기지 않는다. 관련 없는 refs/worktree·외부 검증 자료는 보존하고 reflog expire·복구 불가능한 purge를 하지 않는다.
- 해당 remote branch→Git을 통한 worktree 제거→local branch 정리 순서. managed worktree는 앱의 정리 도구를 사용한다. Finder/rm으로 worktree를 먼저 지우지 않는다.
- Squash 때문에 Git의 일반 merged 판정과 다를 수 있으므로 local branch 강제 삭제가 필요한 경우도 실제 PR merge·모든 변경 반영·외부 복구 자료 검증 및 추가 백업 불필요가 확인된 해당 branch에만 적용한다. 확인되지 않으면 삭제하지 않는다.

## 7. CI·보호·workflow 확장

- 초기 운영 적용에서는 Markdown template만 추가했으나 최신 사용자 보완 요청으로 PR 형식 checker·관련 테스트·단독 workflow를 함께 옮겼다. 제품 build/test CI·Ruleset·Secret·권한 설정은 변경하지 않는다. 자동 검사의 실제 최신 head 결과는 PR에서 확인하고 required 보호와 구분한다.
- WYBU 형식 검사와 관련 테스트는 코팡 type·4개 확인 항목·WORK 링크 관례에 맞춰 적용한다. 원본 workflow의 제품 테스트 glob은 제외하고 checker 테스트만 실행한다. Issue/Work 관계·실제 검증 진실성·승인·merge Gate는 별도 직접 확인한다.
- 코팡의 기존 실제 frontend/Gradle/ML 명령과 재현 가능한 입력을 먼저 확인한다. 안정적인 build/test/lint와 반복 회귀 위험이 확보될 때 그 명령만 최소 CI에 연결한다. 현재 앱에 인증·권한·결제·DB 경계가 있으므로 해당 변경에서 필요한 검증을 미루지 않되 문서 적용으로 실행됐다고 주장하지 않는다.
- 반복 필요별 확장: 정기 협업자→PR 경유만 허용·작성자 외 review 1명·미해결 대화 차단·안정 CI required·main 삭제/force push 차단·서버 Squash only; 안정적인 실행 명령→CI; 반복 bug/feature 혼재→Issue 구분; 우선순위 관리 곤란→label/Project; reviewer 오배정→해당 경로 CODEOWNERS; 자주 동시 merge 대기+지원/안정 CI→merge queue; 실제 배포→tag/release; 동시 여러 배포 버전→release branch; 재현 성능/메모리 문제→targeted profiling/benchmark부터.
- Secret/권한/DB/외부 입력 검증은 규모와 무관하다. credential·manifest/lockfile이 있으면 native push protection·dependency 알림 등 실제 지원·권한을 확인해 별도 적용한다. 원격 보안 설정 변경은 이 규칙을 복사한 것만으로 승인되지 않는다.
- 반복적인 API/DB/config/배포 영향·복구·review 누락이 생기면 그 내용을 담은 확장 PR 양식으로 교체한다. 기존/확장 양식을 동시에 유지하지 않고, Bug/Feature로 교체할 때도 공통 Work 양식을 함께 유지하지 않는다. screenshot·migration·rollout 항목은 실제 반복 필요 때만 추가한다. template을 바꿀 때 자동검사도 있다면 같은 변경에서 맞춘다. merge queue는 지원 조건·여러 사람이 자주 merge·안정적인 required CI·다른 merge로 검사 결과가 빈번하게 stale이 되는 조건을 확인한 뒤 검토한다. 도입 시 Squash·최신 head 검사·merge_group 이벤트를 확인한다. 지원/필요가 부족하면 maintainer가 PR을 순차 merge하고 다음 PR을 최신 main으로 재검증한다. 현재 WYBU의 계정/플랜 지원 판단을 코팡의 현재 사실로 복사하지 않는다.
