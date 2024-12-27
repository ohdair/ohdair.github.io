---
title: Obsidian 사용자의 블로그 자동 포스팅(with Hugo)
date: 2024-12-27
lastmod: 2024-12-27
aliases: 
tags: 
author: 
description: 
summary: Obsidian에서 정리한 기록을 온라인으로 공유하려고 했습니다. 하지만 다른 플랫폼에 내용을 복사해서 붙여넣는 과정이 번거롭고, 글이 제대로 적용되지 않는 경우가 있어 이를 자동화하는 방법을 고민했습니다. 그래서 GitHub Pages를 활용해 효율적으로 기록을 공유하려는 계획을 세웠습니다.
cover: 
relative: false
editPost: 
showToc: true
---
## 나의 기록 Obsidian
저는 `Obsidian`이라는 앱을 통해 학습한 내용이나 감명 깊었던 책의 내용을 정리하고 기록합니다. 단순히 기억에 의존하기보다 글로 정리함으로써 흐릿해질 수 있는 정보를 명확히 남기고자 하는 목적입니다.

개발자가 되겠다는 목표를 세운 후, 부트캠프와 독학을 병행하며 깨달은 점이 있습니다. 혼자 성장하는 것도 의미 있지만, 마음 맞는 사람들과 함께 성장할 때 더 많은 것을 배우고 시간도 절약된다는 점입니다. 함께한다는 것은 서로 교차 검증을 통해 더 나은 방법을 찾고, 잘못된 점을 수정하며 성장할 기회를 제공합니다.

이러한 경험을 바탕으로 `Obsidian`에서 정리한 기록을 온라인으로 공유하려고 했습니다. 하지만 다른 플랫폼에 내용을 복사해서 붙여넣는 과정이 번거롭고, 글이 제대로 적용되지 않는 경우가 있어 이를 자동화하는 방법을 고민했습니다. 그래서 **GitHub Pages**를 활용해 효율적으로 기록을 공유하려는 계획을 세웠습니다.

## GitHub Pages
GitHub에서 제공하는 정적 웹사이트 호스팅 서비스입니다. 이를 통해 **HTML, CSS, JavaScript** 등 정적 파일을 기반으로 웹사이트를 간단히 생성하고 공개할 수 있습니다.

**Jekyll** 혹은 **Hugo** 와 같은 정적 사이트 생성기를 사용하면 `Markdown` 파일을 `HTML`로 변환해 더 쉽게 웹사이트를 관리 가능하다는 걸 알게 되었습니다.

블로그는 일방적인 소통하는 곳으로 포스팅된 내용을 올리게 되면 내용이 업데이트되고 보여주기만 하면 되기에 **GitHub Pages**로도 충분히 블로그로 사용할 수 있다는 걸 확인할 수 있습니다.

### **Jekyll** 그리고 **Hugo**
**Jekyll**는 **GitHub Pages**에서 기본적으로 지원하는 정적 사이트 생성기로 `Ruby`로 작성되었습니다.
다양한 테마와 플러그인을 제공하며 **GitHub Pages**와 완벽하게 호환, 별도의 설정 없이 바로 사용 가능합니다.
하지만 Ruby 환경 설정이 번거로울 수 있으며, 대규모 사이트에선 상대적으로 시간이 오래 걸릴 수도 있습니다.

**Hugo**는 `Go` 기반으로 만들어진 빌드 속도가 매우 빠른 정적 사이트 생성기입니다.
매우 빠른 빌드 속도로 대규모 웹사이트에도 적합하며, 설정 파일이 간단하고 디렉토리 구조가 직관적입니다.
테마 커스터마이징에 약간의 학습 곡선이 있습니다.

> `GitHub` 내에서 지원하는 게 `Jekyll`이지만,
> 계속 기록을 하는 거라면 Hugo가 낫다는 판단이 있었으며, 이미 테마가 존재하기 때문에 커스터마이징에 대한 학습이 당장에는 필요없다고 생각했습니다.

## Hugo 설치
MacOS에서 **homebrew**가 설치되어 있다면,  `brew install hugo` 명령어를 통해 **hugo**를 설치할 수 있습니다. Windows 환경이라면 **Chocolatey**를 설치하여 `choco install hugo -y` 명령어를 통해 **hugo**를 설치할 수 있습니다.

