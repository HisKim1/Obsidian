## 2. UNIX/LINUX Basics
![[Pasted image 20241006143613.png|400]]
### Kernel
: sys의 <font color="#0d73ff">모든 task를 control</font>하는 the core of the system
- initialize the device drivers
- manages processor, data/file access and storage
- performs all HW access
- loaded into mem. at sys. startup
### Shell 
: The <font color="#0d73ff">interface</font> btw the kernel and user 
- interprets cmd typed by a user
- executes user cmds
- supports a custom env. for each user $\to$ can define their own env.
- $\not\exists$ in Windows, but $\exists$ in Linux
### System Calls
: their funcs are implemented되었을 때의 <font color="#0d73ff">entry points into kernel code</font>
  kernel에서 제공하는 func를 부르기 위한 / 주로 kernel mode에서 실행
### Library Functions
: desired functions를 user code로 transfer해주는 역할
  <font color="#0d73ff">user space에서</font>, sys call이나 다른 lib func를 부르는 데에 사용

---
### Shell
: a program that
- accepts inputs from the user
- runs / manages programs for the user
- often supports limited programming
$\to$ 대부분의 OS는 shell을 갖고 있음

e.g. sh, csh, ksh, bash, tcsh, zsh (`echo $shell` 하면 어떤 쉘인지 확인 가능)

### Standard I/O
: 모든 Unix/Linux는 <font color="#0d73ff">standard file streams</font> $\simeq$ <font color="#0d73ff">standard file descriptor</font>를 3개 갖고 있다
1. **standard<font color="#0d73ff"> input</font>** / `stdin` file stream / file descriptor **0**
    terminal에 printed된 info.를 읽기 위한 primary input stream
   
2. **standard <font color="#0d73ff">output</font>** / `stdout` file stream / file descriptor **1**
    terminal에 output할 info & prog.를 print하기 위한 primary output stream
   
3. **standard <font color="#0d73ff">error</font>** / `stderr` file stream / file descriptor **2**
    terminal에 print할 info.를 위한 primary error stream
    error 1) resulted from an error in processing
    error 2) should not be considered part of the prog. output

### File Descriptors
: kernel에서 file을 identify하기 위한 small, non-neg. int. 
$\to$ shell은 any file descriptor를 redirect할 수 있다다

### Pipes, | 
: <font color="#0d73ff">message passing</font> 이용한 <font color="#0d73ff">inter-process communication</font>;
  앞 prog. output을 pipe로 다음 prog.의 input으로
$\to$ proc. seq.를 parallel하게 execute 
$\to$ series complete될 수 있게 dependency 부여
![[시프 날로 A+ 먹어버리기 2024-10-06 14.59.23.excalidraw|700]]  

### Redirection
: redirect the std file streams to a file on the filesystem
- **Output Redirection (>):** <font color="#0d73ff">Sends the output</font> of a command to a file (<font color="#0d73ff">overwrites</font> the file).
- **Input Redirection (<):** <font color="#0d73ff">Takes input </font>for a command from a file.
- **Append Redirection (>>):** <font color="#0d73ff">Appends the output </font>of a command to a file.

note. 
**>** 랑 **<** 가 pipe보다 우선시 된다. redirect되고 남은 게 pipe 뒤로 넘어가.

e.g.
`$ cmd < input_file > output_file 2> error_file`
: `cmd` 실행할 때 input은 `input_file`를 사용하고, 
  출력 중에서 `stdout`은 `output_file`에, `stderr`는 `error_file`에 저장
  
`$ cmd < input_file | cmd2 2> error_file | cmd3 > output_file`
: 

### Files
1. ordinary files
     text, data, prog. 담은 / within or under a dir. file
     다른 files나 dir.를 contain할 수 없음
2. directory files
     other files & dir. list를 갖고 있는 file
     filename, inode number $\in$ dir. file
3. special files
     *device is dealt with as a file.*

### Directories
**directory entry**: mapping btw inode and filename
**directory**: directory entries를 contain하는 special files

`~`: home dir  / `.`: current working dir / `..`: 하나 상위 working dir

absolute path: `/home/ubuntu/a.txt` (`/`부터 시작할 때)
relative path: `usr/bin/xv`

