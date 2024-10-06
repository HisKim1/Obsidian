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
1. standard<font color="#0d73ff"> input</font> / `stdin` file stream / file descriptor 0
   : terminal에 printed된 info.를 읽기 위한 primary input stream
2. standard <font color="#0d73ff">output</font> / `stdout` file stream / file descriptor 1
   : terminal에 output할 info & prog.를 print하기 위한 primary output stream
3. standard <font color="#0d73ff">error</font> / `stderr` file stream / file descriptor 2
   : terminal에 print할 info.를 위한 primary error stream
   error 1) resulted from an error in processing
   error 2) should not be considered part of the prog. output

### Pipes, | 
: <font color="#0d73ff">message passing</font> 이용한 <font color="#0d73ff">inter-process communication</font>;
  앞 prog. output을 pipe로 다음 prog.의 input으로
$\to$ proc. seq.를 parallel하게 execute 
$\to$ series complete될 수 있게 dependency 부여

  


- **Redirection:**
    - **Output Redirection (>):** Sends the output of a command to a file (overwrites the file).
    - **Input Redirection (<):** Takes input for a command from a file.
    - **Append Redirection (>>):** Appends the output of a command to a file.
- **Files and Directories:**
    - The UNIX filesystem is a tree structure with '/' as the root directory.
    - Directories map filenames to inodes.
    - Absolute paths start with '/', while relative paths do not.
    - **Types of Files:** Ordinary files, Directory files, Special files (for I/O devices).
- **Listing Files:** The `ls` command lists files in a directory.
    - You can use wildcards like '?', '*', '[ ]', '!', and '{ }' to specify file patterns.
- **User Identification:** User IDs (UIDs) and Group IDs (GIDs) are used for identification and permissions.
- **Unix Time:** Measured in seconds since the Unix epoch (Jan 1, 1970, 00:00:00 GMT).
- **Process Time:** CPU time used by a process, measured in clock ticks.

#### 2.3 Processes and Signals

- **Processes:** Programs executing in memory.
    - Identified by a unique Process ID (PID).
    - Created using the `fork()` system call.
    - Loaded into memory using `exec()` functions.
    - Controlled by `fork()`, `exec()`, and `wait()`.
- **Signals:** Notify a process of an event.
    - Can have a default action, be ignored, or be caught and handled by a user-defined function.

## 3. Tools in Linux

#### 3.1 Important Commands (Beyond Basics)

- `chown`: Changes file/directory ownership.
- `chmod`: Changes file/directory permissions.
- `vim`: A powerful text editor.
- `gcc`: The GNU C/C++ compiler.
- `gdb`: A debugger for analyzing program execution.
- `make`: A build tool for managing projects with multiple source files.
- `screen`: A terminal multiplexer for managing multiple terminal sessions.
- `diff`: Compares files line by line and generates a patch file.
- `patch`: Applies a patch file to a source file.
- `git`: A distributed version control system.

#### 3.2 Vim Text Editor

- **Modes:**
    - **Command Mode:** For entering commands.
    - **Visual Mode:** For selecting text.
    - **Edit Mode:** For inserting text.
- **Basic Commands:** See the source for a list of useful Vim commands.

#### 3.3 Compiler Toolchain

- A compiler translates high-level code to machine code in several steps (lexical analysis, preprocessing, parsing, etc.).
- **GCC (GNU Compiler Collection):**
    - `gcc` compiles C code.
    - `g++` compiles C++ code.
- **GCC Options:**
    - `-c`: Compile without linking.
    - `-o <filename>`: Specify output filename.
    - `-g`: Include debugging information.
    - `-Wall`: Show all warnings.
    - `-Werror`: Treat warnings as errors.
    - `-O`: Optimize the code.
    - `-E`: Stop after preprocessing.
    - `-S`: Stop after generating assembly code.
    - `-l<library name>`: Link with a specific library.
    - `-I<path>`: Specify the path for header files.
    - `-L<path>`: Specify the path for library files.

#### 3.4 gdb Debugger

- **Usage:**
    - Compile with `-g` to include debugging info.
    - Run `gdb [program]` to start the debugger.
- **Commands:**
    - `break <line number>` or `b <line number>`: Set a breakpoint.
    - `info b`: List breakpoints.
    - `delete <breakpoint number>`: Delete a breakpoint.
    - `run` or `r`: Run the program.
    - `step` or `s`: Step into a function call.
    - `next` or `n`: Step over a function call.
    - `continue` or `c`: Continue to the next breakpoint.
    - `bt`: View the stack backtrace.
    - `print <variable>` or `p <variable>`: Print the value of a variable.
    - `quit` or `q`: Quit the debugger.

#### 3.5 make and Makefiles

- `make` is used to manage project builds by following rules in a Makefile.
- **Makefiles:**
    - Define dependencies between files.
    - Specify rules for building targets (usually object files or executables).
    - Use macros to simplify rules.
- **Makefile Format:**
    
    ```
    target: dependencies
        command1
        command2
        ...
    ```
    
- **Macros:**
    - Similar to #define in C, used to store reusable values.
    - Defined as `MACRO_NAME = value`
    - Referenced as `${MACRO_NAME}` or `$(MACRO_NAME)`
- **Inference Rules:**
    - Generalize the build process using patterns.
    - `%`: Represents a wildcard.
- **Special Macros:**
    - `$*`: Basename of the current target.
    - `$<`: Name of the first dependency file.
    - `$^`: Names of all dependencies.
    - `$@`: Name of the current target.
    - `$?`: Names of dependencies newer than the target.

#### 3.6 Other Tools

- **screen:**
    - A terminal multiplexer for managing multiple terminal sessions.
    - Useful for keeping processes running even if disconnected.
    - Provides commands for creating, detaching, reattaching, and managing windows within a screen session.
- **diff and patch:**
    - `diff` compares files and produces a patch file.
    - `patch` applies a patch file to a source file.
- **git:**
    - A distributed version control system.
    - Allows multiple developers to work on the same codebase.
    - Provides commands for cloning repositories, committing changes, branching, pushing and pulling changes, and more.

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