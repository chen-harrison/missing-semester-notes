# The Shell

### Stream Manipulation

- Standard I/O
    - `stdin`: standard input
    - `stdout`: standard output
    - `stderr`: standard error
- `COMMAND > FILE`: takes the `stdout` and writes it to the file
    - `2>` writes `stderr` to file
    - `>>` appends instead of overwriting file contents
- `COMMAND < FILE`: takes the contents of the file and sends it as input to the command
- `COMMAND_1 | COMMAND_2`: the pipe character, which takes the `stdout` of the left command and moves it to `stdin` for the right command
    - `stdin` *input is NOT the same as sending arguments to command!* Some commands will have functionality to take file arguments and read its contents, or to take in contents of `stdin`
- `tee FILE`: takes input and write it to file and `stdout`

### Useful Commands

- `cd -`: changes directory to the one you were at previously, i.e. a back button
- `pushd`, `popd`: generate/prune a directory stack as you move between directories
- `which COMMAND`: shows the absolute path to the command being called
- `man PROGRAM`: the manual command, a more readable `-h` or `--help`
- `sudo`: “do as su (super user)”
    - `sudo su`: creates a super user terminal instance, which you’ll notice looks like `root@DEVICE:PATH#` instead of `USER@DEVICE:PATH$`
- `xdg-open FILE`: open file in appropriate application

### Linux Filesystem

- Uses for different directories in `/`:
    - `/bin` = essential command binaries
    - `/sbin` = essential system binaries, usually to be run by root
    - `/dev` = device files, special files that often are interfaces to hardware devices
    - `/etc` = host-specific system-wide configuration files
    - `/home` = home directories for users in the system
    - `/lib` = common libraries for system programs
    - `/opt` = optional application software
    - `/sys` = contains information and configuration for the system
    - `/tmp` = temporary files (also `/var/tmp`). Usually deleted between reboots.
    - `/usr/` = read only user data
        - `/usr/bin` = non-essential command binaries
        - `/usr/sbin` = non-essential system binaries, usually to be run by root
        - `/usr/local/bin` = binaries for user compiled programs
    - `/var` = variable files like logs or caches