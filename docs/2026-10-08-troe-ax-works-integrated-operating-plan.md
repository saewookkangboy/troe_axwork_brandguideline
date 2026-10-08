# TROE × AX WORKS 통합 운영 및 웹사이트 이관 계획

> 기준일: 2026-10-08
> 상태: 문서화 완료 · 구현 전 검증 단계

## 1. 결정 요약

TROE와 AX WORKS를 서로 경쟁하는 두 브랜드로 운영하지 않는다.

- **TROE**는 법인·대표·콘텐츠·사례·도서를 묶는 마스터 브랜드다.
- **AX WORKS by TROE**는 AX 진단부터 설계·실행·교육·운영까지 연결하는 상업 서비스 브랜드다.
- **`troe.kr`**은 모든 고객 여정의 대표 허브로 전면 리뉴얼한다.
- GitHub는 코드·콘텐츠·변경 이력의 대표본, Vercel은 Preview·Production 배포의 대표본으로 사용한다.
- 기존 호스팅과 DNS는 새 사이트 검증 전까지 유지하며, DNS 전환은 마지막에 수행한다.

## 2. 목표 사이트 구조

```text
troe.kr
├── /ax-works      AX WORKS 서비스 허브
├── /cases         사례와 Evidence Library
├── /insights      재구성된 블로그·리서치
├── /books         도서와 TROE 방법론의 연결
├── /about         TROE와 박충효 소개
└── /contact       단일 문의·개인정보 동의

연결 자산
├── ax.allrounder.im     AX 준비도·ROI 진단
├── book.allrounder.im   도서 캠페인
├── park.allrounder.im   박충효 포트폴리오
└── gaeo.allrounder.im   GAEO 제품·실험
```

`ax.allrounder.im`은 1차 이관에서 유지한다. `diagnose.troe.kr` 같은 TROE 하위 도메인으로 옮길지는 전체 허브 안정화 이후 판단한다. `axworks.kr`과 `axworks.im`은 소유권·DNS·대표 도메인 결정 전까지 대외 대표 주소로 확정하지 않는다.

## 3. AX WORKS 서비스 체계

| 단계 | 서비스 | 고객이 얻는 것 |
| --- | --- | --- |
| 1 | Diagnose | AX 준비도·ROI·우선 과제 진단 |
| 2 | Blueprint | 업무·데이터·사람·승인 구조 설계 |
| 3 | Sprint 90 | 핵심 업무 1개를 90일 안에 가동 |
| 4 | Academy | 리더·실무자·빌더 역량 전환 |
| 5 | Operate | 지표·예외·승인·거버넌스 운영 |
| 6 | GAEO | 생성형 검색·콘텐츠 실험과 제품화 |

모든 서비스는 `진단 → 설계 → 실행 → 역량 → 운영`의 단일 여정으로 설명한다. Gate Line은 시각 장식이 아니라 근거 확인, 브랜드 승인, 법무·개인정보 확인, QA, 배포 승인의 실제 운영 절차로 사용한다.

## 4. 블로그 재구성 원칙

기존 글을 일괄 삭제하거나 새 URL로 무조건 바꾸지 않는다. 먼저 전체 URL을 수집한 뒤 아래 네 가지로 분류한다.

| 결정 | 기준 | URL 처리 |
| --- | --- | --- |
| 유지·업데이트 | 현재도 유효하고 고유한 가치가 있음 | 기존 slug 유지 우선 |
| 전면 재작성 | 주제는 유효하지만 내용·수치·화면이 낡음 | 검색 의도가 같으면 slug 유지 |
| 통합 | 유사 주제가 여러 글에 분산됨 | 대표 글로 합치고 나머지는 301 |
| 종료 | 시의성이 끝났고 대체 가치가 없음 | 가장 가까운 글이나 주제 허브로 301 |

새 콘텐츠는 다음 네 기둥으로 운영한다.

1. **AX 실행** — 준비도, 진단, 로드맵, 변화관리, 운영체계
2. **AI 마케팅** — AI Agent, GEO·AIEO, 콘텐츠·광고·CRM 자동화
3. **조직 역량** — 리더십, 실무자 교육, Responsible AI, 검증 습관
4. **TROE Proof** — 사례, 파트너십, 도서, 강연, 방법론

글마다 핵심 답변, 실행 단계, 검증 출처, 관련 서비스, 관련 글·도서·포트폴리오, 단일 CTA를 포함한다.

## 5. GitHub·Vercel 운영 방식

이 저장소는 브랜드 원칙·목업·기획 문서를 보존하는 **브랜드 시스템 저장소**로 유지한다. 운영 사이트는 별도 저장소 `troe-web`을 권장한다.

```text
작업 브랜치
  → GitHub Pull Request
  → Vercel Preview
  → 브랜드·콘텐츠·기능 Gate QA
  → main 병합
  → Vercel Production
  → troe.kr
```

