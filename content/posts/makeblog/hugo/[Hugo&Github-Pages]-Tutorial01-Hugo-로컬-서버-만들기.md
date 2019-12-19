---
title: "[Hugo&Github Pages] Tutorial01 Hugo 로컬 서버 만들기"
date: 2019-12-18T15:46:20+09:00
draft: false
author: "joowan kim"
description: "Blog creation"
categories: ["Hugo", "Github Pages", "Blog"]
Tags: ["create blog", "installation"]
type: post
---

### Hugo 설치하기
> [Hugo installation 페이지](https://gohugo.io/getting-started/installing/)로 가면 설치방법을 ~~영어로~~ 설명하고 있다.  
> 다만, 필자는 Windows를 사용하기에 이 [영상](https://www.youtube.com/watch?v=G7umPCU-8xc&feature=emb_logo)을 보고 설치했다.  
> 영상 내용을 요약하면 아래와 같다:

1. 원하는 위치에 Hugo 및 bin 디렉토리(폴더) `C:\Hugo\bin`생성
1. [Hugo releases](https://github.com/gohugoio/hugo/releases)에서 OS에 맞는 압축파일 다운로드
1. 다운받은 압축파일을 방금 생성한 폴더 `C:\Hugo\bin`에 압축 해제
1. 환경변수를 설정 __*두 가지 방법 중 택 1*__
    * 커맨드 라인에서 `C:\Hugo\bin`으로 이동해 `$ set PATH=%PATH%;C:\Hugo\bin` 명령어 설정
    * **또는,** 내 컴퓨터(우클릭)>속성>고급 시스템 설정>고급 탭>환경 변수 버튼>사용자 변수의 Path 클릭>편집 버튼에 hugo.exe 파일이 있는 경로 `C:\Hugo\bin` 추가
1. 명령 프롬프트(cmd)나 git bash에서 `$ hugo version` 명령어로 hugo가 설치되었는지 확인
1. 혹시라도 version이 나오지 않는다면 GO 설치여부를 확인하거나 재부팅

### Hugo 블로그 디렉토리 구조 생성하기
> 이 단계에서는 커맨드 라인 명령어를 사용해야 한다.  
> mac OS나 Linux를 사용한다면 원래 하던대로 커널을 이용하면 된다.  
> 필자는 Windows를 사용하기에 git bash를 사용했다.
1. 다음 명령어를 통해 새로운 사이트 생성
    ```bash
    $ cd <Hugo-directory-path>   # C:\Hugo로 이동
    $ hugo new site <blog-name>  # 새로운 사이트 생성 (필자는 'blog')
    ```
1. 아래와 같은 디렉토리 구조가 생성되었다면 성공
    ```
    Hugo
      |-blog #<blog-name>을 말한다
         |-archetypes
         |  |-default.md
         |-content
         |-data
         |-layouts
         |-static
         |-themes
         |-config.toml
    ```

### 블로그 테마 설정하기
1. https://themes.gohugo.io/ 원하는 테마 선택
1. `C:\Hugo\blog` 디렉토리로 이동한 후에 아래 명령으로 테마 다운로드
    ```bash
    $ git init
    $ git submodule add <theme-github-url> themes/<theme-name>
    ```
    `<theme-github-url>`과 `<theme-name>`은 테마의 Github 주소와 테마의 이름
    * 필자는 다음과 같이 입력 (northendlab 테마를 사용했음)
    > * `<theme-github-url>` : https://github.com/themefisher/northendlab-hugo.git  
    > * `<theme-name>`       : northendlab-hugo
1. 테마 홈페이지에서 안내하는 대로 `config.toml`파일 등을 수정
    * 이 부분은 테마마다 설정해야 할 것이 다르기 때문에 필히 테마 홈페이지 참조
1. 위 과정을 마쳤다면 themes 디렉토리 아래에 테마 폴더 생성됨  
   **아래 트리는 themes 디렉토리 밑에 폴더가 생성된 것을 표현한 것, 실제와 다를 수 있음**
    ```
    Hugo
      |-blog
        |-archetypes
        |  |-default.md
        |-content
        |-data
        |-layouts
        |-static
        |-themes
        |  |-northendlab-hugo
        |     |-..
        |     :  
        |-config.toml
    ```
### Content 생성하기
> `C:\Hugo\blog` 디렉토리로 이동한 후에 아래 명령 입력  
> `$ hugo new <category-path>/<post-name>.<post-format>`
```bash
$ hugo new posts/my-first-post.md
```
1. 위 명령어를 통해 `content` 디렉토리 밑에 `posts` 디렉토리와 `my-first-post.md`파일이 생성된다
    ```
    Hugo
      |-blog
        |-archetypes
        |  |-default.md
        |-content
        |  |-posts
        |     |-my-first-post.md
        |-data
        :
        :
    ```
1. `my-first-post.md`
    ```
    title: "My First Post"
    date: 2019-03-26T08:47:11+01:00
    draft: true
    ```
### Hugo server 구동하기
```bash
$ hugo server -D
```
1. 위 명령어를 통해 서버 구동
1. `-D` 옵션은 post의 property 중 `draft: true`인 문서도 홈페이지에 띄우겠다는 것
1. http://localhost:1313/ 을 통해 자신의 블로그에 접근할 수 있다

---
###### 참고 자료
- [Hugo Docs](https://gohugo.io/getting-started/quick-start/)  
- [Hugo로 github.io 블로그 만들기](https://github.com/Integerous/Integerous.github.io)

*부족한 점이 있다면 댓글로 알려주세요!*