### Wildcard
- `?`: 단일 문자와 일치
     `ls file?.txt   # file1.txt, fileA.txt 등과 일치`
     
- `*`: 0개 이상의 문자와 일치
     `ls *.jpg       # 모든 .jpg 파일과 일치`
	 `ls doc*        # doc로 시작하는 모든 파일과 일치`
	 
- `[]`: 대괄호 안의 문자 중 하나와 일치
     `ls [abc]*.txt  # a, b, 또는 c로 시작하는 모든 .txt 파일과 일치`
	 `ls file[0-9].txt  # file0.txt부터 file9.txt까지 일치`
	 
- `!`: 대괄호 내에서 사용 시 해당 문자 집합의 부정을 나타냄
     `ls [!a]*.txt   # a로 시작하지 않는 모든 .txt 파일과 일치`
  
- `{}`: 쉼표로 구분된 패턴 목록과 일치
     `ls {*.jpg,*.png}  # 모든 .jpg 및 .png 파일과 일치`
	 `mv {file1.txt,file2.txt} /backup/  # file1.txt와 file2.txt를 /backup/ 디렉토리로 이동`

### Processes and Signals
- **Processes** 
    Programs <font color="#0d73ff">executing in memory</font>
    - Identified by a unique Process ID (PID)
    - `fork()` system call로 생성
    - Loaded into memory using `exec()` functions
    - Controlled by `fork()`, `exec()`, and `wait()`
- **Signals**
     Notify a process that <font color="#0d73ff">a condition has occured</font>
    - Can have a default action, be ignored, or be caught and handled by a user-defined function.

### Others
- **User Identification**
     User IDs (UIDs) and Group IDs (GIDs)를 자연수로 할당
     GID에는 primary, secondary 있음
  
- **Unix Time** 
    Measured in seconds since the Unix epoch (Jan 1, 1970, 00:00:00 GMT)

- **Process Time** 
    CPU time used by a process, measured in clock ticks.

---
## 3. Tools in Linux
### Linux Commands
- `date/cal`: 현재 날짜/시간 표시 / 이번 달 달력 표시
- `clear`: 터미널 화면 지우기
- `whoami`: 현재 로그인한 사용자 (본인) 확인
- `who`:  현재 로그인한 모든 사용자 확인
- `exit`: 현재 세션에서 로그아웃
- `pwd`: 현재 작업 디렉토리 경로 출력
- `ls [-la]`: 디렉토리 목록 표시 [숨김 파일 포함 상세 목록]
- `cd dir`: 디렉토리 변경
- `mkdir/rmdir dir`: 디렉토리 생성/삭제
- `man command`: 명령어 매뉴얼 표시
- `cp/mv/rm [-r] file`: 파일 복사/이동/삭제
- `grep [-r] pattern files`: 파일에서 패턴 검색
- `cat`: 파일 내용 출력 및 연결
- `vi/vim`: 프로그래머용 텍스트 에디터
- `chmod/chown`: 파일 권한/소유자 변경
- `ps`: 현재 실행 중인 프로세스 표시
- `kill pid`: 특정 PID의 프로세스 종료
- `file filename`: 파일 형식 확인
- `which app`: default로 실행되는 app의 경로
- `whereis app`: app으로 쓸 수 있는 모든 경로
- `df`: disk utilization 표시
- `du`: 특정 파일, 경로의 사용 용량 표시

### Ownership & Permissions
#### chown
파일/디렉토리 소유권 변경
```
chown <options> USER[:GROUP] <file>
```
e.g.
`chown jeany:jeany integer.c`
=`chown 1001:1003 integer.c`
`id jeany` 쳤을 때 나오는 int로 owner 바꿀 수 있다
#### chmod
파일/디렉토리 권한 변경
```
chmod <class><operator><mode> <file>
```
- class: u(user), g(group), o(other), a(all)
- operator: +, -, =
- mode: r, w, x 또는 조합
e.g.
`chmod 755 integer.c`
`chmod u=rwx, g-w+x, o+x integer.c`

### Vim
1. 일반 모드 (Normal mode)
2. 입력 모드 (Edit mode)
3. 명령 모드 (Command mode)
4. 비주얼 모드 (Visual mode)

