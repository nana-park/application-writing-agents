# 요청 분기와 모델 실행

## Agent와 skill의 구분

이 프로젝트의 작성·재작성·첨삭 요청은 main → 실제 subagent 도구 호출로 실행한다. 스킬 로드는 에이전트에게 작업 지침을 주는 행위이며 에이전트 생성이 아니다. 에이전트마다 역할과 작업 ID를 만들고 생성 도구가 반환한 ID로 결과를 기다린다. ID 없는 역할 서술은 실행으로 보고하지 않는다.

- `자소서 써줘`, `지원동기 써줘`, 공고 맞춤 작성·전면 재작성: 입력 확보 후 실제 역할 에이전트를 실행한다.
- 지원서 연구·논문·특허·프로젝트·담당업무 입력란용 정리: Main이 양식과 기존 경험을 확인하고 writer-coordinator에 application-experience-entry-writer 적용을 지시한다. 자소서 A/B·전체 기업조사는 재실행하지 않으며 작성자는 기본 한 안을 반환한다. Main이 요청된 Notion 회사별 토글 저장·재조회를 담당한다. 채용 사이트 실제 입력 요청만 application-form-writer로 연결한다.
- 초안의 특정 문장 교정: main이 맥락을 유지하며 writer-coordinator에 해당 구간만 맡긴다. 모든 조사를 다시 돌리지 않는다.
- 구조 설명·상태 질문·파일 정리: 작성 에이전트를 불필요하게 생성하지 않는다.
- 스킬 자체 개선·EDUCE 학습: 작성 작업과 구분하여 별도 요청 범위에서 처리한다.
- 상위 취업준비 프로젝트에서는 상위 AGENTS.md의 자기소개서 진입 규칙으로 이 실행 계약을 읽는다. 그 외 프로젝트는 명시적으로 이 파일을 읽거나 이 폴더를 프로젝트로 연다. 글로벌 설치 스킬의 자동 선택 설정을 임의로 바꾸지 않는다.

## 모델

- Main: 사용자가 선택한 UI 모델 `GPT-6 Astra Light`. Light와 API reasoning low의 대응은 확인되지 않았으므로 low로 자동 변환하지 않는다.
- 리뷰어 reviewer-it-hr와 reviewer-it-service-planning: `gpt-6-astra`, reasoning `medium`.
- 그 외 subagent: `gpt-5.6-sol`, reasoning `medium`.
- 메인의 모델은 Codex 작업의 모델 설정이다. 이 문서를 읽거나 spawn_agent를 호출하는 것만으로 현재 메인 모델은 바뀌지 않는다. 새 작업 시작 시 사용자가 원하는 UI 모델을 선택한다. 실제 설정을 확인할 수 없으면 원하는 설정과 확인된 실행 상태를 구분한다.
- 하위 에이전트는 생성 호출에서 model과 reasoning_effort를 명시한다. 현재 collaboration 도구는 모델 override와 fork_turns=all을 함께 지원하지 않으므로 fork_turns=none을 쓰고 필요한 맥락을 인계문에 명시한다. 런타임이 다르면 실제 도구 스키마를 확인한다.

현재 런타임 호출 예시(자동 실행 코드나 별도 서비스가 아님):

```json
{
  "task_name": "prework",
  "fork_turns": "none",
  "model": "gpt-5.6-sol",
  "reasoning_effort": "medium",
  "message": "역할, 필수 스킬 절대 경로, JD·문항, 소스 범위, 인계 버전, 읽기/쓰기 권한, 반환 형식과 완료 조건을 여기에 전달"
}
```

완료된 에이전트 재사용 시 원래 모델 설정을 유지한다. 원하는 모델을 사용할 수 없으면 임의의 다른 모델로 실행했다고 숨기지 말고 불가 범위를 알린다. 사용자에게 agent ID/역할, 요청한 모델, 작업 상태를 필요 시 보고하되 요청한 모델을 별도로 검증된 실제 백엔드 모델이라고 주장하지 않는다.

리뷰어 생성 시 task_name은 해당 reviewer 키, model은 gpt-6-astra, reasoning_effort는 medium, fork_turns는 none으로 지정한다. 이전 Sol 리뷰 인스턴스는 그대로 재사용하지 않고 Astra로 새로 생성한다. 파일 설정 변경만으로 실행 중인 모델이 바뀌었다고 보고하지 않는다.
