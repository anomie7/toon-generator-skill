# TODO

## 병렬화

### Phase 1: toon-prep

- [ ] **Doc-Gen Wave 내 병렬화**
  - Wave 1 문서 4종 (`character-sheet.md`, `character-concept.md`, `art-direction.md`, `character-sheet-detailed.md`) 동시 생성
  - Wave 2 문서 2종 (`emotion-chart.md`, `bgm-guide.md`) 동시 생성
  - Wave 3 EP별 `conti/EP{N}.md` + `episode-design/EP{N}.md` 동시 생성
  - 현재: doc-generator 에이전트 내부에서 순차 생성
  - 구현 방향: doc-generator 에이전트에 Wave별 병렬 생성 지시 명시

- [ ] **레퍼런스 이미지 카테고리 병렬 생성**
  - character / background / tone-master 3카테고리 동시 생성
  - 현재: `generate-refs.ts`에서 7장을 순차 생성
  - 구현 방향: `generate-refs.ts`에서 `Promise.all`로 카테고리별 병렬 호출

### Phase 3: toon-reels

- [ ] **EP 파이프라인화**
  - EP1 릴스 인코딩과 EP2 이미지 생성을 겹치게 실행
  - 현재: toon-run이 EP1 이미지 → EP1 릴스 → EP2 이미지 → EP2 릴스 순서로 순차 실행
  - 구현 방향: toon-run 오케스트레이터에서 EP{N} 이미지 완료 시 EP{N} 릴스와 EP{N+1} 이미지를 동시 시작

---

## 워크플로우 강제

- [ ] **슬라이드 A→B 단계 파일 기반 강제**
  - 현재: A(요소 정의), B(reference-explorer 호출)는 SKILL.md 지시로만 강제
  - 구현 방향: `slide-plan.json`에 요소 정의 + 선정 ref 경로를 저장하고, `pipeline-slide.ts`가 해당 파일을 필수 입력으로 요구 → A, B를 건너뛰면 스크립트 실행 불가

---

## 기타

- [ ] `toon-run` 스킬 테스트 (test-minimax에서 전체 파이프라인 수동 검증)
- [ ] `refactor/workflow-enforcement` 브랜치 → main 머지 및 PR 생성
