---
title: "LabEx 리눅스 퀵 스타트 코스"
date: 2026-05-10 00:00:00 +0900
categories: [강의]
tags: [Linux, Hactor]
---


# 리눅스 퀵 스타트

## 1 첫 번째 리눅스 실습

### 1) Hello LabEx

`echo`: 사용자가 입력한 내용을 그대로 화면에 다시 보여 줌

-리눅스는 대소문자 구분함: echo, Echo, ECHO 모두 서로 다른 명령어로 인식

-공백 (띄어쓰기) 중요. echo와 따옴표(”) 사이 **반드시 공백 존재해야 함**

-따옴표는 echo가 반복해서 출력할 텍스트의 범위 지정

### 2) 현재 사용자 표시하기

`whoami`: 현재 시스템에서 작업을 수행하고 있는 **사용자의 이름**을 확인함

-여러 계정으로 작업 or 권한 확인 시 유용 → 누구로 로그인되어 있는지 즉시 파악 가능

### 3) 사용자 및 그룹 정보 표시하기

`id`: 어떤 그룹에 속해 있는지 알 수 있음

- uid: 사용자 ID (고유한 숫자 식별자)
- uid=0: 리눅스 시스템에서의 0번 아이디는 모든 권한을 가진 ‘슈퍼 유저’ 의미
- gid: 기본 그룹 ID.
- groups: 현재 사용자가 속해 있는 모든 그룹의 목록. sudo 그룹에 포함되어 있다면, 시스템 관리 작업을 수행할 수 있는 권한이 존재한다는 뜻
- root: 시스템 관리자와 같은 권한을 가진 슈퍼유저

### 4) 사용자 이름만 추출하기

때로 id 명령어가 필요 이상의 정보를 보여 줄 때, 필요한 정보만 요청할 줄 알아야 한다.

`id -un`: 현재 사용자 ID(UID) 에 해당하는 사용자 이름만 출력

- -un: 사용자 이름만 출력하도록 하는 옵션

#### 요약

- 터미널을 열고 사용하는 방법
- 기본 명령어 사용법: echo, whoami, id
- id -un을 사용하여 특정 신원만 추출하는 방법

## 2 기본 파일 작업

### 1) 작업 환경 이해하기

`pwd`: 파일 시스템 내에서 현재 위치 표시

-print working directory 의 약자

-리눅스 파일 구조 내에서 자신의 위치를 파악하는 데 중요

- ~: 현재 사용자의 홈 디렉터리 경로를 가리킴

`ls`: 현재 위치 안의 파일 나열

`ls ~`: 홈 디렉터리 안의 파일 나열 

### 2) 파일 시스템 탐색하기

- 루트 디렉터리(/): 리눅스 파일 시스템의 가장 꼭대기(부리)에 해당하는 곳

**home/labex/project=**루트에서부터 `home` 폴더로, 그다음 `labex` 폴더로, 마지막으로 `project` 폴더까지 순서대로 경로를 따라가라.

- .. : “상위 디렉터리” 의미

