---
date: '2025-05-24T21:27:01+09:00'
draft: false
title: 'Hugo 블로그 만들기'
ShowToc: true
TocOpen: true
---

## Velog는 뭔가 부끄러웠다.

취업 전에도 살짝, 취업 후에도 동기들과 “블로그 쓰기 내기”를 하며 또 살짝—두 번이나 Velog에 글을 올린 적이 있다.
하지만 어느 순간부터 자연스럽게 손이 멀어졌다. Velog는 왠지 “사람들 앞에 전시되는 공간” 같아서, 글 한 줄 쓰기가 괜히 부끄러웠다. 그래서 블로그 대신 Obsidian으로 공부 내용을 조용히 정리하는 편을 택했다.

그러다 최근, 다시 글을 공개적으로 남기고 싶어졌다.
개인 공부는 계속 Obsidian에 쌓더라도, 경험담이나 삽질 기록 같은 건 블로그에 남겨 두고 싶었다. 마침 “직접 호스팅”도 해보고 싶어서 정적 사이트 생성기를 찾아봤는데, Hugo·Jekyll·Gatsby 중에서 결국 Hugo가 가장 눈에 들어왔다. 마크다운 기반이라 옮기기도 편할 것 같고, 복잡하게 파고들기보다 **일단 ‘써보고 배우자’** 라는 마음으로 시작했다.

이 공간은 말 그대로 내 아지트다. 맘껏 뻘글도 쓰고, 공부도 하고, 장난감 프로젝트도 전시할 예정이다.
그리고 그 첫 장난감이 바로 지금 보고 있는 이 블로그다.

## Hugo 블로그 작성하기

