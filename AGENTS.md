# Application writing: multi-agent entrypoint

이 프로젝트의 자기소개서 요청은 메인 멘토가 아래 절차로 실행한다. 이 저장소는 지원서 스킬의 관리 원본과 실행 역할, 인계 순서를 함께 정의한다. 설치된 스킬의 지침 중 동일 에이전트 전환 방식은 이 프로젝트에서 아래 실제 서브에이전트 방식으로 수행한다. 사실·개인정보·문체 규칙은 유지한다.

## 실행 계약

지원서 관련 여섯 스킬의 관리 원본은 이 저장소의 skills/ 아래에 있다: application-form-writer, application-experience-entry-writer, pm-drama-upgrade-mentor, application-prework-strategist, company-role-researcher, application-writing-motivation-mentor. 이 프로젝트에서는 skills/<스킬명>/SKILL.md와 그 상대 참조를 읽고, 서브에이전트에도 해당 관리 원본 경로를 전달한다. 관련 외부 스킬은 설치되어 있고 현재 요청에 필요한 경우만 사용한다. 누락된 선택 스킬은 사용했다고 주장하지 않는다.

메인의 역할과 결정권은 [agents/main.md](agents/main.md), 역할별 스킬 매핑은 [agents/roles.md](agents/roles.md)를 따른다. 실제 호출 방식과 모델은 [docs/dispatch.md](docs/dispatch.md), 호출 조건·병렬화·재작업은 [docs/schedule.md](docs/schedule.md), 검수는 [docs/review.md](docs/review.md)가 기준이다. 인계 형식과 자료 규칙은 docs/handoff.md 및 docs/sources.md를 읽는다.

메인은 단계 담당 서브를 생성하고 writer-coordinator 총괄은 agents/writer-coordinator.md에 따라 전용 문항 에이전트 또는 범용 A/B 자식을 생성할 수 있다. 그 외 자식의 재위임과 별도 사용자 작업(create_thread) 생성은 금지한다. 같은 문서 동시 쓰기를 금지하고 사용자 질문은 메인에 모은다. 전문 스킬의 내부 실행 순서가 이 프로젝트의 역할 분리와 겹치면 메인의 인계 범위를 따른다. 작성 기법은 스킬에 두고 프로젝트 파일에 반복 복제하지 않는다.

## 완료와 실패 처리

각 작성 턴을 마치기 전에 [실행 QA](docs/execution-qa.md)를 적용한다. 작성 품질 리뷰와 실제 실행·저장 검증은 별개다. 실행 가능한 저장 작업을 '저장하겠다'는 최종 답변만 남기고 종료하지 않는다.

스킬이나 소스 접근이 없으면 이름과 미확인 범위를 메인에 반환한다. 검색 결과 없음과 권한 실패를 구분한다. 실패한 결과를 근거로 삼지 않고, 가능한 분석을 유지하며 필요한 조치만 사용자에게 요청한다. timeout 뒤 동일 외부 쓰기를 반복하기 전 실제 저장 상태를 확인한다. 문서 저장 성공이나 원문 학습 완료는 실제 확인한 경우에만 보고한다.

개인 원문·공고 원문·회사 내부 자료·인증정보는 Git에 넣지 않는다. 필요하면 gitignored `private/` 아래에서만 작업한다. 공개 저장소에는 일반화된 규칙과 합성 예제만 둔다. 이 프로젝트에서 다른 프로젝트의 스킬을 임의 수정하지 않는다.