> [!info] homebrew
> macOS에서 가장 널리 사용되는 패키지 관리자로, 터미널에서 다양한 소프트웨어를 쉽게 설치하고 관리합니다. 터미널에 아래 명령어를 입력하면 설치됩니다.
> 
> `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
> 
> 설치가 완료되었는지 확인하려면 `brew --version` 를 입력하세요.

> [!info]  Chocolatey
> 가장 널리 사용되는 Windows용 패키지 관리자로 아래 명령어를 입력하면 됩니다.
> 
> `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))`

## PaperMod 테마 사용
[Hugo 테마](https://themes.gohugo.io/) 를 보게 되면 제일 많이 사용되는 것이 **PaperMode**입니다.
디자인 자체가 미니멀하기도 하고 제일 마음에 들었기 때문에 해당 테마를 사용하고자 합니다.

**PaperMode** 테마도 좋기도 하지만, 더욱 미니멀하게 변경했다는 [GitHub 주소](https://github.com/pmichaillat/hugo-website)를 보게 되어서 그대로 적용하겠습니다. 물론 퍼포먼스도 좋다고 하는데, 깊게 생각을 하지 않고 바로 적용을 해보겠습니다.

[GitHub 주소](https://github.com/pmichaillat/hugo-website) 에서 **fork** 혹은 **use this template** 을 해서 새로운 레포지토리를 만듭니다.
그리고 복사된 레포지토리를  `git clone`으로 로컬로 가져옵니다.
레포지토리의 이름을 `{github ID}.github.io`로 만들게 되면 **GitHub Pages**의 주소가 **ohdair.github.io** 와 같이 만들어지게 됩니다. 언급한 이름으로 레포지토리를 만들지 않으면 `ohdair.github.io/new_repository`로 생성됩니다.

## 나만의 블로그로 변환
해당 정적 사이트를 보기 위해서는 터미널에서 파일이 존재하는 위치로 이동합니다.
`hugo server`를 입력하면 코드가 동작하게 되고 브라우저를 통해서 [사이트](http://localhost:1313/](http://localhost:1313/)를 확인할 수 있습니다. 

1. 프로필 사진
2. 제목 및 내용
3. social icon
4. buttons
5. favicon

Hugo에 대해서 파악하기보다는 [Document](https://pascalmichaillat.org/d5/)를 읽어가면서 설정 파일을 변경하여 입맛대로 수정했습니다. **config.yml** 은 설정 파일로 정적사이트를 수정할 수 있습니다.

우선 변경해야 하는 것은 **baseURL**은  **GitHub Pages**의 주소로 입력하고, 메인 화면의 **title** 을 입력하시면 됩니다.

`menu -> main` 항목으로 보게 되면 **weight**의 순서대로 버튼이 놓이게 됩니다.
상세 페이지로 들어갔을 때, 우측 상단에 고정적으로 보여지는 버튼입니다.
상단에 고정으로 보여질 컨텐츠로 작성하면 됩니다.
`params -> MainSections`도 보여지는 요소만 넣었습니다.

`params -> profileMode` 항목에서는 메인 화면에 어떻게 구성할지 수정할 수 있습니다.
**title** 및 **subtitle**은 원하는 문구로 수정하시면 됩니다.

**imageUrl**은 로컬 파일에서 `static/` 폴더 내에 있는 파일로 변경하시려면 `"picture.jpeg"` 이라는 설정과 파일을 변경해서 원하는 프로필 사진으로 변경 가능합니다.

**buttons** 항목에서도 메인 화면에서 보이는 버튼으로 컨텐츠의 내용과 **Tags** 와 **Archive**를 볼 수 있습니다. **Tags** 는 `content/tags/_index.md` 의 내용으로 포스팅된 글에서 포함된 태그를 종합해서 보여줍니다. **Archive** 는 `content/archive.md` 의 내용으로 포스팅된 글들을 시간 순으로 보여줍니다.

**socialIcons** 항목에서는 각 icon으로 표현이 되며, 저장된 pdf를 연결하거나 이메일, 깃허브를 연결할 수 있습니다. 

**lavel** 은 favicon과 함께 사이트를 표현하는 것으로 해당 이미지는 [새로운 favicon](https://favicon.io/)을 쉽게 만들어서 `static/` 내에 있는 파일들(`apple-touch-icon`, `favicon`이 들어간 파일)과 교체하면 됩니다. 

이것으로 설정 파일은 끝이 났습니다.

## 불필요한 파일 삭제
기존에 보여주기 위한 파일들이 많기 때문에 삭제해야 할 파일들이 좀 있습니다.
`archetypes/` 내부에 있는 파일과 사용하지 않는 `static/` 내부의 파일들 그리고 `content/`에서 사용하지 않는 폴더와 파일들입니다.

개인적으로 **tags** 와 **archive**는 이후에서 유용하게 사용될 수 있다고 판단되어 그 외 `content/` 폴더들을 지웠습니다.

그리고 자동으로 정적 페이지 생성하려면 터미널에서 명령어를 치시면 자동으로 페이지에 관련된 파일들이 생성됩니다.
```
hugo
```

이렇게 되면 드디어 길고 길었던 기본 설정이 끝났습니다.

## Obsidian과 연결
옵시디언에서 연결하는 방법으로는 여러가지가 있겠지만, 개인적으로 연결하는 방법으로는 작성하고 있는 폴더 및 파일들과 구분짓는 거였습니다. 새로운 vault를 만들어도 되지만, 2개로 나누어지는 순간 관리가 불편할 거라고 생각했습니다.

기본 설정을 끝나면 왠만해서는 `content/` 내에 있는 파일만 올리고 `hugo` 명령어로 정적 페이지 생성하면 끝이기 때문에 `content` 폴더만 연결합니다.

MacOS에서 작업하기 때문에 Windows 환경이신 분들은 제가 테스팅 하지 못하기 때문에 관련 내용을 생성형 AI로 답을 얻으시면 될 거 같습니다.

심볼릭 링크의 기능으로 바로가기를 만들어줍니다.
**TARGET**은 `ohdair.github.io`라는 레포지토리 내 `content/`로 설정합니다.
**LINK_NAME**은 기존에 사용하는 Obsidian 내 폴더로 생성하면 됩니다.
```
ln -s TARGET LINK_NAME
```

## 자동으로 GitHub 포스팅
Obsidian 내 **Shell commands**라는 플러그인을 설치합니다.
그리고 새로운 Shell command 및 단축키를 입력합니다. 그리고 설정을 눌러줍니다.

![Command Setting 1](commandSetting1.png)

```
#!/bin/bash
cd ~/GitBlog || exit 1

hugo

git add . 
git commit -F -
git push 
```

여기서 **title**은 글 제목으로 `commit` 하기 위해서 입력을 받습니다.
Alias 로는 해당 단축키가 어떤 기능인지 입력하시고 `Pass variables to standard input (stdin)` 에 **{{title}}** 을 입력합니다. 

![Command Setting 2](commandSetting2.png)

포스팅할 글을 만들어서 `Cmd + Shift + P` 를 누르게 되면 자동적으로 GitHub에 올라가게 됩니다.