> - 환경
>   - Macbook Pro 14 (Apple M1 Pro)
>     - macOS 15.5
> - 참고 자료
>   - [Hugo 공식 문서](https://gohugo.io/documentation/)
>   - [Hugo Quick Start](https://gohugo.io/getting-started/quick-start/)

### 0. Hugo 설치하기

Homebrew를 사용하여 Hugo를 설치한다.

설치가 완료되면 `hugo version` 명령어로 설치된 버전을 확인할 수 있다.  
개인적으로는 뭘 깔던 처음에는 `--help`를 쳐보는 편이다.

```shell
brew install hugo

hugo version
hugo --help
```

명령어가 꽤 많이 출력된다.

![hugo help 명령어](/images/hugo-help-command.png)

### 1. 사이트 생성하고, 테마 설치하기

Quick Start를 따라 사이트를 생성해보자. `hugo new site {사이트 이름}` 명령어를 사용한다.  
hugo의 기본 파일은 `.toml`로 생성된다.
개발자들은 대체로 `.json` 또는 `.yaml`을 선호할테니, `--format` 옵션으로 파일 형식을 바꿔보자.
 
```shell
hugo new site some-blog --format yaml
cd some-blog
ls -al # 생성된 디렉토리 확인, 뭔가 많이 생겼을거다.
```

이후에는 테마를 설치해보자. 먼저 마음에 드는 테마를 찾아야 한다.
테마는 [Hugo Themes](https://themes.gohugo.io/)에서 찾아볼 수 있다.
quick start에 나온 대로 ananke 테마를 설치해보자.
theme는 git 서브모듈로 설치하도록 가이드 되어 있기 때문에, 먼저 site 디렉터리로 이동해서 `git init`을 실행하고 submodule을 추가한다.
`~/some-blog` 디렉토리에서 아래 명령어를 실행한다.

```shell
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
echo "theme: ananke" >> hugo.yaml
hugo server # 내장 서버로 실행
```

정상적으로 실행이 됐다면, `http://localhost:1313` 주소로 접속해서 블로그를 확인할 수 있다.  
- *기본적으로 1313 포트로 실행되나, 이미 해당 포트를 사용중이라면 다른 포트로 실행된다.*
- *만약 포트를 직접 지정하고 싶다면 `hugo server --port 1414`와 같이 실행하면 된다.*

![blog-첫-실행](/images/ananke-theme-blog.png)

### 2. 첫 글 작성하기

이제 첫 포스트를 작성해보자.

```shell
hugo new content content/posts/my-first-post.md
```

생성된 `/content/posts/my-first-post.md`에는 아래와 같은 내용이 작성되어 있다.

```markdown
---
date: '2025-05-24T22:19:04+09:00'
draft: true
title: 'My First Post'
---
```

포스트를 처음 작성하면 draft 상태로 작성된다.
draft 글은 기본적으로 블로그에 표시되지 않는다.
포스트 작성을 완료했다면, `draft: false`로 변경해주자. 그래야 블로그에 표시가 된다.
작성중인 포스트를 블로그에 표기하고 싶다면, `draft: true` 상태로 두고, `hugo server --buildDrafts` 명령어로 서버를 실행하면 된다. (또는 `hugo server -D`)

방금 생성한 포스트를 블로그에서 확인할 수 있다.

![첫글-작성하기](/images/hugo-first-post.png)

이제 포스트를 원하는 내용으로 작성하는데 markdown 형식이니 [Markdown Guide](https://www.markdownguide.org/basic-syntax/)를 참고해 작성하면 된다.
아마 개발자라면 markdown을 많이 사용해봤을테니, 크게 어려움은 없을 것이다.

*TMI: 보통 vscode를 markdown 편집기로 많이 사용하는 것 같은데, 나는 Jetbrains를 사랑해서 WebStorm으로 작성중이다.*

![WebStorm 마크다운 에디터](/images/webstorm-markdown-editor.png)

### 3. 블로그 배포하기

블로그 배포는 여러 방법이 있다.
GitHub Pages, Vercel, Netlify 등 다양한 호스팅 서비스를 이용할 수도 있고, 직접 서버를 구축해서 배포할 수도 있다.
호스팅 서비스를 사용하면 간단하게 배포도 가능하고 관리도 편하다.

> “직접 호스팅”도 해보고 싶어서...

도입부에 썼던 이 말은 직접를 구축해서 배포한다는 의미였다. 나만의 아지트를 당근에서 업어온 작고 소중한 맥미니에 배포해보자.

맥미니는 이미 기본적인 구성이 되어있다.
포트 포워딩을 설정해놨고 [Caddy](https://caddyserver.com/)를 사용해서 HTTPS도 설정해서 웹 서버를 구성해놨다.
특정 directory에 빌드된 파일을 복사하기만 하면 된다.

hugo는 `hugo` 명령어로 빌드하고 `public` 디렉터리에 빌드된 파일을 생성한다.
이 `public` 디렉터리를 맥미니의 웹 서버가 접근할 수 있는 디렉터리로 복사해주면 된다.

```shell
hugo --minify
ls # public 디렉터리 확인
scp -P {port} -r public {user}@{host}:{path-to-web-server-directory}
```

이정도만 해도 충분히 편하긴 한데, 뭔가 개발자스럽지 못하다.
직접 빌드하고 배포하는 과정을 자동화 하고싶다.
블로그를 작성만 하면 자동으로 빌드되고 배포되면 멋질 것 같다.
GitHub Actions를 사용해서 자동 배포를 해보자.

`.github/workflows/deploy.yml` 파일을 생성하고 아래와 같이 작성한다.

```yaml
name: hugo-blog-deploy

on:
  push:
    branches:
      - master

# 동시에 실행되는 action을 방지한다.
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v2
        with:
          submodules: true
          fetch-depth: 0

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: 'latest'

      - name: Build Hugo site
        run: hugo --minify

      - name: Upload artifact
        uses: actions/upload-artifact@v4
        with:
          name: hugo-public
          path: ./public

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Download build artifact
        uses: actions/download-artifact@v4
        with:
          name: hugo-public
          path: ./public

      - name: Deploy via SCP
        uses: appleboy/scp-action@v1
        with:
          host: ${{ secrets.SSH_HOST }}
          username: ${{ secrets.SSH_USERNAME }}
          password: ${{ secrets.SSH_PASSWORD }}
          port: ${{ secrets.SSH_PORT }}
          source: "./public"
          target: ${{ secrets.TARGET_PATH }}
          rm: true
```

GitHub에 push를 하면 자동으로 빌드를 하고, 빌드가 성공한다면 `public` 디렉터리를 지정한 서버의 지정한 경로로 복사하게 된다.
딱히 설명이 필요 없을 것 같다.

private repository를 사용한다면 크게 상관이 없을 수는 있지만,
public repository를 사용하거나 추후에 public으로 옮겨갈 가능성이 있다면,
**서버의 민감한 정보들은 직접 코드에 작성하지 말고 GitHub Secrets에 저장해두자.**

![github-action-시행착오](/images/hugo-github-actions-try.png)

오타나 잘못된 설정으로 약간의 시행착오가 있었지만, 성공적으로 배포를 했다.

그럼 여기까지 배포 우선 끝!

## 마무리

Velog 시절에는 '누군가 보는 공간'이라는 압박 때문에 글쓰기가 쉽지 않았지만,
직접 호스팅하니 좀 더 마음이 편해졌다.
덕분에 **개발 메모, 뻘글, 뻘짓**을 마음껏 쌓아둘 아지트가 간단하게 구성된 것 같다.

글에서 언급했던 맥미니 홈서버는 어떻게 구성했는지 조만간 적어봐야겠다.