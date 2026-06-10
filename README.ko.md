# 학술 포트폴리오 — 연구자를 위한 Hugo 템플릿

[English](README.md) · **한국어**

조용하고 종이 질감을 가진 학술 포트폴리오 및 연구 블로그입니다. 소개, 연구 관심분야,
논문, 소식, CV, 그리고 다국어를 염두에 둔 블로그를 담았습니다 — 따뜻한 오프화이트
색조와, 라틴 문자와 한글을 똑같이 정성껏 렌더링하는 이중언어 글꼴 **Chiron GoRound
TC** 와 함께. **Hugo (Extended)** 기반이라 Node.js도 JS 프레임워크도 없고, Hugo
바이너리 외의 빌드 단계가 없습니다.

**[▶ 라이브 데모](https://2ood.github.io/hugo-academic-portfolio/)** &nbsp;·&nbsp;
MIT 라이선스 &nbsp;·&nbsp; 정적 사이트 + GitHub Pages 무료 호스팅

![](static/images/screenshot_front.png)
---

## 왜 이 템플릿인가

- **의존성 최소화.** 빌드는 Hugo 바이너리 하나뿐입니다 — Node도, 번들러도, PostCSS도
  없습니다. 선택적으로 쓰는 콘텐츠 편집기는 의존성 없는 Python 파일 하나입니다.
- **기본 제공되는 다국어 지원.** 영어 + 한국어 데모, 헤더의 언어 드롭다운, 언어별
  콘텐츠와 UI 문자열. 설정에서 언어를 추가하거나 뺄 수 있습니다.
- **템플릿을 건드리지 않고 설정.** 신원 정보, 소셜 링크, 이름이 붙은 색상 팔레트,
  표시할 섹션이 모두 하나의 YAML 파일에 있습니다 — 직접 편집하거나 대시보드에서
  편집합니다.
- **라이트/다크 + 이름이 붙은 팔레트.** 브라우저별로 기억되는 방문자 토글, 로드 시
  깜빡임 없음, OS 설정 존중, CSS 커스텀 속성으로 구현된 4가지 팔레트.
- **브라우저 콘텐츠 대시보드.** 논문·소식·CV·연구 관심분야를 위한 스키마 기반 편집기와,
  이미지를 붙여넣어 업로드하는 분할 마크다운 편집기 — 저장소에 깔끔한 단일 커밋으로
  반영됩니다.
- **무료 호스팅.** `main` 에 푸시할 때마다 GitHub Actions 가 정적 결과물을 압축해
  GitHub Pages 에 게시합니다.

## 구성 요소

| 섹션 | 표시 내용 |
|---|---|
| **홈** | 프로필, 소개, 태그라인, *Selected Publications*(주요 논문) 목록 |
| **연구 관심분야** | 주제별 관심분야 — 각 항목마다 요약과, 관련 논문을 자동으로 나열하는 전용 페이지 |
| **논문(Publications)** | 유형별 필터(Conference / Workshop / Journal / Preprint)와 paper·code·data·project 링크, 수상 내역 |
| **소식(News)** | 날짜와 이모지가 붙은 공지 |
| **CV** | 학력, 수상, 학술 활동, 강의 — 그리고 내려받을 수 있는 PDF |
| **블로그** | 태그·초안·언어별 형제 글·이미지 라이트박스를 지원하는 마크다운 글 |

모든 섹션은 설정에서 끌 수 있으며, 각 섹션은 다국어를 지원합니다.

## 빠른 시작 (약 5분)

**사전 준비물:** [Hugo Extended](https://gohugo.io/installation/) ≥ 0.146 (콘텐츠
어댑터 + 네이티브 Sass). 브라우저 대시보드를 쓰려면 Python 3 도 필요합니다. 테마는
CSS 상대 색상 구문을 사용하므로 방문자는 2023년 이후 브라우저가 필요합니다 (Chrome
119, Safari 16.4, Firefox 128).

1. **템플릿 가져오기** — GitHub 에서 *Use this template* 을 클릭하거나 클론합니다:
   ```bash
   git clone <your-repo-url> && cd <repo>
   ```
2. **개인화** — 한 번의 프롬프트로 `hugo.toml` + `params.yaml` 을 대신 작성해 줍니다
   (이름, 소속, 소셜 링크, 팔레트, Pages URL). 의존성이 없고, 주석과 언어 목록은
   보존됩니다:
   ```bash
   python init.py
   ```
   직접 편집이 더 좋다면 건너뛰고 [나만의 사이트로 만들기](#나만의-사이트로-만들기)를
   보세요.
3. **미리보기** — 편집하는 대로 실시간 새로고침됩니다:
   ```bash
   hugo server        # http://localhost:1313/
   ```
4. **콘텐츠 추가** — 마크다운/YAML 을 직접 편집하거나 대시보드를 사용합니다:
   ```bash
   python cms-server.py   # 그런 다음 http://localhost:8787/ 열기
   ```
   `content/_index.md` 의 데모 소개, `data/en/*.yml` 의 데이터,
   `static/images/profile.svg`, `static/cv.pdf` 를 교체하세요.
5. **배포** — `baseURL` 을 본인의 Pages URL 로 설정한 뒤 푸시합니다. GitHub Actions 가
   Hugo 로 빌드해 자동으로 게시합니다:
   ```bash
   git push origin main
   ```

결과: `https://<you>.github.io/<repo>/` 에 라이브 학술 사이트가 만들어집니다.

> 📖 더 자세히 따라 하고 싶다면 **[QUICKSTART.ko.md](QUICKSTART.ko.md)** 에 전체
> 워크스루가 있습니다 — 첫 배포, 글 작성, 논문/소식/CV 편집, 언어 추가, 대시보드 설정,
> 그리고 자주 하는 실수(예: *브랜치가 아니라 GitHub Actions 로 배포하기*)까지.

## 나만의 사이트로 만들기

직접 편집하는 설정을 원하거나, `init.py` 가 다루지 않는 부분까지 손보려면:

1. **신원 정보 & 구조** — `config/_default/hugo.toml` 에서 `baseURL`, `title`(본인
   이름), 언어 목록을 설정합니다. `config/_default/params.yaml` 에서 `description`,
   `tagline`, 소셜 링크, `palette`, `sections` 토글을 설정합니다.
2. **콘텐츠** — `data/<lang>/*.yml`(publications, news, cv, research_interests)의
   자리표시 데이터, `content/_index.md` 의 소개, `content/blog/` 의 데모 글을
   교체합니다. `static/images/profile.svg` 와 `static/cv.pdf` 도 본인 것으로 바꿉니다.
3. `hugo server` 로 **미리보기** 한 뒤 `main` 에 푸시해 배포합니다.

### 설정 레퍼런스 (`config/_default/params.yaml`)

| 키 | 용도 |
|---|---|
| `description` | 이름 아래 표시되는 소속 줄 |
| `tagline` | 홈 페이지의 한 줄 요약 |
| `faviconEmoji` | 파비콘으로 쓰는 이모지 (기본값 🌲) |
| `profileImage` | `static/` 아래 프로필 이미지 경로 |
| `email`, `googleScholar`, `github`, `linkedin` | 소셜 링크 |
| `cvPdf` | `static/` 아래 CV PDF 경로 |
| `palette` | `forest` · `slate` · `crimson` · `plum` (`assets/scss/_theme.scss` 참고) |
| `sections` | 섹션별 불리언: `research`, `publications`, `blog`, `news`, `cv` |

`description`/`tagline` 의 언어별 재정의는 `config/_default/hugo.toml` 의
`[languages.<lang>.params]` 아래에 둡니다.

### 언어 추가

1. `config/_default/hugo.toml` 의 `[languages]` 아래에 `[languages.<lang>]` 블록을 추가합니다.
2. `i18n/en.toml` 을 `i18n/<lang>.toml` 로 복사하고 값을 번역합니다.
3. `data/<lang>/*.yml` 을 추가합니다 (`data/en/` 에서 복사 — 슬러그와 상호 링크가
   안정적으로 유지되도록 `title` 키는 동일하게 두고, 본문만 번역합니다).
4. `<name>.<lang>.md` 콘텐츠 형제 파일(예: `_index.<lang>.md`)과, 논문·연구 관심분야
   섹션을 위한 `_content.<lang>.gotmpl` 을 추가합니다.
5. 대시보드가 새 언어의 콘텐츠를 편집할 수 있도록 `static/admin/admin.js` 의 `LANGS`
   를 갱신합니다.

### 색상 & 테마

팔레트는 `assets/scss/_theme.scss` 에 CSS 커스텀 속성 묶음으로 정의되어 있습니다.
소유자가 선택한 `palette` 는 `<html>` 에 `data-palette` 를 설정하고, 방문자의 라이트/
다크 선택은 `data-theme` 를 설정합니다. 팔레트를 추가하려면 `[data-palette="name"]`
블록을 추가하고 `static/admin/admin.js` 의 `PALETTES` 에 이름을 넣습니다.

## 콘텐츠 대시보드 (`/admin/`)

![](static/images/screenshot_dashboard.png)

콘텐츠를 편집하는 두 가지 방법:

1. **직접** — 마크다운/YAML 을 편집하고 커밋합니다.
2. **대시보드** — 편집기를 제공하고 **로컬** git 저장소에 커밋하는, 의존성 없는 Python
   백엔드입니다 (준비되면 한꺼번에 푸시):

   ```bash
   python cms-server.py     # 그런 다음 http://localhost:8787/ 열기
   ```

   **콘텐츠 언어 선택기**(우측 상단)로 각 언어의 데이터와 글을 편집합니다. **Settings**
   탭은 `config/_default/params.yaml`(팔레트, 섹션, 소셜 링크)을 편집합니다. 로컬
   서버는 루프백 요청만 받습니다.

   편집 내용은 하나씩 커밋되지 않고 **브라우저에 스테이징** 됩니다: 각 편집기의 저장
   버튼이 변경을 기록하고, 내비게이션 바의 단일 **Commit (N)** 버튼이 전체 묶음을 **하나
   의** 커밋으로 반영합니다 (대기 중인 변경이 있을 때만 나타납니다). 편집기는 항상
   스테이징된(아직 커밋되지 않은) 작업을 반영하며, 대기 중인 변경이 있는 상태로 페이지를
   떠나거나 로그아웃하려 하면 경고합니다 — 히스토리를 깔끔하게 유지합니다.

   각 콘텐츠 편집기에는 다른 언어의 콘텐츠를 가져와 번역본을 *지금 편집 중인 편집기로*
   불러오는 **⤳ Translate from …** 버튼이 있습니다 (그래서 다른 편집과 똑같이 검토하고
   저장합니다 — 스스로 커밋하지 않습니다). 무료이고 키가 필요 없는
   [MyMemory](https://mymemory.translated.net) 서비스를 사용합니다 (클라이언트 측이라
   로컬과 Pages 모두에서 동작). 본문만 번역하고 — 제목·저자·게재처·URL·슬러그는 고정 —
   마크다운을 보호하며, *비어 있는* 필드만 채우므로 직접 편집한 내용은 절대 덮어쓰지
   않습니다. 결과물은 검토용 초안으로 다루세요 (LLM 이 아닌 일반적인 기계 번역입니다).

   대시보드를 GitHub Pages 에서 제공할 때는, 저장소로 범위가 한정된 **fine-grained
   토큰**(Contents: read/write)을 사용해 GitHub API 로 커밋하는 방식으로 대체됩니다.
   로그인 화면에서 **Authorize with GitHub** 를 클릭하면 GitHub 토큰 페이지가 미리
   채워진 채 열리며, 발급한 토큰을 붙여넣습니다. 소유자/저장소는 Pages URL 에서
   감지됩니다 (커스텀 도메인은 `static/admin/admin.js` 의 `OWNER`/`REPO` 를 재정의).
   토큰 만료를 짧게 설정하세요 — 대시보드도 저장된 토큰을 2일 뒤 스스로 만료시킵니다.
   대시보드의 팔레트, 라이트/다크 모드, UI 언어는 헤더에서 조정할 수 있습니다.

## 배포

`main` 에 푸시하면 `.github/workflows/deploy.yml` 이 트리거되어 Hugo Extended 로
빌드하고 `public/` 을 GitHub Pages 에 게시합니다. 먼저 `config/_default/hugo.toml` 의
`baseURL` 을 본인의 Pages URL 로 설정하세요.

## 프로젝트 구조

```
config/_default/  hugo.toml (구조적 설정) + params.yaml (소유자 편집용)
content/          마크다운 페이지 + 글; 데이터 기반 섹션은 _content.<lang>.gotmpl 로 생성
data/<lang>/      언어별 구조화 콘텐츠 (publications, news, cv, interests)
i18n/             UI 문자열 번들 (en.toml, ko.toml, …)
layouts/          Go 템플릿 — 셸, 섹션별 뷰, 파셜, 렌더 훅
assets/scss/      main.scss 진입점, _variables.scss, _theme.scss 토큰, 컴포넌트별 파셜
assets/js/        main.js (빌드 시 캐시 무효화를 위해 핑거프린팅)
static/           이미지, cv.pdf, 그리고 /admin 대시보드
```

## 문서

- [QUICKSTART.ko.md](QUICKSTART.ko.md) — 자주 하는 작업을 위한 단계별 워크스루
- [CHANGELOG.md](CHANGELOG.md) — 주요 변경 사항
- [ROADMAP.md](ROADMAP.md) — 방향과 아이디어

## 라이선스

[MIT](LICENSE). 이 템플릿으로 무언가를 만든다면 템플릿으로 돌아오는 출처 링크를 남겨
주시면 감사하지만, 필수는 아닙니다.
