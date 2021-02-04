# 해피해킹 메모장

![Opengraph Image](assets/og-image.png)

---

## Table of Contents
- [로컬 서버 설정 및 실행](#로컬-서버-설정-및-실행)
  - [Hugo 설치](#Hugo-설치)
    - [macOS](#macos)
    - [Linux](#linux-snap)
    - [Windows](#windows)
    - [설치 확인](#설치-확인)
  - [로컬 서버 실행](#로컬-서버-실행)
- [게시글 작성법](#게시글-작성법)
  - [게시글 기본 구조 만들기](#게시글-기본-구조-만들기)
  - [게시글 폴더 구조](#게시글-폴더-구조)
  - [index.md 기본 구조](#indexmd-기본-구조)
  - [이미지 용량 최적화](#이미지-용량-최적화)
- [출판하기](#출판하기)
  - [Pull Request](#pull-request)

---


## 로컬 서버 설정 및 실행

### Hugo 설치

#### macOS

[Homebrew](https://brew.sh/)를 통해 Hugo를 설치합니다.

```bash
$ brew install hugo
```

#### Windows

[Scoop](https://scoop.sh/)을 통해 Hugo를 설치합니다.

```bash
$ scoop install hugo-extended
```

#### Linux (Snap)

Snap을 통해 Hugo를 설치합니다.

```bash
$ snap install hugo --channel=extended
```

#### 설치 확인

아래의 버전 확인 명령어로 Hugo가 잘 설치 되었는지 확인합니다.

```bash
$ hugo version
```

### 로컬 서버 실행

'해피해킹 메모장' GitHub repo를 clone 받고, 해당 폴더로 이동합니다.

```bash
$ git clone https://github.com/hphkinc/notes.git
$ cd notes
```

테마 적용을 위해 repo 내부의 submodule을 업데이트 합니다.

```bash
$ git submodule update --init --recursive
```

아래의 명령어로 서버를 실행합니다. 여기서 `-D`는 draft를 포함하여 렌더링 하는 옵션입니다.

```bash
$ hugo serve -D
```


## 게시글 작성법

### 게시글 기본 구조 만들기

아래의 명령어로 작성할 게시글의 기본 구조를 생성합니다.

```bash
$ hugo new posts/{:slug}/index.md
```

여기서 `slug`는 게시글의 고유하게 할당되는 문자열로, 다음과 같은 규칙으로 작성합니다.

- 영문 소문자 또는 숫자만으로 구성
- 단어간 띄어쓰기는 공백 대신 `-`(dash) 문자 사용
- 해당 게시글이 어떤 내용을 담고 있는지 간략하게 표현

### 게시글 폴더 구조

위의 명령어를 입력하면, `images` 폴더를 제외한 폴더 및 파일이 아래와 같이 생성됩니다. `imags` 폴더는 직접 생성하여 게시글에서 사용되는 이미지 파일들을 하나로 모아 정리합니다.

```bash
content/
└── posts/
    └── example-post/
        ├── images/
        │   └── example-image.png
        └── index.md
```

### index.md 기본 구조

```markdown
---
slug: "example-post"
title: "Example Post"
description: ""
date: "2021-01-25T20:41:41+09:00"
lastmod: "2021-01-25T20:41:41+09:00"
categories: []
tags: []
image: ""
authors: []
draft: true
---
```

- `slug`: 게시글의 고유한 값입니다. 게시글의 기본 구조를 만들 때, 입력한 값이 기본으로 작성되어 있습니다. 이 값은 index.md 파일이 들어있는 폴더의 이름과 같으며, URL로도 사용되는 값입니다. 폴더 이름과 같을 필요 없으며 원하는 값이 있다면 변경하여 사용할 수 있습니다. 해당 속성으로 지정된 값을 우선적으로 사용합니다.
- `title`: 게시글의 제목입니다. slug로 입력한 내용을 title case로 변경한 값이 기본으로 작성되어 있습니다.
- `description`: 해당 게시글의 한 줄 또는 요약 설명입니다. 기본적으로 빈 값이 작성되어 있으며, 해당 내용은 사이트 상에서도 요약 정보로 보여지는 내용이며, meta description 및 og:description에서도 사용되는 값입니다.
- `date`: 게시글의 작성 시간입니다. 명령어를 입력하여 기본 구조를 만드는 시점의 시간이 기본으로 작성되어 있으며, 자유롭게 변경 가능합니다. 현재 시간을 넘어선 미래 시간을 입력하면, 해당 게시글은 사이트 내에서 보여지지 않습니다. 테마에 따라 시간까지 보여지기는 하나, '해피해킹 메모장'에서 사용 중인 테마에서는 날짜까지만 보여집니다.
- `lastmod`: 게시글의 최종 수정 시간입니다. date 속성의 값과 같은 값이 기본으로 작성되어 있으며, 자유롭게 변경 가능합니다. 해당 값은 date 속성과는 다르게 시간을 포함하여 표시됩니다.
- `categories`: 카테고리입니다. 배열의 형태로 문자열을 입력합니다. 사이트 상에서 카테고리별로 모아보는 기능이 있습니다. 여러개의 값을 작성할 수 있으며, 첫글자가 대문자인 영문(e.g. Python)으로 작성합니다. 큰 단위로 그룹을 만드는 느낌으로 사용합니다.
- `tags`: 태그입니다. 배열의 형태로 문자열을 입력합니다. 사이트 상에서 태그별로 모아보는 기능이 있지만, 카테고리와는 조금 다르게 보조적인 느낌으로 사용합니다. 여러개의 값을 작성할 수 있으며, 모두 소문자인 영문(e.g. html)으로 작성합니다. 해당 게시글의 키워드를 나열하는 느낌으로 사용합니다.
- `image`: 대표 이미지 입니다. 이미지의 상대 경로를 입력합니다. 사이트 상에서 목록 및 상세 게시글 페이지에서 메인으로 보여지는 이미지이며, og:image로 사용되는 이미지 입니다.
- `authors`: 작성자 입니다. 복수의 작성자를 작성할 수 있으며, 배열의 형태로 작성자 이름을 입력합니다. 'content > authors' 폴더에 'zzulu'와 같이 작성자에 대한 정보가 등록되어 있으면, 해당 정보(이미지 및 이름)를 가져와 사용합니다. 이 때, author의 title 속성에 지정된 값으로 작성자를 지정하여야 합니다.
- `draft`: 게시글의 draft 유무입니다. 기본 값으로 true가 작성되어 있으며, 이 때는 게시글이 production에 게시되지 않습니다. 게시글 작성이 완료되면 false로 변경하여 공개하도록 합니다.
- 그 아래로는 마크다운 문법을 활용하여 게시글을 작성합니다.

### 이미지 용량 최적화

게시글에 사용할 이미지들은 원활한 페이지 로딩을 위하여 [tinypng.com](https://tinypng.com) 또는 [squoosh.app](https://squoosh.app)으로 용량과 해상도를 조절하여 사용합니다. 이미지의 가로 길이가 **1200px** 이상 일 때 모든 해상도에서 잘 보여지며, 가로 길이가 1200px 이하이더라도 보여지는 것에는 문제가 없지만 선명하게 보이지 않을 수 있습니다.


## 출판하기

### Pull Request

게시글 작성이 완료되면 `draft: false`로 변경 후, 새로운 브랜치에 `images` 폴더와 `index.md` 파일을 commit 하고 push 합니다. 그리고 GitHub 사이트에서 Pull Request를 보냅니다.

간단한 리뷰를 받은 후 게시글이 main 브랜치에 머지되면, GitHub Pages에 배포된 사이트에 반영됩니다.