### 주요 Vim 명령어
- 일반 모드:
  - `i`, `a`, `o`, `r`: 입력 모드로 전환
  - `w`, `b`, `e`: 단어 단위 이동
  - `/`, `?`: 검색
  - `d`, `y`, `p`: 삭제(잘라내기), 복사, 붙여넣기
  - `u`, `Ctrl+r`: 실행 취소, 재실행

- 명령 모드:
  - `:w`, `:q`, `:wq`: 저장, 종료, 저장 후 종료
  - `:set nu`: 줄 번호 표시
  - `:%s/old/new/g`: 전체 파일에서 문자열 치환

- 비주얼 모드:
  - `u`, `U`: 소문자/대문자 변환
  - `d`, `y`: 선택 영역 삭제/복사
  - `>`, `<`: 들여쓰기/내어쓰기

### SW dev. tools
1. Compiler Toolchain
2. `gdb`: debugging
3. `make`: project build management, maintain prog. dependencies
4. `diff` & `patch`: report and apply differences btw files
5. `screen`: terminal multiplexer
6. `git`: distributed project management, version control

### Compiler
: high-level programming language로 되어 있는 source code를 machine code로 translate해주는
![[시프 날로 A+ 먹어버리기 2024-10-06 18.01.16.excalidraw|300]]
### GCC (GNU Compiler Collection)
gcc: C 코드 컴파일
g++: C++ 코드 컴파일

**Procedure**
`program.c`로 출발
1. preprocessing
     `cpp program.c program.i`
     =`cc -v -E program.c > program.i`
     $\Rightarrow$ `program.i` 생성
     
2. compilation
     `cc -v -S program.i`
     $\Rightarrow$ `program.s` 생성
     
3. assembly
     `as -o program.o program.s`
     $\Rightarrow$ `program.o` 생성
     
4. linking
     `ld program.o`

- 주요 옵션:
  - `-c`: 링킹 없이 컴파일
  - `-o <filename>`: 출력 파일 이름 지정
  - `-g`: 디버깅 정보 포함
  - `-Wall`: 모든 경고 표시
  - `-Werror`: 경고를 에러로 취급
  - `-O`: 최적화

```bash
$ cc hello_world.c
# 기본 컴파일: a.out 실행 파일 생성

$ cc -c hello_world.c
# 컴파일만 수행: hello_world.o 오브젝트 파일 생성

$ cc -E hello_world.c
# 전처리만 수행: 전처리된 코드를 화면에 출력

$ cc -S hello_world.c
# 어셈블리 코드 생성: hello_world.s 파일 생성

$ cc hello_world.c -o hello_world
# 출력 파일 이름 지정: hello_world 실행 파일 생성

$ cc -g hello_world.c -o hello_world
# 디버깅 정보 포함: 디버깅 가능한 hello_world 실행 파일 생성

$ cc hello_world.c -o hello_world -I../include
# 추가 헤더 파일 경로 지정: ../include 디렉토리의 헤더 사용

$ cc hello_world.c -o hello_world -lmath
# 수학 라이브러리 링크: math 라이브러리를 사용한 실행 파일 생성

$ cc hello_world.c -o hello_world -Llib
# 라이브러리 검색 경로 추가: lib 디렉토리에서 라이브러리 검색
```

### gdb; debugging tool
**breakpoint**
: stop on specified conditions
**backtrace**
: prog.이 stop했을 때 examine what has happened 
**stepping**
: inspect control flow

- `break`: 브레이크포인트 설정
- `run`: 프로그램 실행
- `step`/`next`: 한 줄씩 실행
- `continue`: 다음 브레이크포인트까지 실행
- `print`: 변수 값 출력
- `backtrace`: 스택 추적

### make & Makefile; 
Unix tool to <font color="#0d73ff">simplify building</font> prog. executables from many modules

##### Make
user가 만든 **Makefile**에서 규칙 파악하여 **make**로 필요한 obj나 executable만 re-built하는 
c.f. CMake: for large projects / cross platform build sys.
##### Makefile
<font color="#0d73ff">avoid having to rebuild the entire proj.</font> 하도록 *dependency graph* 통해 <font color="#0d73ff">selective rebuild</font>
macros & suffices로 simplified rule 사용 가능

