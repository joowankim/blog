---
title: "[Operating System] 04 Operations on Processes"
date: 2019-12-30T05:18:36+09:00
draft: true
author: "joowan kim"
description: "Operations on Processes"
categories: ["Operation System"]
Tags: ["Process"]
type: post
---

Processes는 동시에 실행할 수 있다. 다르게 말하면 동적으로 **생성**되거나 **삭제**될 수 있다.
* 그렇기에 OS는 프로세스를 생성하거나 끝내는 등의 mechanism이 있어야한다.
* 일반적으로, 프로세스는 pid(process identifier)라는 정수값으로 구분된다.  

그리고 프로세스는 서로 **부모**와 **자식**관계, 즉, 다음 그림과 같은 **tree**를 형성한다.  

![process-tree](/images/post/os/process-tree.png#center100)

```bash
# 리눅스에서 다음과 같은 명령어를 통해
# 아래와 같은 결과를 확인할 수 있다.

ps -el

:<<'END'
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S     0     1     0  0  80   0 -  2081 -      ?        00:00:00 init
0 S     0     3     1  0  80   0 -  2082 -      tty1     00:00:00 init
0 S  1000     4     3  0  80   0 -  4836 -      tty1     00:00:00 zsh
0 R  1000    60     4  0  80   0 -  4271 -      tty1     00:00:00 ps
END
```

### UNIX examples
UNIX에서는 여러 system call로 process를 관리한다.   
`fork()`, `exec()`, `wait()`를 통해 process를 생성하고,  
`exit()`, `abort()`를 통해 process를 종료한다.

#### Process Creation

`fork()`
* 새로운 프로세스를 생성한다.
* 새로운 프로세스는 부모 프로세스의 메모리 공간을 복사본으로 구성한다.  

`exec()`
* `fork()` 명령 이후에 사용된다.
* 새로 생성된 프로세스에 새로운 프로그램을 올린다.
* 새로운 바이너리 파일을 로딩한다.

`wait()`
* parent process는 `fork()`후에 `wait()`를 통해 child가 끝나기를 기다린다.

![process-creation](/images/post/os/process-creation.png#center100)

#### Process Termination

`exit()`
* process가 OS에 `exit()` system call을 통해 작업이 끝나서 해당 프로세스를 삭제하도록 요청한다.
* parent process에 `wait()`를 통해 status value를 반환한다.

`abort()`
* parent process가 children processes를 끝낼(terminate) 때 호출한다.
* children이 끝나거나 제한된 resource 이상을 할당 받거나 할 때 호출됨.
* parent process가 끝나면 children process도 모두 종료: **cascading termination**

### Interprocess Communication
프로세스끼리 협업할 때 요구된다.
* Information sharing *(e.g. shared file, ..)*
* Computation speedup *(e.g. parallel computing in multi-core environment, ..)

원칙적으로 프로세스끼리는 보안상의 이유를 서로 통신이 불가능하다.  
그렇기 때문에 OS는 system call을 통해 InterProcess Communication(IPC)을 제공한다.
 
#### Communication Models
두 가지의 Communication model이 존재한다.
* Message passing
* Shared memory
  
이는 프로세스 간의 소통(communicate)과 process actions의 동기화(synchronize)를 위한 mechanism이다.  

![mp-sm](/images/post/os/mp-sm.png#center100)

##### Message Passing
message를 통해 process끼리 소통한다.  
IPC는 `send(message)`와 `receive(message)`를 제공한다.  

Process끼리 communicate를 위해서는:
1. 프로세스 사이에 **communication link**를 세우고
1.  `send()`와 `receive()`를 통해 message를 교환한다.
    * 이때 **system call**이 필요하다

대표적인 예로는 *Microkernel structure, Sockets(networking), RPC(distributed systems)* 가 있다.


##### Shared Memory
둘 이상의 프로세스가 system call을 통해 같은 메모리 공간을 공유한다.
* 프로세스끼리 공유된 공간을 read & write하며 정보를 교환한다.

###### Problems
1. producer process와 consumer process가 동시에 shared memory에 접근하려 할 때
    * **Process Synchronization**을 통해 해결
1. multi-core processors에서 **cache coherence problem**이 발생할 수 있다.


---
###### 참고 자료

*부족한 점이 있다면 댓글로 알려주세요!*