`cd:` 디렉터리(폴를 변경할 때 사용하는 명령어

-Change Directory

`cd project` “project라는 이름을 가진 디렉터리로 내 현재 위치를 옮겨라”

project: 이동하고 싶은 대상 디렉터리의 이름

### 3) 파일 생성 및 디렉터리 내용 나열하기

1. 몇 개의 파일을 생성해 보자

- touch: 빈 파일 생성

`touch file1.txt`

-파일이 이미 존재할 시 내용물 건드리지 않고 수정 시간 (타임스탬프) 만 업데이트

- >(리다이렉션): 명령어의 출력 결과를 화면 대신 파일에 저장하라는 기호

```c
echo “Hello, Linux” > file2. txt
```

(1) echo “Hello, Linyx”: 화면에 "Hello, Linux"라는 글자를 출력하라는 명령어

(2) file2.txt: 출력된 글자가 저장될 파일명

#### Tip

- 만약 똑같은 명령어 (`echo “something” > file2.txt`)를 다시 입력
→ 기존의 “Hello Linux”는 사라지고 “Something”으로 **덮어쓰기** 됨
- 내용을 지우지 않고 **뒤에 덧붙이고 싶다면**…
→ > 대신 >> 사용

```c
echo "Hidden file" > .hiddenfile
```

- 리눅스에서는 점(.) 으로 시작하는 모든 파일이나 디렉터리를 숨김 항목으로 간주함
- `ls` → 목록에 .hiddenfile X
- `ls -a` → 목록에 비로소 .hiddenfile O

1. 디렉터리를 생성해 보자

```jsx
mkdir testdir
```

`mkdir [디렉터리 이름]`: [ ] 라는 이름의 새 디렉터리를 만듦.

1. 기본 목록 확인

`ls`

1. 상세 목록 확인
- -l(숫자 1 아닌 소문자L): 긴 형식의 목록을 제공하는 옵션. 파일 권한, 소유자, 크기, 수정 날짜와 같은 추가 정보를 볼 수 있다.

1. 숨김 파일 표시

`ls -a` : 점으로 시작하는 숨김 파일을 포함하여 모든 파일을 보여 줌

- -a: 숨겨진 파일을 포함한 모든 파일과 디렉터리를 보여라

1. 옵션 조합하기

`ls -la`

```jsx
labex:project/ $ ls -la
total 12
drwxr-xr-x 1 labex labex   74 May 11 14:04 .
drwxr-x--- 1 labex labex 4096 May 11 14:06 ..
-rw-rw-r-- 1 labex labex    0 May 11 14:02 file1.txt
-rw-rw-r-- 1 labex labex   13 May 11 14:03 file2.txt
-rw-rw-r-- 1 labex labex   12 May 11 14:04 .hiddenfile
drwxrwxr-x 2 labex labex    6 May 11 14:01 testdir

```

- ls -l (긴 형식으로 목록 보기) 와 ls -a (모든 항목 보기) 옵션의 조합
- 다음과 같은 정보 확인 가능

-**권한 (Permissions)**: 앞부분의 `drwxrwxr-x` 같은 문자들이 파일이나 디렉터리에 누가 접근할 수 있는지를 나타냄

-**소유자 (Owner)**: 파일이나 디렉터리를 소유한 사용자(`labex`) 표시

**-파일 크기 (Size)**: 데이터가 차지하는 용량 표시

-**수정 시간 (Timestamp)**: 마지막으로 수정된 날짜와 시간 표시

(+) 수정 시간 뒤: 파일 이름

1. 특정 디렉터리의 내용 확인

`ls -l testdir`

testdir 디렉터리 내부의 목록을 보여 줌

### 4) 파일 및 디렉터리 복사하기

1. 파일 복사

`cp file1.txt file1_copy.txt`

:현재 디렉터리에 file1.txt를 복사한 file1_copy.txt 생성

1. 파일을 다른 디렉터리로 복사

`cp file2.txt testdir/`

: file2.txt. 를 testdir 디렉터리 안으로 복사

1. 디렉터리 복사

`cp -r testdir testdir_copy`

cp -r [원본디렉터리] [대상디렉터리]

: testdir 디렉터리를 '통째로' 복사해서, 그 결과물로 (존재하지 않던) `testdir_copy`라는 이름의 디렉터리를 새로 만들어라

- -r: “ 재귀적” 의미를 가진 옵션.

디렉터리를 복사할 때는 내부의 모든 내용물도 함께 복사되도록 -r 옵션 반드시 사용

1. 복사 결과 확인

```jsx
ls
ls testdir
ls testdir_copy
```

### 5) 파일 및 디렉터리 이동 및 이름 변경하기

리눅스에서 `mv` 명령어는 이동과 이름 변경 두 가지 용도로 모두 사용됨

1. 파일 이름 변경

`mv file1.txt newname.txt`

file1.txt의 이름을 newname.txt로 변경

1. 파일을 디렉터리로 이동

`mv newname.txt testdir/`

newname.txt 파일을 testdir 디렉터리 안으로 이동

1. 디렉터리 이름 변경

`mv testdir_copy new_testdir`

testdir_copy 디렉터리 이름을 new_testdir로 변경

1. 이동과 이름 변경을 동시에 수행

`mv testdir/newname.txt ./original_file1.txt`

testdir 안에 있는 newname.txt 를 밖으로 꺼내며

현재 디렉터리에 original_file1.txt 라는 이름으로 저장

주의: 현재 위치에 original_file1.txt 라는 파일이 **이미 존재할 시** 기존 파일은 흔적도 없이 사라지고 newname.txt  의 내용으로 **덮어쓰기** 됨

1. 변경 사항 확인

```jsx
ls
ls testdir
```

### 6) 파일 및 디렉터리 삭제하기

`rm` : 파일을 삭제하는 명령어

1. 단일 파일 삭제

`rm original_file1.txt`

1. 대화형 삭제 (더 안전한 방법)
- -i: 파일 삭제 전 매번 확인을 요청하는 옵션. 삭제 승인 시 y 입력 후 엔터. n 혹은 다른 키 누를 시 파일 삭제 X

1. 비어 있는 디렉터리 삭제

`rmdir` : (remove directory) 비어 있는 디렉터리에만 작동

`ls new_testdir`

로 파일 확인 시 비어 있다면(파일이 보이지 않는다면) `rmdir` 을 사용하여 삭제 가능.

비어 있지 않다면 new_testdir 은 삭제되지 않는다. (ex `rmdir: failed to remove 'testdir': Directory not empty` 오류 메시지 나타남)

1. 디렉터리와 그 내용물을 모두 삭제 (재귀적 삭제)

`rm -r [디렉터리이름]` : [] 디렉터리와 그 안에 포함된 모든 하위 파일 및 디렉터리를 강제로 삭제하라

1. 강제 삭제 (극도로 주의하여 사용)

`rm -rf` : 실행하기 전 무엇을 삭제하는지 100% 확신해야 함. 날아간 데이터나 파일 복구 불가.

- -f: 쓰기 방지된 파일이라도 묻지 않고 삭제하는 옵션

## 3 파일 내용 확인 및 비교

### (1) 파일 내용 출력하기

`cat [파일명]` : 파일의 전체 내용을 한 번에 출력

### (2) 줄 번호와 함께 파일 내용 표시하기

`cat -n [파일명]` 

-파일의 내용이 길어질 때 특정 위치를 지칭해야 하는 경우 유용

EX) → 1 Hi,

          2 I am Labby!

