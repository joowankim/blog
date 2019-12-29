---
title: "[Operating System] 00 Intro"
date: 2019-12-26T12:15:22+09:00
draft: true
author: "joowan kim"
description: "Opertaing System Introduction"
categories: ["Operating System", "Intro"] 
Tags: ["Introduction", "Overview"]
type: post
---

### Operating System
A collection of computer programs
* **mananges** computer hardware resources
* **provides** a **basis** for application programs
* acts as an **interface** between the computer user and the computer hardware

### What OSes do
* User View:
    1. Command Line Interface(CLI)
    1. Graphical User Interface(GUI)
    1. Touch Screen Interface
* System View: Kernel
    1. A collection of programs that is an interface
    1. OS makes hardware useful to the programmer
    1. OS controls user programs
    1. 간단한 가정을 가진다
        * 한번에 하나의 프로그램만 실행된다
        * 나쁜 유저는 없다
    1. **하드웨어나 유저의 사용성에서 문제가 생길 수 있다**
    1. OS provides mechanisms to address the problems
        * **preemption**: looping process로 부터 CPU resource를 다시 가져옴
        * **Memory Protection**: 다른 process의 메모리 영역을 침범하지 못하게 함
### Computer System
하드웨어, OS, application programs, 유저로 나뉜다  

![an-interface](/images/post/os/as-an-interface.png#center50)

 






---
###### 참고 자료
- 학교 강의자료
- Operating System Concepts 9th edition

*부족한 점이 있다면 댓글로 알려주세요!*
