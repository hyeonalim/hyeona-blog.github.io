---
layout: post
title: "[Concept] 파일 IO(Input/Output) 개념과 사용법"
subtitle: "FileStream/Buffer/Channel 개념"
date: 2021-12-23 11:30:00 +0900
background: '/img/posts/06.jpg'
---

[1. Stream / Buffer](#Stream-/-Buffer)  
[2. Channel](#Channel)  

# Stream / Buffer
FileInputStream / FileOutputStream
- 바이트 단위로 작성한다.
- 저수준의 클래스로 한줄씩 데이터를 읽어오는 것
- 초기화나 리턴값으로 -1 지정하는 것이 룰

BufferdInputStream / BufferdOutputStream
- 실제 스트림의 입출력의 편리를 위해 사용하는 보조 스트림
- 버퍼링을 사용하여 입출력의 성능을 향상시키는 스트림

### Buffer 과 Stream 의 차이
Buffer
- 모두 읽고 한 글자씩 출력
- null일 때까지 한번에 읽어와서 한 글자씩 내보낸다.

※ 버퍼링: 자료 처리 속도가 다른 두 장치 간에 일정 크기의 임시 저장 장치를 이용하여 정보 처리를 보다 빠르게 하는 방법

Stream(byte 단위)
- 입출력에 필요한 정보 흐름의 통로 역할
- 한 글자씩 읽어와서 return 값으로 -1 받기

### 형변환(casting)

    (변환할 타입) 변환할 변수명

- 기본형에서 boolean을 제외한 나머지 타입들은 서로 형변환이 가능하다.
- 기본형과 참조형간의 형변환은 불가능하다.

### 데이터 변환이 필요한 이유는 뭘까?
파일을 읽어올 때 int로 읽어온다. int로는 숫자를 출력해주기 때문에 아스키코드로 표현해주려면 형변환이 필요하다.  
한줄로 읽어오는 변수를 readOne이라고 하면 형변환을 해주려면 => (char)readOne 으로 작성해주어야 한다.

FileReader / FileWriter
- 문자 기반으로 파일에 입출력

InputStreamReader / InputStreamWriter
- 바이트 기반의 스트림을 문자 기반의 스트림으로 연결시켜준다.

BufferedReader / BufferedWriter
- 문자 기반으로 파일에 입출력

readAllByte
- 전부 다 메모리에 올려둔다.
- 읽어오는 양이 많은 메모리를 필요로 하면 꺼져버린다.

### 작성한 것을 덮어씌우기 하려면?
Overwrite 하는 과정이 필요하다.

``` java
// FileWriter 사용 시
FileWriter fw = new FileWriter(file, true);

// BufferedWriter 사용 시
BufferedWriter bw = new BufferedWriter(new FileWriter(file));

```

## 주로 일어나는 예외
1. 존재하지 않는 파일 (FileNotFoundException)
2. 하드디스크 정전이나 망가질 때(IOException)

## 그외 도움이 되는 지식들
- 변수 초기화는 필수로 해주자
- printStackTrace(): 에러 메세지의 발생 근원지를 찾아서 단계별로 에러를 출력해준다.
- IO open 시, 무조건 close 해주어야 한다. 이후 메모리 용량 초과가 일어날 수도 있다.

# Channel
Channel
- 주로 네트워크에서 사용된다.
- Buffer가 필요하다.
- 모드: r / w / rw
- 양방향으로 Read/Write 둘 다 사용할 수 있다.