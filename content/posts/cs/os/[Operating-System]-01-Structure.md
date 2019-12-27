---
title: "[Operating System] 01 Structure"
date: 2019-12-26T12:15:44+09:00
draft: true
author: "joowan kim"
description: "Operation System Structure"
categories: ["Operating System"]
Tags: ["Structure"]
type: post
---


### Challenging Issues
> 1. At any given time, each resource can serve only one process
>   * OS -> **Process Management**
> 1. Multiple processes can be executed while sharing memory
>   * OS -> **Memory Management**
> 1. Using I/O device takes a long time, and CPU is idle and underutilized
>   * OS -> **I/O Management**
> 1. An unauthorized process causes a system fault although other processes have no problem
>   * OS -> **Protection**

1. Process Management
    * process: 실행중인 프로그램
    * process(thread) scheduling
1. Memory Manageement
    * CPU reads both **instructions** and **data** from main memory
    * **multitasking**
    * **(Virtual) Memory Manangement**
1. I/O Subsystem
    * There is always **a device driver and device controller** for each I/O device
    * I/O request from application
    * device controller takes action
    * device controller informs the CPU via an **interrupt** that it has finished

### Basic Operations
> OS의 기본적인 동작에는 multitasking, interrupt, protection이 있다

#### Multitasking
> 메인메모리에 동시에 올라와 있는 process들은 CPU time이나 I/O devices와 같은 resource를 공유한다.
> 이를 관리하고 조정하는 게 멀티태스킹.

* 장점
    1. CPU Utilization
        * Keep several jobs in memory simultaneously
        * One job selected and run via **scheduling**
    1. Time Sharing
        * CPU switches jobs so frequently: **illusion of multitasking**
        * which process do we run first?: **CPU Job Scheduling**

#### Interrupt
> Interrupt: device의 작업이 끝났음을 CPU에게 알리는 수단
![interrupt](/images/post/os/interrupt.png#center50)

1. Hardware Interrupt: Hardware I/O device interrupt CPU
1. Software Interrupt: Software programs interrupt CPU
    * **System calls**: application program이 kernel functions을 call하기 위해 사용
    * **Exceptions**: divide by zero exception
1. Interrupt Handler
    1. CPU가 interrupt되면,
    1. 하던거 멈춤
    1. **interrupt vector**(interrupt한 device의 드라이버 위치)로 **interrupt service routine**을 실행
    1. service routine을 끝내면 다시 하던거 함
    ![hardware-interrupt-timeline](/images/post/os/hardware-interrupt-timeline.png#center100)

#### Protection
> OS와 user는 컴퓨터 시스템의 HW/SW를 공유한다. 
> Malicious program이 다른 프로그램에 해를 끼치지 못하도록 하기위해 OS code와 user code를 구별해야했다.

##### Dual-mode operation
> Kernel mode와 User mode를 구분  
> 하드웨어(e.g. CPU)에서 Mode bit를 가짐(Kernel:0, user:1)

![dual-mode](/images/post/os/dual-mode.png#center100)

---
###### 참고 자료
- 학교 강의자료
- Operating System Concepts 9th edition

*부족한 점이 있다면 댓글로 알려주세요!*