- 운영 사이트는 Next.js App Router·TypeScript·MDX 구성을 기본안으로 한다.
- 블로그·사례·도서는 MDX 콘텐츠 대표본으로 관리한다.
- 리다이렉트, sitemap, robots, canonical, JSON-LD, OG 규칙을 코드로 관리한다.
- 문의 수신 정보와 운영 환경변수는 GitHub에 저장하지 않는다.
- 브랜드 가이드의 대용량 HTML 내보내기와 목업은 운영 번들에 포함하지 않는다.

## 6. 단계별 실행

### Phase 0 · 현행 보존

- 호스팅·등록기관·DNS·분석·문의 계정 소유권 확인
- 전체 DNS Zone과 기존 사이트·블로그·이미지·메타 백업
- 전체 URL과 상태 코드 수집

### Phase 1 · 정보 구조와 URL 맵

- `troe.kr`의 새 메뉴와 페이지 책임 확정
- 블로그 전수 감사와 301 매핑
- AX WORKS 서비스명·근거·CTA 승인

### Phase 2 · GitHub·Vercel 기반

- `troe-web` 저장소와 Vercel 프로젝트 생성
- 핵심 페이지 템플릿과 브랜드 토큰 구현
- PR별 Preview와 `main` Production 연결

### Phase 3 · 콘텐츠 이관

- 기존 글을 MDX로 보존 이관
- 상위 유입 글과 핵심 기둥 글부터 재작성
- 관련 서비스·도서·포트폴리오 연결

### Phase 4 · 통합 페이지

- Home, AX WORKS, Cases, Insights, Books, About, Contact 완성
- 문의 실전송·성공·실패·개인정보 동의 구현

### Phase 5 · Preview QA

- 모든 새 URL 200, 구 URL 단일 301
- self-canonical, sitemap, robots, OG, JSON-LD 확인
- 모바일 390px, 키보드, 폼 실수신, 분석 이벤트 검증

### Phase 6 · DNS 전환

- 전환 24~48시간 전 웹 레코드 TTL 하향
- Vercel 프로젝트가 제시한 실제 DNS 값만 적용
- MX·SPF·DKIM·DMARC 보존
- 기존 호스팅 7~14일 병행

### Phase 7 · 안정화

- Search Console sitemap 제출
- 404, 리다이렉트 체인, 폼, 색인, 전환 점검
- 안정화 이후 기존 호스팅 종료 판단

## 7. 현재 로컬 배포 후보

아래 파일은 2026-10-08 기준 로컬 작업 트리에 존재하지만 아직 Git에 포함하지 않았다.

| 파일 | 상태 | 판단 |
| --- | --- | --- |
| `index.html` | TROE 메인 목업 | `website-mockup.html`과 SHA-256 동일 |
| `website-mockup.html` | TROE 메인 목업 | 중복 후보. 대표 파일 확정 필요 |
| `ax-works.html` | AX WORKS 서브페이지 | 서비스 체계 반영 후 운영 후보 |
| `robots.txt` | 크롤링 설정 | 대표 도메인 확정 후 검증 필요 |
| `sitemap.xml` | URL 목록 | 실제 라우팅 확정 후 재생성 필요 |
| `favicon.svg`, PNG·OG 자산 | 브랜드 자산 | 크기·명도·메타 렌더 검증 필요 |

이 파일들은 이번 문서 업데이트 커밋에 포함하지 않는다. 운영 대표본, URL, 폼, 법적 문서, 수치 근거를 승인한 뒤 별도 구현 커밋으로 다룬다.

## 8. 배포 차단 항목

현재 목업을 그대로 배포하지 않는다.

- `index.html`과 `website-mockup.html`이 완전 중복이다.
- 문의 폼이 `action="#"`이라 실제 전송되지 않는다.
- 소셜 링크와 개인정보처리방침·이용약관이 `href="#"`이다.
- Organization 구조화 데이터의 `sameAs`가 비어 있다.
- 20년·21년·`2016—2026` 경력 표기가 서로 충돌한다.
- `ax@allrounder.im`과 `chunghyo@troe.kr` 문의 주소가 혼재한다.
- `axworks.kr`, `axworks.im`, `ax.allrounder.im`의 대표 역할이 문서마다 다르다.
- 고객사 로고·성과 수치·환급률·시장 수치는 Evidence Library 승인 전 공개하지 않는다.

## 9. 완료 기준

- 전체 기존 URL에 200 또는 의도한 단일 301이 있다.
- 블로그 감사표와 URL별 처리 결정이 있다.
- GitHub `main`이 운영 코드·콘텐츠 대표본이다.
- 모든 PR에 Vercel Preview가 생성된다.
- TLS, 대표 도메인, sitemap, robots, canonical, JSON-LD가 검증된다.
- AX 진단·도서·박충효 포트폴리오·GAEO 링크가 동작한다.
- 문의 폼 실수신과 분석 이벤트를 확인한다.
- 기존 호스팅을 7~14일 병행할 수 있는 DNS 롤백 문서가 있다.

## 10. 이번 문서화 범위

이번 업데이트는 통합 운영 방향과 실행 순서를 GitHub 저장소에 기록하는 작업이다. 운영 사이트 생성, Vercel 프로젝트 생성, DNS 변경, 기존 호스팅 종료는 수행하지 않았다.
