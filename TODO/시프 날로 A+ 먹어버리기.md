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
- `cp/mv/rm [-r] file`: 파일 복사/이동/삭제 [디렉토리]
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
     
2. compilation
     `cc -v -S program.i`
     
3. assembly
     `as -o program.o `
4. linking

- 주요 옵션:
  - `-c`: 링킹 없이 컴파일
  - `-o <filename>`: 출력 파일 이름 지정
  - `-g`: 디버깅 정보 포함
  - `-Wall`: 모든 경고 표시
  - `-Werror`: 경고를 에러로 취급
  - `-O`: 최적화

### 3.5.2 gdb(1) - 디버깅 도구

GDB를 사용하면 프로그램 실행 중 내부 상태를 검사하고 제어할 수 있습니다.

주요 명령어:
- `break`: 브레이크포인트 설정
- `run`: 프로그램 실행
- `step`/`next`: 한 줄씩 실행
- `continue`: 다음 브레이크포인트까지 실행
- `print`: 변수 값 출력
- `backtrace`: 스택 추적

### 3.5.3 make(1) - 프로젝트 빌드 관리

Make는 여러 모듈로 구성된 프로그램의 빌드 프로세스를 자동화합니다.

Makefile 기본 구조:
```makefile
target: dependencies
    commands
```

주요 개념:
- 타겟: 생성할 파일
- 의존성: 타겟 생성에 필요한 파일들
- 명령: 타겟을 생성하는 쉘 명령어

매크로 사용 예:
```makefile
CC = gcc
CFLAGS = -g -Wall
OBJ = main.o print.o hello.o

hello: $(OBJ)
    $(CC) $(OBJ) -o hello
```

### 3.5.4 diff(1)와 patch(1) - 파일 비교 및 패치

- `diff`: 파일 간 차이점을 라인 단위로 비교
- `patch`: diff 파일을 이용해 원본 파일에 변경 사항 적용

[[이미지 첨부]]

### 3.5.5 screen(1) - 터미널 멀티플렉서

여러 터미널 세션을 하나의 콘솔에서 관리할 수 있게 해주는 도구입니다.

주요 명령어:
- `screen`: 새 screen 세션 시작
- `Ctrl+a c`: 새 창 생성
- `Ctrl+a n`: 다음 창으로 이동
- `Ctrl+a d`: 현재 세션 분리 (detach)

### 3.5.6 git(1) - 분산 버전 관리 시스템

Git은 프로젝트의 변경 이력을 관리하고 여러 개발자의 협업을 지원합니다.

주요 명령어:
- `git init`: 새 저장소 초기화
- `git clone [URL]`: 원격 저장소 복제
- `git add [file]`: 파일을 스테이징 영역에 추가
- `git commit -m "[message]"`: 변경 사항 커밋
- `git push`: 로컬 변경 사항을 원격 저장소에 업로드
- `git pull`: 원격 저장소의 변경 사항을 로컬로 가져오기

UNIX/LINUX는 텍스트 기반의 다중 사용자 운영 체제로, 수천 개의 명령어를 동시에 실행할 수 있지만 초기 학습 곡선이 매우 가파릅니다.

## 4. Shell Programming
#### 4.1 Introduction

- **Shell:** An interface between the user and the kernel.
- **Shell Scripting:** Writing sequences of commands in a file for later execution.
- **Popular Shells:** `sh`, `ksh`, `bash`, `csh`, `tcsh`.
- **When to Avoid Shell Scripts:** For resource-intensive tasks, complex data structures, heavy math, cross-platform needs, security-critical applications, extensive file operations, GUI programming, or direct hardware access.
- **Why Use Shell Scripts?** For task automation, combining commands, ease of use, transparency, and portability.

#### 4.2 Shell Script Basics

