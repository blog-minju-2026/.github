# 한채

한 사람이 한 채의 집을 짓고, 그 안에 기록을 쌓고, 이웃의 집을 찾아가는 블로그 서비스.

티스토리처럼 회원마다 블로그 하나를 열어 글을 쓰고, 마을(첫 화면) · 찾기 · 이웃으로 다른 블로그의 글을 발견하고, 댓글 · 공감 · 방명록으로 어울린다. 블로그를 집 한 채로, 블로그들이 모인 곳을 마을로 본다. 글은 집 안의 방에 쌓이고, 같은 주제의 글은 마을의 골목에 모인다.

🏠 **사이트** · [hanchae.java21.net](https://hanchae.java21.net) &nbsp;|&nbsp; 📝 **바뀐 내용** · 사이트의 '릴리즈' 버튼(`/releases`), 지금 판 1.12.0 (2026-11-23)

## 한채의 말

| 한채에서 | 흔히 부르는 이름 |
| --- | --- |
| 한채 | 블로그 |
| 마을 | 첫 화면. 모든 한채의 공개 기록이 모이는 곳 |
| 대문 · 현판 | 블로그 첫 화면 · 블로그 이름 |
| 마당 | 한 블로그의 글 목록 |
| 기록 | 글 |
| 방 · 마루 | 블로그 안의 카테고리 · 카테고리 없음 |
| 골목 | 마을 전체의 주제 (10개) |
| 이웃 | 구독 |
| 방명록 | 방명록 |

## 할 수 있는 것

- **들어오기** — 이메일로 가입하거나 카카오 · 구글 · 네이버로 로그인한다
- **한채 짓기** — 주소 · 현판 · 주인 소개를 정하면 대문이 생긴다
- **기록 쓰기** — 사진, 방, 골목, 태그, 공개 범위(공개 · 이웃 공개 · 나만 보기)를 고른다. 쓰는 동안 저절로 임시저장된다
- **마을 둘러보기** — 골목별 기록, 새 기록, 이웃 소식, 지금 많이 읽는 기록(매 정각 갱신), 북적이는 한채
- **찾기** — 마을 전체 또는 한 한채 안에서 기록과 한채를 찾는다
- **이웃과 어울리기** — 공감, 댓글, 방명록, 이웃 맺기
- **내 한채 꾸리기** — 한채 관리, 방 관리, 기록 · 댓글 · 이웃 관리, 내 정보
- **마을 지키기** — 서비스 관리자는 기록 · 댓글 숨김과 회원 이용 제한으로 마을을 지킨다

## 이렇게 만든다

[GitHub Spec Kit](https://github.com/github/spec-kit)의 흐름(constitution → specify → clarify → plan → tasks → implement)을 따른다. 팀 통합 기능명세서를 기준으로 [spec.md](https://github.com/blog-minju-2026/blog-docs/blob/main/specs/001-blog/spec.md)를 쓰고, 코드는 그 요구사항 ID로 거슬러 올라갈 수 있게 만든다.

지키는 원칙 ([constitution](https://github.com/blog-minju-2026/blog-docs/blob/main/.specify/memory/constitution.md)):

1. **명세가 먼저다** — 명세에 없는 기능은 만들지 않고, 달라져야 하면 명세를 먼저 고친다
2. **권한은 서버가 지킨다** — 모든 요청을 API에서 권한표로 검사하고, 볼 수 없는 글은 404로 존재를 숨긴다
3. **기본이 안전하다** — 입력은 이스케이프하고, 본문은 허용 목록으로 정제하고, 상태를 바꾸는 요청은 CSRF로 지킨다
4. **데이터는 언제나 맞는다** — 연달아 눌러도 한 번만 처리하고, 여러 단계 작업은 한 트랜잭션으로 묶는다
5. **테스트로 확인한다** — 수용 시나리오마다 자동 테스트를 두고, 기능과 테스트를 같은 PR에 넣는다
6. **단순하게 만든다** — 정적 HTML + 빌드 없는 JavaScript + JSON API. 화면 프레임워크와 번들러를 쓰지 않는다

## 저장소

| 저장소 | 내용 |
| --- | --- |
| [blog-code](https://github.com/blog-minju-2026/blog-code) | 화면 · Django API · 배포 |
| [blog-docs](https://github.com/blog-minju-2026/blog-docs) | 기능명세서 · API 명세서 · Spec Kit 문서(spec · plan · data-model · tasks) |

## 만든 재료

| 영역 | 쓰는 것 |
| --- | --- |
| 화면 | HTML · CSS · JavaScript (프레임워크 없이, 디자인 시스템 「한채」, 직접 만든 에디터) |
| 서버 | Python 3.12 · Django 5.2 · Django REST framework · django-allauth · nh3 |
| DB | MySQL 8 (ERD 는 Crowfoot 「한채 블로그 플랫폼」) |
| 테스트 | Django 테스트 러너 · DRF `APITestCase` (PR 마다 GitHub Actions 로 실행) |
| 배포 | Docker · gunicorn · nginx · GitHub Actions (main 에 합치면 학교 서버로 무중단 자동 배포) |