- -n: cat에게 출력되는 모든 줄에 번호를 붙이도록 지시하는 옵션

### (3) 파일의 앞부분 출력하기

`head`: 파일의 시작 부분, 즉 ‘머리’ 부분을 확인하는 데 사용

`head -n1 [파일명]`

- -n1: 첫 번째 줄만 보여 달라고 요청하는 옵션

(1을 원하는 숫자로 바꾸면 그만큼의 줄을 확인할 수 있다.)

- 만약 -n1 옵션 없이 head 명령어만 사용하는 경우, 기본적으로 파일의 처음 10 줄을 보여 준다.

### (4) 파일의 처음 몇 바이트 확인하기

`head -c1 [파일명]`

- -c1: 파일의 첫 1 바이트 (문자 하나) 만 보여 주도록 지시하는 옵션

(1을 원하는 숫자로 바꾸면 그 바이트 수만큼 볼 수 있다.)

### (5) 파일의 뒷부분 출력하기

`tail`: 파일의 끝부분, 즉 ‘꼬리’ 부분을 보여 주는 명령어

-옵션을 지정하지 않으면 `tail` 은 기본적으로 마지막 10 줄을 보여 준다.

### (6) 파일의 마지막 몇 바이트 확인하기

`tail -c1 [파일명]` 시 아무것도 출력되지 않는 것처럼 보인다면, 파일의 마지막 문자가 줄 바꿈 문자일 가능성 높음.

→ 대신 마지막 2 바이트를 확인해 보자

`tail -c2 [파일명]`

### (7) 파일 비교하기

`diff` : 첫 번째 파일을 두 번째 파일과 동일하게 만들기 위해 어떤 변경이 필요한지 설명하는 명령어.

-수정 사항을 검토하거나 코드를 비교할 때 자주 쓰임

```c
labex:project/ $ diff file1 file2
1c1
< this is file1
---
> this is file2

```

- `1c1` : 첫 번째 파일의 1 행이 두 번째 파일의 1 행과 일치하도록 변경되어야 함을 나타낸다
- `< this is file1` : < 기호는 첫 번째 파일 (file1) 의 내용을 나타냄
- `---` : 두 파일의 내용을 구분하는 구분선
- `> this is file2` : > 기호는 두 번째 파일 (file2) 의 내용을 나타냄

-위 코드는 file1 을 file2와 똑같이 만들려면 “this is file1” 이라는 줄을 “this is file2”로 바꿔야 한다는 뜻

### (8) 디렉터리 비교하기

diff 명령어를 사용하여 디렉터리 전체를 비교해 보자.

`diff -r ~/Desktop ~/Code`

-r 옵션은 하위 디렉터리까지 포함하여 재귀적으로 비교하도록 diff 에 지시함. ~/Desktop 과 ~/Code 는 비교할 두 디렉터리의 경로.

결과 예시

```c
Only in /home/labex/Desktop: code.desktop
Only in /home/labex/Desktop: gedit.desktop
Only in /home/labex/Desktop: gvim.desktop
Only in /home/labex/Desktop: xfce4-terminal.desktop
```

이 출력은 Desktop 디렉터리에는 있지만 Code 디렉터리에는 없는 4개의 파일을 보여 줌.
