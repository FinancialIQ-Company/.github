# FinancialIQ 개발팀 Git 가이드

## Git Flow 브랜치 전략

```
main(master) ─────────────────●─────────────────●──────
                            /                   /
release     ──────────────●───────────────────●────────
                        /                     /
develop     ────●─────●─────────●──────────●───────────
              /     /         /          /
feature    ──●─────●─────────●──────────●──────────────
```

### 브랜치 구성
- `main`: 제품 출시/배포 브랜치
- `release`: QA 및 배포 준비 브랜치
- `develop`: 개발 브랜치
- `feature`: 기능 개발 브랜치
- `hotfix`: 긴급 버그 수정 브랜치

### 브랜치 네이밍 규칙
```
feature: feature/[feature-name]
hotfix: hotfix/[issue-number]
release: release/v[version]
```

## Git 커밋 메시지 컨벤션

### 기본 구조
```
type(scope): subject

body

footer
```

### Type 종류
- `feat`: 새로운 기능 추가
- `fix`: 버그 수정
- `docs`: 문서 수정
- `style`: 코드 포맷팅, 세미콜론 누락 등
- `refactor`: 코드 리팩토링
- `test`: 테스트 코드
- `chore`: 빌드 업무 수정

### Scope 예시
- `auth`: 인증 관련
- `user`: 사용자 관련
- `api`: API 관련
- `core`: 핵심 기능
- `ui`: UI 관련

## 커밋 메시지 예시

### 기능 개발
```
feat(auth): 소셜 로그인 기능 추가

- 카카오 로그인 구현
- 토큰 관리 로직 추가
- 로그인 상태 유지 기능 구현

Resolves: #123
```

### 버그 수정
```
fix(user): 프로필 업로드 오류 수정

- 이미지 크기 검증 로직 수정
- 에러 메시지 개선

Fixes: #456
```

## Git Flow 작업 프로세스

### 1. 기능 개발 (Feature)
```bash
# develop 브랜치에서 feature 브랜치 생성
git checkout develop
git checkout -b feature/user-auth

# 작업 완료 후
git checkout develop
git merge --no-ff feature/user-auth
```

### 2. 릴리즈 준비 (Release)
```bash
# develop 브랜치에서 release 브랜치 생성
git checkout develop
git checkout -b release/v1.2.0

# 버그 수정 및 QA 완료 후 main과 develop에 머지
git checkout main
git merge --no-ff release/v1.2.0
git tag -a v1.2.0
```

### 3. 긴급 수정 (Hotfix)
```bash
# main 브랜치에서 hotfix 브랜치 생성
git checkout main
git checkout -b hotfix/login-crash

# 수정 완료 후 main과 develop에 머지
git checkout main
git merge --no-ff hotfix/login-crash
```

## Pull Request 규칙

### PR 제목 형식
```
[TYPE] 작업 내용 요약
예시: [FEAT] 회원가입 기능 구현
```

### PR 템플릿
```markdown
## 작업 내용
- 구현 내용 설명
- 변경사항 목록

## 테스트 결과
- 테스트 방법
- 테스트 결과

## 참고 사항
- 리뷰어 참고 사항
- 관련 이슈 번호
```

## 코드 리뷰 규칙
1. 최소 1명 이상의 리뷰어 승인 필요
2. PR은 200줄 이내로 제한
3. 24시간 이내 피드백 반영

## Footer 키워드
- `Fixes`: 이슈 수정중
- `Resolves`: 이슈 해결
- `Ref`: 참고 이슈
- `Related to`: 관련 이슈

## 주의사항
1. 커밋 메시지는 한글로 작성
2. 제목은 50자 이내로 제한
3. 본문은 72자 이내로 줄바꿈
4. 제목과 본문은 한 줄 공백으로 구분
5. 제목 끝에 마침표 없음
