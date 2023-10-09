# Debugging and Profiling

### Logging

- Use logging instead of print statements
    - Allows output to go to files, sockets, remote servers, etc. instead of  just `stdout`
    - Supports different severity levels (INFO, DEBUG, WARN, ERROR), allowing for filtering
    - Color code them for improved readability
- `systemmd` in Linux systems places logs in `/var/log/journal`, accessed via `journalctl` command

### Debuggers

- Debugger benefits
    - Halt execution of program at a certain line or when conditions are met
    - Step through program incrementally
    - Inspect variable values after crashing
- Debuggers
    - C++: `gdb`
        - https://sourceware.org/gdb/download/onlinedocs/refcard.pdf
    - Python: `pdb` or `ipdb` (similar but with tab completion, syntax highlighting, etc.)
        - https://docs.python.org/3/library/pdb.html
- System calls are used by programs to perform actions via the kernel; `strace` allows you to track when they occur
- Firefox/Chrome are good debugging tools for web dev - inspect site elements, live modification, etc.

### Static Analysis

- Static analysis programs take source code as input and analyze it with coding rules, allowing you to find issues without running code - especially helps for time-intensive programs
    - Options for many languages here: https://github.com/analysis-tools-dev/static-analysis

### Profiling

- Types of time
    - Real: time from start to finish of program, including time taken by other processes
    - User: time spent in CPU running user-level code
    - Sys: time spent in CPU running kernel-level code
- Profiler types
    - Tracing: execute with code, take note of every function call. At the end, able to tell time spent in different functions
        - Problem: lots of overhead, affect performance of original program
    - Sampling:  on a fixed time interval, stops program, looks at stack trace to see where in program you are, and enough samples will be able to tell where time is spent
- Profiler examples
    - `cProfile`: Python tracing profiler that measures time per function call
        - `python -m cProfile -s tottime PYTHON_SCRIPT.PY 1000 '^(import|\s*def)[^,]*$' *.py`
        - Can be hard to parse through, since you might want to measure a function that calls other third-party library functions
    - `line_profiler`: Python profiler that uses `@profile` decorator above functions to identify which one to measure
        - `kernprof -lv SCRIPT.PY`
- Memory profiling: can help identify memory leaks and inefficiencies
    - C++: `valgrind`
    - Python: `memory_profiler`
- Event profiling: ignores specifics, treats program as a black box
    - `perf`: hardware-agnostic evaluation, reporting system events that occurred from a certain command
        - `perf stat COMMAND ARG_1 ARG_2`: gets counts of different events related to a command
- Profiling visualization tools
    - Flame graph: `perf COMMAND report flamegraph`
    - Call graphs: `pycallgraph graphviz -- ./PYTHON_SCRIPT.py`
- Resource monitoring: determine what resource is the main bottleneck/constraint
    - `htop`: general
    - `iotop`: I/O usage
    - `du`, `ncdu`: disk usage
    - `free`: memory
    - `lsof`: open files
    - `ss`, `ip`: network connections
    - `nethogs`, `iftop`: network usage
- `hyperfine`: black box speed comparison between command line programs
    - `hyperfine --warmup 3 'COMMAND_1' 'COMMAND_2'`
- [eBPF](http://www.brendangregg.com/blog/2019-01-01/learn-ebpf-tracing.html): perform kernel tracing of user programs