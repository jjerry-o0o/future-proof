# Future Proof 작업 노트

Obsidian으로 글을 작성하고 Quartz로 정적 블로그를 배포하는 저장소다.
이 파일은 블로그 콘텐츠가 아니며, 사람과 AI 에이전트가 작업할 때 참고한다.

## 저장소와 배포

- GitHub 저장소: `jjerry-o0o/future-proof`
- 기본 브랜치: `main`
- 사이트 주소: `https://jjerry-o0o.github.io/future-proof/`
- 배포 방식: GitHub Pages + GitHub Actions
- 워크플로우: `.github/workflows/deploy.yml`

`main`에 푸시하면 GitHub Actions가 다음을 수행한다.

1. `npm ci`로 의존성 설치
2. `npx quartz build`로 사이트 생성
3. `public/` 결과물을 GitHub Pages에 배포

GitHub 저장소 설정의 **Settings → Pages → Source**는 `GitHub Actions`여야 한다.

## 작성자 정보

이 저장소의 로컬 Git 작성자 정보는 다음과 같다.

- 이름: `jjerry-o0o`
- 이메일: `alfndp25@gmail.com`

## 주요 경로

| 경로 | 용도 |
| --- | --- |
| `content/` | 블로그에 게시되는 Markdown 글 |
| `content/index.md` | 사이트 홈 화면 |
| `quartz.config.ts` | 사이트 제목, 주소, 언어, 플러그인 등의 Quartz 설정 |
| `quartz.layout.ts` | 페이지 레이아웃 설정 |
| `.github/workflows/deploy.yml` | GitHub Pages 자동 배포 워크플로우 |
| `.obsidian/` | Obsidian 로컬 설정 |
| `PROJECT_NOTES.md` | 이 작업 안내 문서. 블로그에는 게시되지 않음 |

Quartz는 `content/` 폴더만 블로그 콘텐츠로 처리한다. 저장소 루트의 문서는 배포 사이트에 올라가지 않는다.

## 글 발행 흐름

1. Obsidian에서 `content/` 안에 `.md` 글을 만든다.
2. 필요하면 YAML 프론트매터를 작성한다.
3. 저장 후 Git 변경 사항을 커밋한다.
4. `main`으로 푸시한다.
5. GitHub Actions의 `Deploy Quartz site to GitHub Pages` 성공 여부를 확인한다.

예시:

```md
---
title: 첫 글
date: 2026-07-27
tags:
  - 기록
---

글 내용
```

## 자주 쓰는 명령

```bash
# 의존성 설치
npm i

# 로컬 빌드
npx quartz build

# Git 상태 확인
git status

# 글 또는 설정 변경 발행
git add <파일>
git commit -m "설명"
git push origin main
```

## 주의 사항

- `content/index.md`가 없으면 홈 화면용 HTML이 생성되지 않아 RSS XML이 루트에 표시될 수 있다.
- `node_modules/`, `public/`, `.quartz-cache/`, `private/`는 Git 추적 대상이 아니다.
- 민감한 메모는 `private/`에 둔다. Quartz 설정과 Git 규칙에서 게시 및 추적 대상에서 제외된다.
- GitHub 토큰, 비밀번호, API 키는 이 저장소나 이 문서에 기록하지 않는다.
- Quartz 원본 원격은 `upstream` (`https://github.com/jackyzha0/quartz.git`)이며, 개인 저장소 원격은 `origin`이다.
