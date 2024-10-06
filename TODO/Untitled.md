
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
