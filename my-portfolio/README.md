# 작은 관찰

여울의 개인 포트폴리오 겸 블로그입니다. Jekyll로 만들었고 GitHub Pages에서 그대로 배포할 수 있습니다.

## 이 프로젝트 구조

```text
_config.yml       사이트 설정 (제목, 소개, baseurl 등)
_layouts/         공통 레이아웃 (default, post)
_data/projects.yml  프로젝트 목록 데이터
_posts/           글 저장 위치 (지금은 비어 있음)
assets/css/       스타일시트
index.html        홈
posts.html        모든 글 목록
categories.html   카테고리별 글 목록
projects.html     프로젝트 목록과 기록
about.md          소개 페이지
404.html          찾을 수 없는 페이지
```

## 로컬에서 미리 보기 (Docker)

Docker는 **작은 가상 컴퓨터가 아니라, 내 컴퓨터(호스트) 위에서 격리되어 실행되는 하나의 프로세스**입니다.
아래 대응표로 이해하면 쉽습니다.

| 용어 | 이 프로젝트에서의 의미 |
| --- | --- |
| IMAGE | `Dockerfile`로 준비한 실행 패키지 (Ruby + Jekyll이 설치된 상태) |
| CONTAINER | `jekyll` 서비스가 실제로 돌아가는 실행 공간 (격리된 프로세스) |
| VOLUME | `.:/site` — 현재 폴더를 컨테이너 안의 `/site`에 그대로 연결 |
| PORT | `4000:4000` — 브라우저에서 `http://localhost:4000`으로 접속할 수 있게 연결 |

### 실행

```bash
docker compose up --build -d
docker compose ps
```

브라우저에서 `http://localhost:4000` 접속.

문제가 있으면 로그 확인:

```bash
docker compose logs jekyll
```

### 종료

수업(작업)이 끝나면:

```bash
docker compose down
```

## Docker가 없을 때

로컬에 Ruby와 Bundler가 이미 설치되어 있다면:

```bash
bundle install
bundle exec jekyll serve
```

Ruby/Jekyll도 없다면 파일 구조와 Liquid 문법, 내부 링크를 눈으로 검사한 뒤 Docker나 Ruby 환경이 준비되면 위 명령으로 확인하세요.

## 다음 단계: 글 쓰기

`_posts/` 폴더에 아래 형식으로 파일을 추가하면 자동으로 글 목록과 카테고리에 반영됩니다.

파일명 규칙: `YYYY-MM-DD-제목.md`

```markdown
---
layout: post
title: 글 제목
date: 2026-01-01
categories: [카테고리1]
tags: [태그1, 태그2]
summary: 목록에 보일 한두 줄 요약
---

본문 내용을 Markdown으로 작성합니다.
```

## 프로젝트 추가하기

`_data/projects.yml`에 항목을 추가하면 홈(최대 3개)과 `projects.html`에 자동으로 표시됩니다.

```yaml
- title: 프로젝트 이름
  type: 웹 / 디자인 / 글쓰기 등
  status: 아이디어   # 아이디어 / 진행 중 / 완료 중 실제 상태
  summary: 한두 문장 설명
  skills: [사용한 도구나 기술]
  reason: 시작한 이유
  process: 진행 과정
  learned: 배운 점
  # year와 link는 실제 정보가 있을 때만 추가
```

## GitHub Pages 배포 (원할 때 진행)

이 저장소는 아직 공개 배포를 진행하지 않았습니다. 준비가 되면 아래 절차를 따르세요.

1. GitHub에 저장소를 만들고 이 폴더의 내용을 저장소 루트에 올립니다 (`_site`, `.nojekyll`은 올리지 않습니다).
2. 저장소 Settings → Pages → Build and deployment에서 **Deploy from a branch**를 선택합니다.
3. Branch를 게시할 브랜치와 `/(root)`로 지정합니다.
4. 저장소 이름이 `my-portfolio`라면 `_config.yml`의 `baseurl: "/my-portfolio"`를 그대로 사용합니다. 저장소 이름을 `<사용자명>.github.io`로 만든다면 `baseurl`을 빈 문자열로 바꿔야 합니다.
5. 배포된 주소는 `https://<사용자명>.github.io/<저장소 이름>/` 형태입니다. 실제 주소는 GitHub 계정이 연결된 뒤에만 확인할 수 있습니다.

## 참고

- `http://localhost:4000`은 내 컴퓨터에서만 열립니다. 다른 사람에게 이 주소를 공유해도 그 사람 화면에서는 열리지 않습니다.
