# AIssue

**GitHub 저장소와 이슈를 분석해 오픈소스 기여를 돕는 AI 웹서비스**입니다. 2025년 한국소프트웨어저작권협회(SPC)의 생성형 AI 기반 실용 웹서비스 개발자 양성과정에서 Mai-Nova 팀이 개발했습니다.

프로젝트 기획·개발과 발표는 2025년 4~6월에 진행했고, 일부 수정은 7월까지 이어졌습니다. 당시 사용한 서버와 자동 배포는 현재 종료한 상태입니다. 저장소는 코드·문서·협업 기록을 담은 포트폴리오로 남겨 두었습니다.

## 주요 기능과 구조

- GitHub 로그인, 저장소 탐색·등록·북마크, README 요약
- 저장소 코드 수집·분할, Gemini 임베딩과 FAISS 검색을 이용한 관련 코드 탐색
- 이슈 분석과 해결 제안, 저장소 문서를 문맥으로 활용한 질의응답
- 인덱싱 진행 상태와 완료·실패 처리, 분석 결과 화면

```mermaid
flowchart LR
    U[사용자] --> R[React]
    R --> E[Express API]
    E <--> D[(MySQL)]
    E --> G[GitHub API]
    E --> F[Flask 분석 API]
    F --> G
    F --> M[Gemini API]
    F <--> V[(FAISS)]
    F -->|완료·실패 콜백| E
```

웹 기능은 Express에서, AI 분석은 Flask에서 처리합니다. 코드 검색 RAG와 문서 기반 질의응답은 별도로 동작하며, 질의응답에는 문서를 직접 문맥으로 전달합니다.

## 저장소와 자료

| 자료 | 내용 |
|---|---|
| [AIssue-BE-Flask](https://github.com/c99-dev/AIssue-BE-Flask) | 코드 인덱싱, 임베딩·검색, AI 분석 API |
| [AIssue-BE-Express](https://github.com/c99-dev/AIssue-BE-Express) | 웹 API, DB, GitHub 및 AI 분석 연동 |
| [AIssue-FE-React](https://github.com/c99-dev/AIssue-FE-React) | 사용자 화면과 분석 결과 표시 |
| [AIssue-Overview](https://github.com/c99-dev/AIssue-Overview) | 프로젝트 안내와 전체 이슈 |
| [AIssue-Meeting-Minutes](https://github.com/c99-dev/AIssue-Meeting-Minutes) | 기획·기술 선택·역할 분담 회의록 |
| [AIssue-Team-Profile](https://github.com/c99-dev/AIssue-Team-Profile) | 팀 소개, 아키텍처·ERD, 원본 발표자료 |

- [프로젝트 보드](https://github.com/users/c99-dev/projects/3)
- [Overview Wiki](https://github.com/c99-dev/AIssue-Overview/wiki) · [Express Wiki](https://github.com/c99-dev/AIssue-BE-Express/wiki)
- [팀 소개와 발표 PDF](https://github.com/c99-dev/AIssue-Team-Profile/blob/main/profile/README.md)
- [시연 영상](https://www.youtube.com/watch?v=ps95XQiVXHI)

## 담당한 부분

| 작업 | 관련 PR |
|---|---|
| Flask RAG·임베딩과 검색 | [Flask #6](https://github.com/c99-dev/AIssue-BE-Flask/pull/6), [#22](https://github.com/c99-dev/AIssue-BE-Flask/pull/22) |
| 인덱싱의 백그라운드 처리와 상태 전달 | [Flask #8](https://github.com/c99-dev/AIssue-BE-Flask/pull/8), [#27](https://github.com/c99-dev/AIssue-BE-Flask/pull/27) |
| Express 저장소·이슈·AI 분석 연동 | [Express #27](https://github.com/c99-dev/AIssue-BE-Express/pull/27), [#41](https://github.com/c99-dev/AIssue-BE-Express/pull/41) |
| GitHub Actions 배포 구성과 React 결과 화면 | [React #11](https://github.com/c99-dev/AIssue-FE-React/pull/11), [#41](https://github.com/c99-dev/AIssue-FE-React/pull/41), [#55](https://github.com/c99-dev/AIssue-FE-React/pull/55) |

인덱싱은 요청 처리와 분리해 백그라운드 스레드에서 실행하고, 진행 상태를 반환하도록 구현했습니다. 프로세스 내부 스레드를 사용한 구현이며, 영속 작업 큐나 프로세스 재시작 후 작업 복구까지는 보장하지 않습니다.

## 팀원

Mai-Nova는 **최성호(c99-dev), 민유진(gnxm37), 김지은(Pracrobo), 나상현(Soberanalysts)** 네 명이 함께한 팀입니다. 민유진은 로그인·JWT 인증·결제를, 김지은은 분석 완료 알림·DB ERD 등을 담당했습니다. 역할 분담과 작업 과정은 발표자료와 각 저장소의 commit·PR·회의록에 남아 있습니다.

## 저장소 이전

2026년 9월 8일 Mai-Nova 조직에 있던 저장소 6개를 `c99-dev` 계정으로 이전했습니다. Git 이력과 issue·PR·review, Wiki는 그대로 유지했고, 문서 저장소 두 개는 찾기 쉬운 이름으로 바꿨습니다. 라이선스는 각 저장소의 기존 LICENSE를 따릅니다.
