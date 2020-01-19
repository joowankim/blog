---
title: "[Operating System] 03 Process Scheduling"
date: 2019-12-28T17:00:54+09:00
draft: false
author: "joowan kim"
description: "Process Scheduling"
categories: ["Operating System"]
Tags: ["Process", "Scheduling"]
type: post
---

### Process State
프로세스는 아래와 같은 5가지의 상태(State)를 가진다.

|상태|설명|
|:---:|---|  
|**new**| 프로세스가 만들어지기 전인 상태 *(아직 프로세스가 아님)*|
|**ready**| 프로세스가 메모리에서 CPU에 할당되기를 기다리는(ready) 상태|
|**running**| CPU가 프로세스의 명령을 수행하고 있는 상태|
|**waiting**| 프로세스가 특정 event _(e.g. I/O operation,..)_ 가 일어나기를 기다리고 있는 상태|
|**terminated**| 프로세스의 작업이 끝난 상태 (더 이상 프로세스가 아님)|

###### 주의
* CPU core 하나 당 오직 하나의 프로세스만 **running** 상태
* 다른 프로세스는 **ready** 또는 **waiting** 상태

![process-state](/images/post/os/process-state.png#center100)

### Process Scheduling
CPU scheduler가 ready queue에서 프로세스 하나를 선택(CPU Scheduling)해 processor에 올려준다(dispatch).  
그리고 running 상태인 프로세스가 특정 event를 기다리기 위해 waiting queue에 들어간다.  
이러한 과정을 Process Scheduling이라고 한다.

* Ready Queue: ready 상태인 프로세스들을 말한다.
* Waiting Queue: 특정 event를 기다리는 중인 waiting 상태의 프로세스 리스트를 말한다.

각 Queue는 다음과 같은 특징을 가진다.  
* PCB로 이루어진 linked list
* head와 tail을 가리키는 Queue header

![schedule-queue](/images/post/os/schedule-queue.png#center100)

### Process Context
프로세스의 Context는 CPU execution context, Process memory space, Process management in OS에 의해 결정된다.
1. CPU execution context:
    * Program Counter(PC)
    * Registers
1. Process memory space
    * code, data, stack
1. Process management in OS
    * Process Control Block(PCB)
    * Kernel stack

![context](/images/post/os/process-context-in-pcb.png#center50)

### Context Switch
OS가 현재 실행중인 프로세스를 다른 프로세스로 바꾸는 것을 말한다.
![context-switch](/images/post/os/context-switch.png#center100)




---
###### 참고 자료
- 학교 강의자료
- Operating System Concepts 9th edition

*부족한 점이 있다면 댓글로 알려주세요!*
