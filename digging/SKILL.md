---
name: digging
description: "디깅(Digging)/땅굴 작업 — Phase별 검증 루프로 복잡한 코드 변경, 리팩토링, 문서화, Firestore rules, 배포 전 검증을 안전하게 수행. Use when user says: '디깅으로 진행해', '땅굴 파듯이 천천히 해', 'Phase별로 나눠서 끝까지 해', '검증 루프 돌리고 넘어가', '복잡한 리팩토링을 안정적으로 해'."
---

# Digging Skill Handoff

Digging은 복잡한 코드 변경, 리팩토링, 문서화, Firestore rules, 배포 전 검증처럼 위험도가 있는 작업을 Phase 단위로 천천히 진행하기 위한 실행 스킬이다.

## 사용 시점

사용자가 다음과 같이 요청하면 Digging을 사용한다.

- "디깅으로 진행해"
- "땅굴 파듯이 천천히 해"
- "Phase별로 나눠서 끝까지 해"
- "검증 루프 돌리고 넘어가"
- "복잡한 리팩토링을 안정적으로 해"

## 핵심 절차

1. Context Dig
   - 최신 사용자 요청 확인
   - git status 확인
   - 관련 문서, 계획서, AGENTS.md, CLAUDE.md 확인
   - 관련 코드, 서비스, rules, 테스트, UI flow 확인

2. Phase Map
   - 작업을 작은 Phase로 나눈다.
   - 각 Phase마다 Scope, 수정 대상, 성공 조건, 검증 방법, 위험/롤백 기준을 적는다.

3. Phase Execution
   - 한 번에 한 Phase만 진행한다.
   - 관련 없는 정리나 리팩토링은 하지 않는다.
   - 기존 사용자 변경은 되돌리지 않는다.

4. Two Validation Loops
   - 각 Phase마다 최소 2회 검증한다.
   - Loop 1: 직접 검증, 실패 수정, 재검증
   - Loop 2: 다른 각도에서 재검토, 개선, 재검증

5. Final Validation
   - lint, build, 테스트, Playwright/브라우저 검증, Firestore rules dry-run 등 작업에 맞는 최종 검증을 수행한다.
   - 최종 체크리스트와 성공 조건이 전부 만족될 때까지 반복한다.

## 중단 조건

아래 상황은 사용자 승인 없이 진행하지 않는다.

- 실제 데이터 마이그레이션
- production Firestore rules 배포
- production Vercel 배포
- 기존 데이터를 삭제하거나 되돌리는 작업
- 제품 정책 판단이 필요한 변경
