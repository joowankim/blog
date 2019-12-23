---
title: "[Hugo&Github Pages] Theme Customizing 01 카테고리 만들기"
date: 2019-12-22T21:38:45+09:00
draft: true
author: "joowan kim"
description: "Create category tab"
categories: ["Hugo", "Github Pages", "Blog"]
Tags: ["Category Tab", "Customizing"]
type: post
---

내가 가진 테마인 northendlab-hugo 테마에서 nested sections를 이용해 트리 구조의 카테고리 탭을 만들었던 과정을 기록하겠다.

### 기존 northendlab 테마 헤더의 탭
![header-tabs](/images/post/hugo/header-tabs.png#center100)
* 단순한 탭으로 된 형태의 메뉴
* **목표: 이걸 지금처럼 드롭다운 형태의 카테고리 형식의 메뉴로 만들기**

#### 목표를 위해 필요한 것
1. 테마의 partials 디렉토리에서 header.html의 메뉴부분 구조 확인
1. config.toml에서 identifier와 parent 설정
1. 메뉴를 만들기 위해 필요한 디렉토리를 config.toml에 설정한 url에 맞게 생성
    * 이 때, 디렉토리 명은 항상 **소문자**로 해야한다.
    * ~~필자는 대문자로 했다가 밤새고, 다음날 자기혐오에서 헤어나올 수 없었다.~~

### header.html의 메뉴 구조 확인하기
```html {hl_lines=[4, 9, 10, 18, 26, 27]}
<!-- northendlab-hugo/layouts/partials/header.html 메뉴 부분 -->

<ul class="navbar-nav ml-auto">
    <li class="nav-item">   <!-- home tab -->
        <a class="nav-link" href="{{ .Site.BaseURL }}">
            {{ with .Site.Params.Home }} {{ . }} {{ end }}
        </a>
    </li>
    {{ range .Site.Menus.main }}    <!-- menu -->
        {{ if .HasChildren }}   <!-- 자식 노드를 가진다면 -->
            <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle" href="#" role="button" 
                 data-toggle="dropdown" aria-haspopup="true" 
                 aria-expanded="false">
                    {{ .Name }}
                </a>
                <div class="dropdown-menu">
                {{ range .Children }}   <!-- 자식 노드 출력 -->
                    <a class="dropdown-item" 
                     href="{{ .URL | absURL }}">
                        {{ .Name }}
                    </a>
                {{ end }}
                </div>
            </li>
        {{ else }}  <!-- 자식 노드를 가지지 않는다면 -->
        <li class="nav-item">
            <a class="nav-link" href="{{ .URL | absURL }}">{{ .Name }}</a>
        </li>
        {{ end }}
    {{ end }}
</ul>
```
1. **line 4**: home tab을 출력
1. **line 9 ~**: main이라는 Menu에 들어 있는 목록을 출력
    * 만약 자식 노드가 있다면 자식까지 출력
    * 없다면 단일 출력
1. 이 코드에서 궁금했던 것 (모두 **config.toml** 파일에서 설정함)
    * main이라는 이름의 메뉴를 어떻게 Menu라는 변수에 추가하는 지
    * 추가된 메뉴에는 parent와 children의 관계를 어떻게 추가하는 지
    * Name이라는 변수는 어떻게 정해지는 지
    
### config.toml 설정하기
> 앞선 단계에서 궁금했던 것들을 config.html 파일을 통해 해결할 수 있었다.
> 1. main이라는 이름의 메뉴를 어떻게 Menu라는 변수에 추가하는 지
>    * `[[menu.<메뉴이름>]]` 추가
> 1. 추가된 메뉴에는 parent와 children의 관계를 어떻게 추가하는 지
>    * parent의 `identifier`와 children의 `parent` 설정
> 1. Name이라는 변수는 어떻게 정해지는 지
>    * 메뉴를 만들면서 `name` 설정

```config.toml
#config.toml

[[menu.main]]           # [[menu.<메뉴이름>]]
URL = "posts"           # URL: <content 디렉토리 아래의 디렉토리 위치>
name = "Posts"          # name: <디렉토리의 원하는 이름>
identifier = "Posts"    # identifier: <children이 parent를 지정할 때 필요
weight = 1              # weight: 메뉴 순서

[[menu.main]]
URL = "posts/languages/"
name = "Languages"
identifier = "Languages"
parent = "Posts"        # parent: parent의 identifier 
```

---
###### 참고 자료
- [northendlab-hugo demo](https://themes.gohugo.io/theme/northendlab-hugo/)
- [northendlab github](https://github.com/themefisher/northendlab-hugo)
- [Hugo docs - menu](https://gohugo.io/content-management/menus/)

*부족한 점이 있다면 댓글로 알려주세요!*