- **Shebang (#!):** Specifies the interpreter for the script (e.g., `#!/bin/bash`).
- **Execution:**
    - Make the script executable: `chmod a+x [script file name]`
    - Run the script: `./[script file name]`
- **Running within the current shell:** `source [script file name]` or `. [script file name]`
- **Special Characters:** `#`, `$`, `\`, `{ }`, `;`, `;;`, `.`, `$?`, `$$`, `[ ]`, `[[ ]]`, `$[ ]`, `(( ))`, `||`, `&&`, `!`.
- **Variables:**
    - **Environment Variables:** Global variables available to all processes.
        - Set using `export NAME=value` or `NAME=value; export NAME`
    - **Shell Variables:** Local to the current shell.
        - Set using `NAME=value`
    - **Accessing Variables:** Use `$NAME` (e.g., `echo $PATH`)
    - **Important Environment Variables:** `PATH`, `HOME`, `USER`, `SHELL`, `DISPLAY`, `EDITOR`, etc.
- **Arrays:**
    - Create: `NAME=(value1 value2 ...)`
    - Access: `echo ${NAME[index]}` (all elements: `${NAME[@]}`)
    - Count: `echo ${#NAME[@]}`

#### 4.3 Quotation, Parameters, and Arithmetic

- **Quotation:**
    - **Single Quotes (''):** Literal interpretation.
    - **Double Quotes (" "):** Variable expansion.
    - **Back Quotes (``) or $( ):** Command substitution.
- **Positional Parameters:** Special variables for command-line arguments.
    - `$0`: Script name.
    - `$1`, `$2`, ...: Arguments 1, 2, ...
    - `$#`: Number of arguments.
    - `$*`: All arguments as a single string.
    - `$@`: All arguments as separate strings.
    - `$?`: Exit status of the last command.
    - `$$`: Process ID of the current shell.
- **Arithmetic Operations:**
    - **Integer Arithmetic:**
        - `$((expression))`
        - `$[expression]`
        - `let "expression"`
        - `expr expression`
    - **Floating-Point Arithmetic:** Requires external tools like `bc` or `awk`.

#### 4.4 Input, Redirection, and Here Documents

- **Input:** `read` command prompts the user for input.
    - `read varname`: Reads input into the variable `varname`.
    - `read -p "prompt" varname`: Displays a prompt before reading.
- **Redirection:**
    - `>&n`: Redirect output to file descriptor `n`.
    - `<&n`: Redirect input from file descriptor `n`.
    - `>&-`: Close standard output.
    - `<&-`: Close standard input.
    - `2> file`: Redirect standard error to `file`.
    - `> file 2>&1`: Redirect both stdout and stderr to `file`.
    - `(command > file1) 2> file2`: Redirect stdout to `file1` and stderr to `file2`.
- **Here Documents:** For providing multi-line input to a command.
    
    ```
    command << delimiter
    input line 1
    input line 2
    ...
    delimiter
    ```
    

#### 4.5 Built-in Commands and Flow Control

- **Built-in Commands:** Internal to the shell, faster than external commands.
    - Use `type -a command` or `command -V command` to check if a command is built-in.
- **Flow Control:**
    - **Conditionals (if-then-else):**
        
        ```
        if condition; then
            commands
        elif condition; then
            commands
        else
            commands
        fi
        ```
        
    - **Loops:**
        - **for loop:** Iterates over a list of values.
            
            ```
            for variable in list; do
                commands
            done
            ```
            
        - **while loop:** Executes commands as long as a condition is true.
            
            ```
            while condition; do
                commands
            done
            ```
            
        - **until loop:** Executes commands as long as a condition is false.
            
            ```
            until condition; do
                commands
            done
            ```
            
    - **Switches:**
        - **case statement:** Multi-way branching based on pattern matching.
            
            ```
            case variable in
                pattern1)
                    commands
                    ;;
                pattern2)
                    commands
                    ;;
                *)
                    commands
                    ;;
            esac
            ```
            
        - **select statement:** Creates a simple menu-driven prompt.
            
            ```
            select choice in list; do
                commands
            done
            ```
            

#### 4.6 Shell Functions, Signals, and Traps

- **Shell Functions:** Group commands for reuse within a script.
    
    ```
    function function_name {
        commands
    }
    # or
    function_name() {
        commands
    }
    ```
    
    - Can be defined in `.bashrc`, within the script, or on the command line.
    - Provide modularity, reusability, and improve readability.
    - Faster than separate scripts.
    - Removed using `unset -f function_name`.
    - Arguments are accessed like positional parameters (`$1`, `$2`, ...).
    - Return values using `return n` (exit status) or by printing to stdout.
    - **Local Variables:** Use the `local` keyword to limit a variable's scope to the function.
- **Signals:** Software interrupts sent to a process.
    - `kill -signal pid`: Sends a signal to a process.
- **Traps:** Used to catch and handle signals.
    - `trap 'commands' signals`: Executes `commands` when `signals` are received.
    - `trap '' signal`: Resets the handler for `signal` to its default.

#### 4.7 Process Substitution

- **Process Substitution:** Treats the input or output of a process as a file.
    - `<(list)`: Input from a process.
    - `>(list)`: Output to a process.
- **Example:** `diff <(ls /bin) <(ls /usr/bin)` compares the output of two `ls` commands.

#### 4.8 Recursion and Debugging

- **Recursion:** Bash functions can call themselves recursively.
    - Can lead to stack overflows if not used carefully.
- **Debugging Shell Scripts:**
    - `echo`: Print values for debugging.
    - `set -x`: Print commands as they are executed.
    - `set -v`: Print shell input lines as they are read.
    - `set +x`: Turn off tracing.
    - `set +v`: Turn off verbose mode.

Please note that this response is based solely on the provided source material and does not include information about Real UID, effective UID, Inode components, `stat`, `lstat`, `fstat`, `fstatat` differences, kernel mode vs. user mode, or the `link`, `symlink`, and `rename` commands. You may want to consult external resources or your course materials for information on those topics.