Makefile format: 아래 2줄을 세트로 <font color="#0d73ff">rule</font>
```makefile
target: dependencies
    commands
```
- target: obj., executable file list
- dependencies: target이 dep.하는 source, obj. files
- commands: dependency따라 obj. file 생성하는 Unix 명령어

e.g.
```makefile
# comment indicated by the character #

# Macro: 자주 사용되는 부분을 변수처럼 저장 후 사용
# 사용법 ${NAME} / $(NAME) / $NAME
CC = gcc
CFLAGS = -g -Wall
OBJ = main.o print.o hello.o

# Rule
hello: $(OBJ)
    $(CC) $(OBJ) -o hello
```

```ad-question
1. Tools in Linux2 p.23
   OBJ 정의할 때 $\eqqcolon$ 써도 됨?
```

##### Rule 
1. pattern rule
```Makefile
# src와 obj가 같은 이름을 가질 때
# % wildcard로 대체

%.o: %.c 
        $(cc) $(FLAGS) -c $<    # $<: 첫번째 dependency file
```
2. suffix rule
```Makefile
# *.c를 *.o로 바꿀 때 
# 바로 위에 거랑 같은 역할을 수행하는 듯?

.c.o:
        $(cc) $(FLAGS) -c $<
```
1. special macros
	1. `$*` basename of current target
	2. `$<` 1st current dependency file name
	3. `$^` all dependents names
	4. `$@` current target name
	5. `$?` 
```ad-question
4. Tools in Linux2 p.25
`$?`가 뭔지 잘 안 와닿음...
```

### screen; terminal multiplexer
여러 터미널 세션을 하나의 콘솔에서 관리할 수 있게 해주는
screen에서 실행된 proc는 보이지 않고, disconnected되더라도 계속 실행됨

주요 명령어:
- `screen`: 새 screen 세션 시작
- `Ctrl+a c`: 새 창 생성
- `Ctrl+a n`: 다음 창으로 이동
- `Ctrl+a d`: 현재 세션 분리 (detach)

### diff(1) & patch(1); file compare and update

- `diff`: 파일 간 차이점을 라인 단위로 비교 $\to$ output이 `patch` file
- `patch`: diff 파일을 이용해 원본 파일에 변경 사항 적용
![[Pasted image 20241009103800.png]]
### git
- `git init`: 새 저장소 초기화
- `git clone [URL]`: 원격 저장소 복제
- `git add [file]`: 파일을 스테이징 영역에 추가
- `git commit -m "[message]"`: 변경 사항 커밋
- `git push`: 로컬 변경 사항을 원격 저장소에 업로드
- `git pull`: 원격 저장소의 변경 사항을 로컬로 가져오기

```ad-question
4.Tools in Linux2
tool 5개 뒤에 (1) 숫자는 왜 붙어있는거? 의미가 있는건가?
```

---
## 4. Shell Programming
### Shell
An <font color="#0d73ff">interface</font> between the user and the kernel
interpret cmd $\to$ execute cmd
$\Rightarrow$ 사용자별로 custom env.를 지원

### Shell Programming
Writing <font color="#0d73ff">sequences of commands</font> in a file for later execution

### Shell Type
- `sh $` Bourne Shell / 가장 흔한 / 제약적
- `ksh $` Korn Shell / superset of `sh`
- `bash $` Bourne-Again Shell / `sh`+`csh` / <font color="#0d73ff">Linux default</font>
- `csh %` C Shell / `sh`-extended / c-like syntex
- , `tcsh %` `csh`-extended
$\to$ `chsh -s path`로 사용할 shell 바꿀 수 있음 / 미묘하게 다르다

### Shell Script
collection of shell cmds stored in a file

