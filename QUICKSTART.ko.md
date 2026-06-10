# 빠른 시작 & 워크스루

[English](QUICKSTART.md) · **한국어**

자주 하는 작업을 차근차근 따라 할 수 있는 안내서입니다. [README](README.ko.md#빠른-시작-약-5분)
에 30초 요약판이 있고, 여기는 자세한 버전입니다. 처음이라면 **첫 배포**부터 시작하세요.

## 목차

1. [첫 배포: 제로부터 라이브까지](#1-첫-배포-제로부터-라이브까지)
2. [`python init.py` 동작 방식](#2-python-initpy-동작-방식)
3. [블로그 글 작성](#3-블로그-글-작성)
4. [논문, 소식, CV 편집](#4-논문-소식-cv-편집)
5. [언어 추가](#5-언어-추가)
6. [대시보드에서 설정하기](#6-대시보드에서-설정하기)
7. [자주 하는 실수와 주의점](#7-자주-하는-실수와-주의점)

---

## 1. 첫 배포: 제로부터 라이브까지

**사전 준비물:** [Hugo Extended](https://gohugo.io/installation/) ≥ 0.146 (*Extended*
빌드가 반드시 필요합니다 — 테마의 Sass 를 컴파일합니다. 일반 Hugo 는 실패합니다). Git,
GitHub 계정, 그리고 브라우저 대시보드를 쓰려면 Python 3.

1. **템플릿으로 본인 저장소 만들기.** GitHub 에서 **Use this template → Create a new
   repository** 를 클릭합니다. (또는 클론한 뒤 `origin` 을 본인 저장소로 바꿔도 됩니다.)
   ```bash
   git clone https://github.com/<you>/<repo>.git && cd <repo>
   ```

2. **개인화.** 설정 프롬프트를 실행하면 이름, 소속, 소셜 링크, 팔레트, Pages URL 을
   설정 파일에 대신 써 줍니다 (자세한 내용은
   [§2](#2-python-initpy-동작-방식)):
   ```bash
   python init.py
   ```

3. **로컬 미리보기.** Hugo 가 편집하는 대로 실시간 새로고침합니다:
   ```bash
   hugo server          # http://localhost:1313/
   ```

4. **데모 콘텐츠 교체** (*Joomo Makguli* 페르소나). 최소한 다음을 바꾸세요:
   - `content/_index.md` — 본인 소개 (언어별로 `_index.<lang>.md`)
   - `data/<lang>/*.yml` — publications, news, cv, research_interests
   - `static/images/profile.svg` — 본인 사진 (아무 이미지나; `profileImage` 갱신)
   - `static/cv.pdf` — 본인 CV PDF
   직접 편집하거나 대시보드를 사용하세요 ([§3](#3-블로그-글-작성),
   [§4](#4-논문-소식-cv-편집)).

5. **커밋하고 `main` 에 푸시.**
   ```bash
   git add -A && git commit -m "chore: personalize template" && git push
   ```

6. **Pages 켜기 — 브랜치가 아니라 GitHub Actions 로.** 저장소에서:
   **Settings → Pages → Build and deployment → Source: _GitHub Actions_.**
   이 템플릿은 `.github/workflows/deploy.yml` 을 포함하며, `main` 에 푸시할 때마다
   Hugo Extended 로 빌드해 게시합니다. 진행 상황은 **Actions** 탭에서 볼 수 있으며,
   첫 실행은 1~2분 걸립니다.

   > ⚠️ 대신 *Deploy from a branch* 를 선택하면 GitHub 가 원시 저장소 파일(또는
   > 존재하지 않는 `gh-pages` 브랜치)을 서빙하려 해서 깨진 사이트나 404 가 나옵니다.
   > Source 는 **반드시** *GitHub Actions* 여야 합니다.
   > [§7](#7-자주-하는-실수와-주의점) 참고.

이제 설정한 `baseURL` — 보통 `https://<you>.github.io/<repo>/` — 에서 사이트가 라이브
됩니다. 이후 `main` 에 푸시할 때마다 다시 배포됩니다.

---

## 2. `python init.py` 동작 방식

`init.py` 는 의존성이 없고 재실행 가능한 개인화 도구입니다. 두 파일 —
`config/_default/hugo.toml` 과 `config/_default/params.yaml` — 에 **수술적인(surgical)**
편집을 가해, 소유자 편집용 값만 바꾸고 주석·구조·언어 목록은 그대로 둡니다.

저장소 루트에서 실행하세요:

```bash
python init.py
```

각 값을 물어보며 현재 값을 대괄호로 보여 줍니다 — **그대로 두려면 Enter** 를 누릅니다:

| 프롬프트 | 기록 위치 | 비고 |
|---|---|---|
| Your name (site title) | `hugo.toml` `title` | 사이트 제목으로 표시 |
| GitHub username | — | 선택; 아래 URL 들을 제안하는 데만 사용 |
| Repository name | — | username 과 합쳐 `baseURL` 제안 |
| Site baseURL | `hugo.toml` `baseURL` | 기본값 `https://<user>.github.io/<repo>/` |
| Affiliation / description | `params.yaml` `description` | 이름 아래 줄 |
| Tagline | `params.yaml` `tagline` | 홈 페이지의 한 줄 |
| Email | `params.yaml` `email` | |
| Google Scholar URL | `params.yaml` `googleScholar` | |
| GitHub URL | `params.yaml` `github` | 기본값 `https://github.com/<user>` |
| LinkedIn URL | `params.yaml` `linkedin` | |
| Favicon emoji | `params.yaml` `faviconEmoji` | 기본값 🌲 |
| Color palette | `params.yaml` `palette` | `forest` / `slate` / `crimson` / `plum` |

편집이 수술적이고 Enter 로 유지되므로, 나머지를 건드리지 않고 값 하나만 바꾸고 싶을
때 언제든 다시 실행할 수 있습니다. 콘텐츠·언어·언어별 재정의는 **건드리지 않습니다** —
그쪽은 수동입니다 ([§5](#5-언어-추가) 참고).

---

## 3. 블로그 글 작성

글은 `content/blog/` 에 있습니다. 기본 언어 글은 `slug.md`, 각 번역본은
`slug.<lang>.md` 입니다 (예: `welcome.md` + `welcome.ko.md`).

### 대시보드 사용 (권장)

```bash
python cms-server.py     # 그런 다음 http://localhost:8787/ 열기
```

1. 작성할 **콘텐츠** 언어를 (우측 상단에서) 선택합니다.
2. **Blog → New post.** 제목, 파일명(슬러그; 비워 두면 제목에서 자동 생성), 날짜,
   태그, 초안 플래그, 설명을 채웁니다.
3. **분할 마크다운 편집기**로 작성합니다 — 오른쪽은 소스, 왼쪽은 실시간 미리보기.
4. **`Ctrl+V` 로 이미지 붙여넣기.** 이미지는 해시되어 `static/images/uploads/` 에
   업로드되고, 커서 위치에 루트 기준 `![](/images/uploads/…)` 링크가 삽입됩니다. 사이트
   에서는 클릭하면 확대되는 라이트박스로 열립니다. (붙여넣은 이미지는 즉시 커밋되고,
   텍스트 편집은 스테이징됩니다 — 아래 참고.)
5. **Save post** — 변경을 *스테이징* 합니다. 편집을 마치면 내비게이션 바의
   **Commit (N)** 버튼을 눌러 전체를 **하나의** 커밋으로 반영합니다. 로컬 모드에서는
   로컬 저장소에 커밋되므로 `git push` 를 잊지 마세요.

### 직접 작성

`content/blog/<slug>.md` 를 프런트매터와 마크다운 본문으로 만듭니다:

```markdown
---
title: Welcome to Brewhouse
date: 2025-01-01T09:00:00Z
tags:
  - meta
draft: false
description: First placeholder post — replace with your own.
---

**마크다운**으로 작성하세요. 목록, 코드 블록, 인용문, 표가 모두 적절한 타이포그래피로
렌더링됩니다.
```

`draft: true` 로 설정하면 프로덕션 빌드에서 글이 숨겨집니다 (`hugo server -D` 는 로컬
에서 초안을 보여 줍니다). 번역본은 `<slug>.<lang>.md` 로 복사하고 본문을 번역하세요 —
언어 전환기가 둘을 연결하도록 같은 슬러그를 유지합니다.

---

## 4. 논문, 소식, CV 편집

이 섹션들은 `data/<lang>/` 아래의 **데이터 파일**로, 직접 편집하거나 대시보드의 스키마
기반 편집기(같은 YAML 을 작성합니다)로 편집합니다. 모두 언어별이므로 편집 전에
**콘텐츠** 선택기를 바꾸세요.

### 논문 (`data/<lang>/publications.yml`)

항목들의 목록입니다. 저자 줄에서 본인 이름을 굵게 표시하려면 **본인 이름**을
`**별표 두 개**`로 감싸세요.

```yaml
- title: Learning Robust Brews from Limited Nuruk
  authors: '**Joomo Makguli**, Bo-ri Lee, Han Saemi'
  venue: BrewNIPS
  year: 2025
  type: Conference          # Conference | Workshop | Journal | Preprint
  selected: true            # 홈 페이지의 "Selected Publications" 에 표시
  award: Outstanding Pour Award
  interest: Fermentation Dynamics   # 연구 관심분야 title 과 정확히 일치해야 함
  paperUrl: https://example.com/paper
  codeUrl: https://github.com/example/repo
  dataUrl: https://example.com/dataset
  projectUrl: https://example.com/project
  abstract: 이 논문 전용 페이지의 본문으로 렌더링됩니다.
```

- `type` 은 Publications 페이지의 필터 탭을 결정합니다.
- `selected: true` 는 홈 페이지 목록에 논문을 노출합니다.
- `interest` 는 논문을 연구 관심분야 페이지에 상호 링크합니다 — 값이 해당 관심분야의
  `title` 과 **정확히** 일치해야 합니다 (언어 간 title 유지에 관해서는
  [§5](#5-언어-추가) 참고).

### 소식 (`data/<lang>/news.yml`)

최신순 정렬은 템플릿이 처리합니다(날짜 기준 정렬). `text` 는 인라인 마크다운 링크를
지원합니다.

```yaml
- date: 2025-09-15
  icon: 🎉                  # 대시보드의 이모지 선택기에서 고르거나, 아무 이모지나
  text: Our paper was accepted to [BrewNIPS 2025](https://example.com).
```

### CV (`data/<lang>/cv.yml`)

네 개의 선택 섹션 — `education`, `awards`, `service`, `teaching` — 이며, 존재할 때만
렌더링됩니다:

```yaml
education:
  - institution: Jumak National University
    degree: Ph.D. in Fermentation Science
    advisor: Advised by Prof. Nuruk
    period: 2023 - Present
awards:
  - title: Outstanding Pour Award, BrewNIPS
    year: 2025
service:
  - role: Reviewer
    detail: BrewNIPS, ICML, ICLR (2024 - 2025)
teaching:
  - course: Introduction to Makgeolli (MG200)
    role: Teaching Assistant
    institution: Jumak National University
    period: 2024
```

내려받을 수 있는 PDF 는 `static/cv.pdf` 입니다 (`params.yaml` 의 `cvPdf` 가 경로를 지정).

### 연구 관심분야 (`data/<lang>/research_interests.yml`)

각 항목은 `/research-interests/<슬러그화된-title>/` 페이지가 됩니다. `details` 는
마크다운이며 페이지 본문으로 렌더링되고, `interest` 가 `title` 과 일치하는 논문이 그
페이지에 자동으로 나열됩니다.

```yaml
- title: Fermentation Dynamics
  summary: 홈과 섹션 페이지에 표시되는 한 줄 요약.
  details: |
    마크다운 한두 문단. **굵게**, [링크](/publications/), 목록을 쓸 수 있습니다.
```

대시보드에는 블로그와 동일한 목록 + 분할 마크다운 편집기를 가진 **Research Interests**
탭이 있습니다.

---

## 5. 언어 추가

템플릿은 영어(기본) + 한국어 데모를 함께 제공합니다. `<lang>` 을 추가하려면:

1. **언어 선언** — `config/_default/hugo.toml` 의 `[languages]` 아래:
   ```toml
   [languages.<lang>]
     label = "Native name"     # 헤더 드롭다운에 표시
     locale = "<lang>"
     weight = 3
     [languages.<lang>.params]
       description = "…"        # 선택적 언어별 재정의
       tagline = "…"
   ```
2. **UI 문자열 번역:** `i18n/en.toml` 을 `i18n/<lang>.toml` 로 복사하고 값을 번역합니다.
3. **데이터 추가:** `data/en/` 을 `data/<lang>/` 로 복사하고 본문을 번역합니다.
   기본 언어와 **`title` 키를 동일하게 유지하세요** — 슬러그와 `interest` 상호 링크가
   title 로 매칭되므로, 바꾸면 링크가 깨집니다.
4. **콘텐츠 형제 파일 추가:** 각 페이지마다 `<name>.<lang>.md`
   (예: `_index.<lang>.md`, `content/blog/<slug>.<lang>.md`)와, 논문·연구 관심분야
   섹션을 위한 `_content.<lang>.gotmpl` 을 추가합니다 (기존 것을 복사해 로직은 두고
   `data/<lang>` 경로만 바꿉니다).
5. **대시보드에 알리기:** `static/admin/admin.js` 의 `LANGS` 배열에 `<lang>` 을 추가해
   콘텐츠 선택기가 제공하도록 합니다.

`hugo server` 로 미리 보고 헤더 드롭다운으로 언어를 전환하세요.

---

## 6. 대시보드에서 설정하기

대시보드의 **Settings** 탭은 YAML 을 직접 편집하지 않고 `config/_default/params.yaml`
을 편집합니다. 다루는 항목:

- **신원 & 소셜:** `description`, `tagline`, `email`, `googleScholar`, `github`,
  `linkedin`.
- **외형:** `faviconEmoji`, `profileImage`, `palette`.
- **`cvPdf`:** `static/` 아래 CV 경로.
- **섹션:** `research`, `publications`, `blog`, `news`, `cv` 를 켜고 끕니다 — 내비게이션
  탭과 홈 페이지 섹션을 함께 제어합니다.

Settings 탭으로 **바꿀 수 없는** 것 (`config/_default/hugo.toml` 을 직접 편집):
**이름/사이트 제목**, **baseURL**, **언어 목록**. Settings 저장은 `params.yaml` 을 다시
쓰며 **주석을 제거합니다** — 의도된 동작입니다.

> 대시보드 자체의 외형 — 팔레트, 라이트/다크, UI 언어 — 은 헤더에서 설정하며, 사이트
> 방문자 테마와는 독립적입니다.

**로컬 vs Pages 모드.** 로컬에서 `python cms-server.py` 를 실행하면 루프백을 통해 로컬
git 저장소에 커밋합니다(토큰 불필요). 반대로 대시보드를 GitHub Pages 에서 서빙하면,
붙여넣은 **fine-grained PAT**(Contents: read/write)로 GitHub API 를 통해 커밋합니다 —
**Authorize with GitHub** 를 클릭하면 토큰 페이지가 미리 채워진 채 열립니다. 만료를 짧게
설정하세요; 대시보드도 저장된 토큰을 2일 뒤 스스로 만료시킵니다.

---

## 7. 자주 하는 실수와 주의점

- **브랜치가 아니라 GitHub Actions 로 배포하세요.** Pages **Source** 는 *GitHub
  Actions* 여야 합니다 (Settings → Pages). *Deploy from a branch* 를 고르면 원시
  파일이나 존재하지 않는 `gh-pages` 브랜치를 서빙해 깨진/404 사이트가 됩니다.
  ([§1](#1-첫-배포-제로부터-라이브까지))
- **`baseURL` 은 저장소 경로와 일치해야 하고 끝의 슬래시를 유지해야 합니다.** 프로젝트
  사이트라면 `https://<you>.github.io/<repo>/` 입니다. 잘못되었거나 슬래시가 없는
  `baseURL` 은 CSS·링크·이미지를 깨뜨립니다 (모든 것이 이를 기준으로 해석됩니다).
- **Hugo _Extended_ 를 쓰세요.** 테마가 Sass 를 네이티브로 컴파일하므로 일반 Hugo
  바이너리는 오류가 납니다. 콘텐츠 어댑터를 위해 ≥ 0.146 이 필요합니다.
- **로컬 대시보드에서 저장한다고 배포되는 게 아닙니다.** 로컬 편집은 **로컬** 저장소에
  커밋됩니다 — 빌드를 트리거하려면 여전히 `git push` 가 필요합니다.
- **언어 간 `title` 키를 동일하게 유지하세요.** 슬러그와 논문↔관심분야 상호 링크가
  title 로 매칭되므로, title 을 번역하면 그 링크가 조용히 깨집니다. 키가 아니라 본문을
  번역하세요. ([§5](#5-언어-추가))
- **`interest` 는 연구 관심분야 `title` 과 정확히 일치해야** 논문이 관심분야 페이지에
  연결됩니다 (대소문자·공백 구분).
- **Settings 저장은 YAML 주석을 제거합니다.** 대시보드가 `params.yaml` 을 다시 쓰므로,
  그 파일의 주석에 메모를 남겨 두면 저장 시 사라집니다.
- **Pages CDN 은 HTML 을 약 10분 캐시합니다.** 배포 후 변경을 보려면 강력 새로고침(또는
  몇 분 대기)이 필요할 수 있습니다 — 빌드 실패가 아니라 GitHub 의 캐시입니다.
- **방문자는 2023년 이후 브라우저가 필요합니다.** 테마가 CSS 상대 색상 구문을 사용합니다
  (Chrome 119, Safari 16.4, Firefox 128).
- **PAT 는 브라우저에만 저장됩니다.** 커밋하지 마세요; 주된 안전장치로 GitHub 만료를
  짧게 두는 편을 권합니다.
