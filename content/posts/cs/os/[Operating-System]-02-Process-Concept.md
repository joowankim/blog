---
title: "[Operating System] 02 Process Concept"
date: 2019-12-26T12:16:15+09:00
draft: false
author: "joowan kim"
description: "process"
categories: ["Operating System"]
Tags: ["Process"]
type: post
---

### Process
A program in execution  
실행중인 프로그램  

![process](/images/post/os/process.png#center50)

### Process in Memory
다음 그림은 메모리 영역을 나타낸 그림이다.  
각 영역은 text, data, stack, heap이라는 이름으로 정의되었으며, data영역은 대략 아래와 같이 3가지로 나뉜다고 한다.

![memory-area](/images/post/os/memory-area.png#center50)

##### Text 영역
프로그램의 실행 코드가 존재하며, 컴파일된 binary assembly code 또한 이 곳에 저장된다
* 프로그램 실행코드
* 컴파일된 Binary Assembly Code
##### Data 영역
전역변수와 static symbol이 저장되는 영역이다.  
해당 영역을 쓰임새에 따라 다음 3가지 영역으로 나뉜다.

1. 읽기 전용으로 초기화되는 영역: **.rodata**
    * const로 선언 되는 영역
    * 각종 문자열 *(e.g. printf()문의 format string, 상수 문자열..)*
1. 읽기/쓰기가 가능한 영역으로 초기화 되는 영역: **.data**
    * 초기값을 갖는 전역변수
1. 초기화되지 않은 영역: **BSS(Block Started by Symbol)**
    * 초기화되지 않은 전역변수
    * static으로 선언된 symbol

|변수|영역|
|---|---|
|int i;|BSS 영역|
|int i = 1;|.data 영역|
|char str[] = "Hi";|.data 영역, 읽기/쓰기 가능|
|char * pstr = "Hi";|문자열은 .rodata 영역, pstr 변수는 .data 영역|
|const char str[] = "Hi";|문자열은 .rodata 영역, str 변수는 .data 영역|
|static int i;|BSS 영역|

##### Stack 영역
function call을 통해 stack 영역 내에 매개변수, 반환 주소값, 지역변수에 대한 영역을 할당한다.  
function call이 일어날 때마다 앞서 말한 3가지가 스택처럼 할당된다. **PUSH**  
function 호출이 완료되었을 땐, 스택에서 사라진다. **POP**
위와 같이 스택 영역에 차례대로 저장되는 함수의 호출 정보를 스택 프레임(Stack Frame)이라고한다.

###### 스택 프레임(Stack Frame) 동작과정
아래와 같은 코드가 있을 때 스택 프레임의 동작과정을 살펴보자  
아래 과정은 [TCP school 스택 프레임](http://tcpschool.com/c/c_memory_stackframe)과 같은 예시이다.
```c
int main(void)
{
    func1();  // func1() 호출
    return 0;
}

void func1()
{
    func2();  // func2() 호출
}
void func2()
{

}
```
![stack-frame](/images/post/os/stack-frame.png#center100)
1. **STEP 01>** **프로그램이 실행**되면, 가장 먼저 `main()` 함수가 **호출**되어 `main()` *함수의 스택 프레임*이 **스택에 저장(PUSH)**
1. **STEP 02>** `func1()` 함수를 **호출**하면 해당 함수의 *매개변수, 반환 주소값, 지역 변수* 등의 *스택 프레임*이 **스택에 저장**
1. **STEP 03>** `func2()` 함수를 **호출**하면 해당 *함수의 스택 프레임*이 추가로 **스택에 저장**
1. **STEP 04>** `func2()` 함수의 모든 **작업이 완료**되어 **반환**되면, `func2()` *함수의 스택 프레임*만이 **스택에서 제거(POP)**
1. **STEP 05>** `func1()` 함수의 **호출**이 **종료**되면, `func1()` *함수의 스택 프레임*이 **스택에서 제거**
1. **STEP 06>** `main()` 함수의 **모든 작업이 완료**되면, `main()` *함수의 스택 프레임*이 **스택에서 제거**되면서 **프로그램이 종료**   

##### Heap 영역
사용자가 직접 관리할 수 있는 영역 `malloc()`이나 `new` 연산자를 통해 메모리를 동적할당할 수 있다.  
사용자는 메모리의 할당(new)과 해제(free)를 직접 관리해야하며, 객체지향언어(C++/Java)에서는 Garbage Collection이 제공되지만 그래도 직접적인 관여는 필요하다.

### Process Management
각 프로세스는 OS에 등록되고 OS가 관리한다.  
이를 위해 OS는 각 프로세스의 정보를 담은 Data Structure가 필요하다.  
이를 PCB(Process Control Block)이라고 한다.
 
 #### PCB(Process Control Block)
 Process state, Process number(pid), Program Counter(PC), CPU registers 등을 포함한다.
 
![PCB](/images/post/os/pcb.png#center100)
 
---
###### 참고 자료
- 학교 강의자료
- Operating System Concepts 9th edition
- [ffun님 Tistory의 메모리 구조 정리글](https://ffun.tistory.com/entry/%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0)
- [TCP school 메모리 구조](http://tcpschool.com/c/c_memory_structure)
- [TCP school 스택 프레임](http://tcpschool.com/c/c_memory_stackframe)

*부족한 점이 있다면 댓글로 알려주세요!*