#### Shell Script 단점 (쓰면 안되는 상황)
1. <font color="#0d73ff">resourse-intensive</font> (sort, hash, etc.)
2. $n$-dim <font color="#0d73ff">array나 data structure</font> 써야 할 때
3. floating point, precision cal., $\mathbb{C}$ $\Rightarrow$ heavy-duty <font color="#0d73ff">math</font>할 때
4. cross-platform <font color="#0d73ff">portability</font> btw diff. shell
5. <font color="#0d73ff">security</font>가 중요할 때 ($\because$ txt라 누구나 볼 수 있다)
6. <font color="#0d73ff">GUI, graphic</font>이 필요할 때
7. <font color="#0d73ff">HW</font>에 direct access 필요할 때
8. <font color="#0d73ff">port나 socket I/O</font> 필요할 때 

#### Shell Script 장점
1. **Task Automation**
   자주 사용되는 operation을 automate
2. **Combining Multiple Commands**
   여러 cmd를 single cmd처럼 실행
3. **Easy to Use**
   write, debug가 쉽다
4. **Transparency**
   진행상황을 쉽게 확인 가능
5. **Portable**
   같은 shell이라면 얼마든지
   
### Shell Script Basics
- **Hashbang (#!)** 
  Specifies the interpreter for the script (e.g., `#!/bin/bash`)
  `.sh`이면 무조건 hashbang + shell 경로로 시작해야 함
- **Execution**
  1. 실행 권한 부여: `chmod a+x [script file name]`
     
  2. 실행 shell 결정 후 실행
    1. <font color="#0d73ff">새로운 shell</font> 열어서 사용
       `./sample.sh`
       `bash sampble.sh`
       
    2. 현재 터미널에서 <font color="#0d73ff">쓰던 shell 그대로</font> 사용
       $\to$ 내가 선언해놓은 `variable` 이어서 사용 가능
       `. sample.sh`
       `source sample.sh`
       
### Variables
1. (global) **Environment Variables**
	<font color="#0d73ff">모든 shell이 공통</font>으로 갖게 되는 variables
	= system shell이 생성될 때 <font color="#0d73ff">상속</font>받아
	(대문자로 작성하는 convention)
	e.g. `NAME=value; export NAME` or `export NAME=value`
	
2. (local) **User-defined** or **Shell Variables**
   현재 사용 중인 shell에만 적용
   $\to$ 다른 proc.로 전달 X
```ad-question
5.Shell Programming1 p.23
"not passed to other processes"
shell을 process라고 보는 건가? 
```

#### 주요 Env. Var.
##### `HOME`
path to your <font color="#0d73ff">home directory</font>
e.g. `$HOME=/home/hiskim1`
##### `PATH`
paths <font color="#0d73ff">to be searched</font> for command
$\to$ cmd를 입력하면 shell은 `$PATH`에서 해당 prog.을 찾아 실행
e.g. `$PATH=/usr/bin:/usr/ucb:/usr/local/bin`
where `:/` is "append"

### Array
```bash
#! /bin/bash

# declare 1D-array
# idx starts from 0
Y=(abc 1 123 xyz)

echo ${Y[2]}
# output: 123
Y[2]=3

echo ${Y[2]}
# output: 3

# all list elements
echo ${Y[@]}
# output: abc 1 3 xyz

# # of list elements
echo ${#Y[@]}
# output: 4
```

### Quotation
#### Single Quotation, \'    \'
<font color="#0d73ff">있는 그대로 출력</font>함
```bash
#! /bin/bash

myvar="This is my var"

echo `$myvar`
# output: $myvar
```

#### Double Quotation, \"     \"
Python에서 f"    "같은 거
안에 들어가 있는 <font color="#0d73ff">variable을 대체</font>해서 실행됨
```bash
#! /bin/bash

myvar="This is my var"

echo "$myvar"
# output: This is my var
```

#### Back Quotation, \`     \`
<font color="#0d73ff">command substitution</font> 용도 
= back quotation 안의 <font color="#0d73ff">cmd를 실행</font>하여 그 <font color="#0d73ff">결과값을 전달</font>
note: `bash`에서 `$(pwd)`$\simeq$\``pwd`\`
```bash
#! /bin/bash

echo `pwd`
# 1. pwd 실행
# 2. back quotation이 pwd 결과값을 받아
# 3. back quotation이 가져온 결과를 echo에 전달
# 4. echo 실행
```

### Positional Parameters
`$0`: Script name
`$1`, `$2`, ... : arg. 1, 2, ...
`$#`: \# of arg.
`$*`: All arguments as a <font color="#0d73ff">single string</font>
`$@`: All arguments as <font color="#0d73ff">separate strings</font>
`$?`: Exit status of the last command
`$$`: Process ID of the current shell

```ad-question
`$*`랑 `$@`를 어떻게 구분할 수 있을까?
```

### Arithmetic Operations
```bash
#! /bin/bash

# 사용 가능한 방법
# 1. $(( ... ))
# 2. $[ ... ]

a=5; b=3;

echo $((1+2))
#output: 3

echo $[$a+$b]
# output: 8
```

#### `let` & `expr`
```bash
#! /bin/bash

# let으로 변수 선언시 integer로 취급
# 띄어쓰기 X
let c=$a-$b
echo $c
# output: 2

# expr는 다 띄어 써야 함
c=`expr $a + $b`
echo $c
# output: 15

expr "(" 4 "*" 3 ")" "*" 2
# output: 24
```

#### `bc` & `awk`
```bash
#! /bin/bash
echo "3.8 + 4.2" | bc
# output: 8.0

echo "scale=5; 2/5" | bc
# output: 0.40000

bc <<< "scale=5; 2/5"
# output: 0.40000 / call bc directly

bc -l <<< "2/5"
# output: .40000000000000000000 / 최대 소수점까지 뽑아보기

awk "BEGIN {x=100/3; y=6; z=x*y; print z}"
```

### Input
```bash
#! /bin/bash

read x
# input: "hi hello"

echo $x
# output: hi hello

read -p "Say hello: " x
# Say hello:
# input: I'm not hello

echo $x
# output: I'm not hello
```

### Redirection
32:00 ~ : "외우라는 게 아니라 이해를 했으면 좋겠다!"
- `cmd >&n` send **cmd** output to file descriptor **n**
- `cmd <&n` take input for **cmd** from file descriptor **n**
- `cmd >&-` close standard output
- `cmd <&-` close standard input
- `cmd 2> file` send standard error to **file**
    - Standard output remains the same $\to$ 터미널에 출력될 듯
- `cmd > file 2>&1`
    stdout은 **file**에, stderr는 file descriptor **1**에. 근데 fd **1**=stdout이니까 
    send both standard error and standard output to **file**
- `(cmd > file1) 2> file2` : send standard output to **file1**, and standard error to **file2**
- `cmd 3< file` : open **file** for reading on file descriptor 3

### Here document, <<
`read`는 한 줄만 입력을 받는데, 여러 줄을 받으려면?
$\to$<font color="#0d73ff"> here document, <<</font>를 사용해서 <font color="#0d73ff">delimeter가 나올 때까지</font> 계속 입력 받는다
```bash
#! /bin/bash

cat << EOF # EOF가 delimeter (구분자)
> multi-line text
> say something nothing anything
> and suddenly meet EOF
> EOF
# output
# multi-line-text
# say something nothing anything
# and suddenly meet EOF
```

```ad-question
![[Pasted image 20241009162503.png|400]]
중간에 만나더라도 잘 살아남는데,,?
```

### Built-in Commands
Internal to the shell / faster & efficient than other cmds
확인 방법
: `type -a cmd` & `command -V cmd`
$\to$ `cmd is a shell builtin`이면 built-in

```ad-question
external cmd면 shell이 *fork*해서 생긴 child proc.가 *exec*해서 cmd를 실행하고 그 결과를 parent proc.인 shell에게 return해주는데, 

internal이면 이 과정이 생략된다는 뜻?
```

### Flow Control 
condition 작성만 똑바로 어떻게 하는지 알고, 각각 문법만 알면 될 듯?
나머지는 직접 연습해보면서 익히는 게 맞다.

```ad-important
6. 51:04 저는 command substitution이랑 process substitution이 굉장히 중요하다고 생각을 해서, 그 부분을 나중에도 주의 깊게 봐줬으면 좋겠구요.
```

#### condition 작성 방법
1. `test EXPRESSION`
2. `[  EXPRESSION ]`
3. `[[ EXPRESSION ]]` $\to$ 얘만 &&, || 등 사용 가능. 얘를 default로 쓰라
<font color="#0d73ff">괄호랑 EXPRESSION 사이 공백 필수</font>!

![[Pasted image 20241009165610.png]]
$\Rightarrow$ 숫자를 flag처럼 비교하고, string을 수학처럼 비교한다

**!** : not / **&&** or **-o** : and / **||** or **-o** : or 
$\Rightarrow$ 무조건 `[[ 여기 안에 써야 함 ]]`

#### 1. if
기본 양식
```bash
if cond1; then
	action1
# elif, else는 선택사항
elif cond2; then
	action2
else
	action3
fi
```

e.g.
```bash
#! /bin/bash

# condtion에 cmd substitution을 할 수 있다!
if [[ `wc -l < "$1"` -gt 10 ]]; then
	echo "The file has more than 10 lines in it."
else
	echo "The file is nonexistent or small"
fi
```

#### 2. for
기본 양식
```bash
for variable in argment-list
do
	action
done
```

e.g.
```bash
#! /bin/bash

# case 1: array로 받을 때
params=(unix linux shell fun)

for param in "${params[@]}" # @: array elem.을 각각 str 하나로
do
	echo $param
done

# case 2: string 통으로 받을 때
params="unix linux shell fun"

for param in $params # 알아서 공백 기준으로 짤라서 가져온다
	echo $param
```

#### 3. while
```bash
while [[ EXPRESSION ]] # 이 true일 때 계속 실행
do
	action
done
```
e.g.
```bash
#! /bin/bash

cont="Y"
while [[ $cont="Y" ]]
do
	ps -A
	read -p "want to continue? (Y/N)" reply
	# tr: translate pattern
	# 여기서는 lower case를 upper case로 translate
	cont=`echo $reply | tr [:lower:] [:upper:]`
done

echo "done"
```
`tr` 관련해서 pattern은 6. p.36에서 참고

```bash
#! /bin/bash

# 이 두 while문이 같은 기능이다!
while read line
do
	echo $line
done < /etc/passwd | head


cat /etc/passwd | head | while read line
do
	echo $line
done
```

#### 4. until
```bash
while [[ EXPRESSION ]] # 이 false일 때 계속 실행
do
	action
done
```

```ad-question
6.Shell Programming2 p.40
until [ ~~~ ]; 
불필요한 자리에 ; 붙어도 문제 안 생기나?
```
#### 5. case
```bash
case str in
	pattern1) # 괄호까지가 필수! 
		action1
		;;
	pattern2)
		action2
		;;
	patternN)
		action3
		;;
esac
```
e.g.
```bash
#! /bin/bash

read -p "Enter your name: " name

case $name in
	*[0-9]*)
		echo "That doesn't seem like a name"
		;;
	A*|B*)
		echo "your name starts with A or B, cool."
		;;
	*) # 약간 default
		echo "You're not special."
		;;
esac
```

```ad-question
default같은 애가 없으면 어카나?
```
#### 6. select
*LIST*에서부터 simple menu를 만들어서 보여줘 (number: word list)
고르면 그게 *WORD*에 들어가고 그걸로 command를 쓰면 됨
(user가 입력한 input은 $REPLY에 저장)

end of input (^d, ^c)할 때까지 계속 돌아

```bash
select WORD in LIST
do
	command
done
```

e.g.
```bash
#! /bin/bash

# 기본적으로 선택지 다 보여주고 이 문장이 출력됨. 
# 따로 echo 안 해도 됨
PS3="select entry or ^D: "

select var in alpha Beta
do
	echo "$REPLY = $var"
done
```

```bash
#!/bin/bash

echo "script to make files private" 
echo "Select file to protect:" 

# *: all file list
select FILENAME in * 
do 
	echo "You picked $FILENAME ($REPLY)" 
	chmod go-rwx "$FILENAME" 
	echo "it is now private" 
done
```

#### Shift
parameter를 하나씩 pop시킨다
```bash
#! /bin/bash

echo "There are" $# "parameters” 

while [ $# -gt 0 ] 
do 
	echo -n "$1 " 
	shift 
done

echo "" 
echo "There are now" $# "parameters" 
echo "end of script"
```

### File Testing
file이 어떤 file인지 확인하는 방법
자세한 설명은 
6.shell programming2  p.49

### Shell Function
- mem에 저장되어 func을 부르는 shell과 같은 shell에서 실행됨
- .bashrc / script / cmd line에서 정의 가능

```bash
function function_name {
    commands
}
 
# or

function_name() {
    commands
}

# 함수 부를 때는 그냥 이름만
function_name 

# argment는 그냥 뒤에 이어 붙여주면 됨
function_name arg1 arg2

# 함수 없애고 싶을 땐
unset -f function_name
```

##### Function parameter
(함수 종료시 script의 `$~~` 값에는 영향 X)
`$1` ~ : function call에서 제공된 argments들
`$0`: script name (func. name 아님주의)
`$@` or `$*`: all params
`$#`: params 개수
`#?`: 가장 최근 사용한 cmd
`$$`: 현재 pid

e.g.
```bash
#! /bin/bash

checkfile()
{
	# 함수 안에서 positional param 하나씩 받을 때는 생략 가능
	for file # in $@
		if [ -f "$file" ]; then
			echo "$file is a file"
		fi
		elif [ -d "$file$" ]; then
			echo "$file is a directory"
		if
	done	
}

checkfile .
```

##### Variable Scope
1. global var.
     상속받은 하위 shell도 사용 가능
2. local var.
     내 shell에서, 어디서든 사용 가능
3. local var in funciton
     function 안에서만 사용 가능
     `local varname=hello`
e.g.
```bash
#!/bin/bash

global="This is global!"

function foo()
{
	local inside="I'm inside"
	echo $global
	echo $inside
	global="This is global in function"
}

echo $global # This is global
foo
echo $global # This is global in function
echo $inside # 출력 없음
```

##### Function Return
- 0 ~ 255 값만 사용 가능
- `$?`;가장 최근 사용한 cmd로 함수 실행 후 return 값 접근 가능
- 함수에서 return값 지정 안 했으면 bash가 마지막 func의 exit status를 알아서 받아와
    다양하게 쓰고 싶으면 stdout이나 global var 써라.

##### Redirection in Function
```bash
#! /bin/bash
function redirection_in()
{
	while read input
	{
		echo "$input"
	}
} < file_in

redirection_in

function redirection_out()
{
	output=("a" "b" "c")
	for element in "${output[@]}"
	do
		echo "$element"
	done
} > file_out

redirection_out
```

### Process Substitution
기존에 하던 redirection이랑 유사함.
process의 input/output을 file처럼 처리할 수 있도록 해주는
-  `<(list)`: Input from a process.
- `>(list)`: Output to a process.

c.f. cmd substitution, \` \` or `$()`, 어떤 value로 다른 cmd에 사용되게

e.g.
```bash
#! /bin/bash
function redirection_in_ps()
{
	wihle read -a input
	do
		echo "${input[2]} ${input[8]}"
	done
# ls 결과가 file로 저장된 후 그 file이 func. input으로 redirection 
}< <(ls -l /bin)

redirection_in_ps
```

### Recursion
가능은 한데, 하지 마라.
`FUNCNEST`: func. call stack 가능 depth 개수

### Handling Signals
`kill -signal pid`
no arg: terminate
`-1`: hangup
`-2`: interrupt with `^c`
`-9`: kill (`trap`으로 block할 수 없으셈)
`kill -l`하면 어떤 시그널 있는지 볼 수 있음

### trap; handling signal
대부분의 signal들은 terminate가 default
custom signal handler를 위한 `trap`
`trap 'cmd' signal_number`
default로 되돌리고 싶을 땐 `trap signal_number`

e.g.
`trap 'echo dont hang up' 1`: `kill -1` 받으면 echo나 해라

### Debuging Shell
- `echo`: Print values for debugging.
- `set -x`: Print commands as they are executed.
    어떻게 실행되었는지 확인할 때 하면 좋은
- `set -v`: Print shell input lines as they are read.
    읽은 문장 다음 출력 나오게
- `set +x`: Turn off tracing.
- `set +v`: Turn off verbose mode.
원하면 첫 줄에 써도 됨; `#! /bin/bash -xv`