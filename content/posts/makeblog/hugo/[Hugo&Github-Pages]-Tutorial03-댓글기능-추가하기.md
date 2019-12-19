---
title: "[Hugo&Github Pages] Tutorial03 댓글기능 추가하기"
date: 2019-12-19T10:38:17+09:00
draft: true
author: "joowan kim"
description: "Add comment function"
categories: ["Hugo", "Blog"]
Tags: ["utterances", "comment open source", "Github api"]
type: post
---

### Utterances
> Utterances configuration 페이지를 해석해보면 Github 이슈 검색 API를 활용해 `url`, `pathname`, `title`을 기반으로 페이지(*e.g. 포스트*)과 관련된 이슈를 찾는다고 한다. ~~*by영알못*~~
> 만약, Issue가 달리지 않은 글이라도 누군가 댓글을 달게 되면 [utterances bot](https://github.com/utterances-bot)이 알아서 Issue를 생성해주기 때문에 걱정말란다.
> **무엇보다 블로그에 붙이기가 매우 편하다.**

### Utterances 사용법
> [utterances docs](https://utteranc.es/)로 들어가서 아래와 같은 순서로 진행한다.  
> Configuration 부분을 설명해둔 것이니 영어에 자신있다면 해당 포스트는 안 보고 해도 무방하다.
#### Repository
1. Utterances와 연결할 Github 저장소를 하나 생성한다. _저장소는 반드시 **public**으로 생성한다._  
(필자는 이미 `kjw217/blog-comments`를 생성했기에 생성할 수 없다고 뜨는 것)
![repository 생성](/images/post/hugo/create-comment-repos.png)
1. 새로 만든 저장소에 [Utterances app](https://github.com/apps/utterances)을 설치한다.
    * configure 버튼을 클릭
    ![click](/images/post/hugo/click-configure.png#center100)
    * 새로 만든 저장소가 있는 계정(?그룹?) 선택 *필자는 이미 댓글 기능을 만든 상태이기에 configure 되어있음*
    ![choose](/images/post/hugo/choose-account.png#center100)
    * Select repositories를 클릭하고 새로 만든 저장소를 선택 후 **SAVE** 버튼 클릭
    ![select](/images/post/hugo/select-repositories.png)
1. 여기까지 왔다면, 새로 만든 저장소의 *Settings* 탭에서 *Issues* 항목을 체크한다.
    ![settings](/images/post/hugo/settings-tab.png#center100)
    ![check](/images/post/hugo/check-issue.png)
1. [utterances docs](https://utteranc.es/)의 Configuration에 있는 빈칸에 새로만든 저장소 이름을 `owner/repo`형식으로 입력한다.
    ![input-repo](/images/post/hugo/input-repo.png)
#### Blog Post ↔️ Issue Mapping  
> Blog Post와 Issue를 mapping하기 위한 방법을 선택한다  
1. Issue title이 page의 `pathname`을 포함하는 Issue와 page(post)를 mapping
1. Issue title이 page의 `url`을 포함하는 Issue와 page(post)를 mapping
1. Issue title이 page의 `title`을 포함하는 Issue와 page(post)를 mapping
1. Issue title이 page의 `og:title`을 포함하는 Issue와 page(post)를 mapping
    * *여기서 `og:title`은 meta 데이터를 말하는 듯*
1. Page(post)마다 specific number를 배정
1. Issue title이 특정 단어를 포함하는 Issue와 page(post)를 mapping
#### Issue Label  
> utterances bot이 생성할 이슈에 붙을 Label의 이름을 짓는 것이다.
#### Theme  
> 테마는 원하는 거 고르자
#### Enable Utternaces
> 지금까지 구성했던 사항들로 작성된 코드이다.  
> 그대로 **COPY**해서 댓글을 넣고 싶은 .html파일의 원하는 부분에 붙여넣기 하면 된다.    

![enable](/images/post/hugo/enable.png)
    
---
###### 참고 자료  
- [Hugo로 github.io 블로그 만들기](https://github.com/Integerous/Integerous.github.io)
- [Outsider's Dev Story](https://blog.outsider.ne.kr/1356?category=1)
- [utterances](https://utteranc.es/)
- [astrod님의 utterances 적용](http://astrod.github.io/etc/2018/05/28/utterances-%EC%A0%81%EC%9A%A9/)

*부족한 점이 있다면 댓글로 알려주세요!*
