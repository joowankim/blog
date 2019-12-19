---
title: "[Hugo&Github Pages] Tutorial02 Github 저장소 생성 및 업로드"
date: 2019-12-19T10:24:34+09:00
draft: true
author: "joowan kim"
description: "Github settings"
categories: ["Blog", "Hugo", "Github Pages"]
Tags: ["github.io"]
type: post
---

### Github repository 생성하기
> Github의 repository는 총 2개가 필요하다.
> 1. `C:\Hugo\blog`의 전체 내용을 담을 repository
> 1. **이후에 생성될** `C:\Hugo\public`의 생성된 정적 웹페이지를 담을 repository
* 첫 번째 저장소는 원하는 이름`blog`으로 생성
* 두 번째 저장소는 `<github계정>.github.io`라는 이름으로 생성
1. 첫 번째 저장소를 `C:\Hugo\blog`의 remote로 설정
    ```bash
    $ cd blog
    $ git init 
    $ git remote add origin <first-github-repository-url>
    ```
1. 두 번째 저장소를 `C:\Hugo\blog`의 submodule로 설정
    ```bash
    $ cd blog
    $ git submodule add -b master <second-github-repository-url> public
    ```
    * 위 명령을 통해 `C:\Hugo\blog\public` 디렉토리 생성됨

### Contents 업로드하기
1. `C:\Hugo\blog`로 이동
1. `$ hugo -t <theme-name>` 명령을 통해 테마가 적용된 블로그를 public에 생성
1. `C:\Hugo\blog\public`로 이동
1. `<username>.github.io` repository에 수정된 블로그 push
    * `git add .` 수정된 파일들을 index에 올림
    * `git commit -m "<commit-message>"` 변경 내용을 commit
    * `git push origin master` commit된 내용을 remote에 push
1. `blog` 저장소에도 변경내용 push
    * `C:\Hugo\blog`로 이동
    * `git add .`
    * `git commit -m "<commit-message>"`
    * `git push origin master`

### 업로드 자동화 파일 deploy.sh 
1. 아래 스크립트 복사해서 `deploy.sh`파일을 `C:\Hugo\blog`에 둔다.  
1. **반드시 테마명은 자신이 선택한 테마로 변경한다.**  
1. 스크립트 실행 방법은 `C:\Hugo\blog`에서 `$ bash deploy.sh`입력

```bash
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project. 여기 테마명 바꾸세요
hugo -t northendlab-hugo

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site $(date)"
if [ -n "$*" ];then
	msg="$*"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master



# Come Back up to the Project Root
cd ..

# blog repos Commit & Push
git add .

msg="rebuilding site $(date)"
if [ -n "S*"];then
	msg="$1"
fi
git commit -m "$msg"

git push origin master
```

---
###### 참고 자료
- [Hugo Docs](https://gohugo.io/getting-started/quick-start/)  
- [Hugo로 github.io 블로그 만들기](https://github.com/Integerous/Integerous.github.io)

*부족한 점이 있다면 댓글로 알려주세요!*

