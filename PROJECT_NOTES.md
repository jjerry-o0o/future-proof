# Future Proof 블로그 작업 메모

Obsidian으로 글을 작성하고 Quartz로 정적 블로그를 생성해 GitHub Pages에 배포하는 저장소다.

## 저장소와 배포

- GitHub 저장소: `jjerry-o0o/future-proof`
- 기본 브랜치: `main`
- 사이트 주소: <https://jjerry-o0o.github.io/future-proof/>
- 배포 워크플로: `.github/workflows/deploy.yml`

`main` 브랜치에 push하면 GitHub Actions가 `npm ci`와 `npx quartz build`를 실행한 뒤 `public/` 결과물을 GitHub Pages에 배포한다.

GitHub 저장소의 **Settings → Pages → Source**는 `GitHub Actions`여야 한다.

## 주요 경로

| 경로 | 용도 |
| --- | --- |
| `content/` | 블로그에 게시할 Markdown 글 |
| `content/index.md` | 홈페이지 |
| `content/<카테고리>/<글>.md` | 폴더 기반 카테고리와 글 |
| `quartz.config.ts` | 제목, URL, 색상, 폰트, Quartz 플러그인 설정 |
| `quartz.layout.ts` | 사이드바, 검색, 목차, 그래프, 푸터의 배치 |
| `quartz/styles/custom.scss` | 추가 CSS 스타일 |
| `.github/workflows/deploy.yml` | GitHub Pages 자동 배포 |
| `.obsidian/` | 이 저장소를 Obsidian vault로 열 때 쓰는 설정 |

`content/` 이외의 문서는 게시되지 않는다. 작업 메모는 이 파일에 작성한다.

## 글 작성과 분류

글은 `content/` 아래에 Markdown 파일로 만든다. Explorer 사이드바는 폴더 구조를 자동으로 표시한다.

```text
content/
├─ javascript/
│  └─ es5 vs es6, 예제 코드 정리.md
└─ react/
   └─ 상태관리.md
```

태그는 폴더와 별도로 여러 글을 가로질러 분류할 때 사용한다.

```md
---
title: ES5와 ES6 비교하기, 예제 코드 정리
date: 2024-09-04
modified: 2026-08-13
tags:
  - JavaScript
  - ES6
---
```

- `date`: 작성일
- `modified`: 수정일
- 날짜를 생략하면 Git 커밋 날짜 또는 파일 수정 시각이 사용될 수 있다.

헤딩은 순수 Markdown으로 작성한다. 헤딩 안에 `<font>` 같은 HTML 태그를 넣으면 목차에도 태그가 표시될 수 있다.

```md
## ES란?
### let과 const 추가
```

## 로컬 미리보기

`future-proof` 폴더에서 실행한다.

```bash
npx quartz build --serve
```

터미널에 나오는 로컬 주소(일반적으로 `http://localhost:8080`)에서 실제 Quartz 렌더링 결과를 본다. `content/` 또는 스타일 파일을 저장하면 자동으로 다시 빌드된다.

`flexsearch` 관련 파일을 찾을 수 없다는 오류가 나면 의존성을 다시 설치한다.

```bash
npm ci
```

`CustomOgImages: fetch failed` 오류가 나면 `quartz.config.ts`의 아래 줄을 주석 처리한다. 이는 공유용 OG 이미지만 끄며 사이트 표시에는 영향이 없다.

```ts
// Plugin.CustomOgImages(),
```

## 디자인 수정

### 설정과 레이아웃

- `quartz.config.ts`
  - `pageTitle`: 사이트 제목
  - `theme.typography`: 글꼴
  - `theme.colors`: 라이트/다크 테마 색상
  - `Plugin.TableOfContents({ maxDepth: 2 })`: 목차를 H2까지만 표시
- `quartz.layout.ts`
  - `left`: 왼쪽 사이드바
  - `right`: 오른쪽 사이드바(그래프, 목차, 백링크)
  - `footer`: 하단 링크

### 추가 CSS

`quartz/styles/custom.scss`에서 본문과 제목을 조절한다.

```scss
article {
  font-size: 1.1rem;
  line-height: 1.8;
}

article h1,
article h2,
article h3 {
  color: #92cddc;
}

:root[saved-theme="light"] .article-title {
  color: #575757;
}

:root[saved-theme="dark"] .article-title {
  color: #f2f2f2;
}
```

`article h1, h2, h3`로 작성하면 `h2`, `h3`가 본문 밖에도 적용되므로 각 선택자에 `article`을 붙인다.

## 커밋 전 확인

```bash
git status
git add content quartz.config.ts quartz/styles/custom.scss
git commit -m "docs: add JavaScript notes"
git push origin main
```

- `.idea/`: 개인 IDE 설정이므로 커밋하지 않는다. `.gitignore`에 `.idea/`를 추가한다.
- `node_modules/`, `public/`, `.quartz-cache/`, `private/`: 커밋하지 않는다.
- 붙여넣은 이미지가 글에서 사용된다면 `content/attachments/` 같은 위치에 두고 함께 커밋한다.
- `.obsidian/`은 현재 추적 중인 파일이므로, 플러그인 설정 변경을 보존하려는 경우에만 커밋한다.

## 원격 저장소

- `origin`: `https://github.com/jjerry-o0o/future-proof.git`
- `upstream`: `https://github.com/jackyzha0/quartz.git`

별도 Obsidian 메인 vault 백업 저장소는 `jjerry-o0o/obsidian-storage`이며, 이 블로그의 `content/`와는 별도 위치다.
