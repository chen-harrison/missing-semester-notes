# Command-line Environment

### Job Control

- Shell communicates with processes using signals, and when process receives them, they stop execution and deal with signal
    - Signals are called software interrupts for this reason
- Signal examples
    - `ctrl-c` = `SIGINT` signal
    - `ctrl-\` = `SIGQUIT` signal
    - `ctrl-z` = `SIGSTOP` signal
    - `man signal` shows all available
- `kill -SIGNAL %JOB_ID`: sends signal to corresponding job/process
    - `-TERM` sends `SIGTERM`, which works well for ending background processes gracefully
- `&` at the end of a command runs it in the background and hands the terminal back over
- `jobs`: lists unfinished jobs in terminal session, which can be referred to by their PID or `%JOB_ID`, latter of which is shown by `jobs`
- `bg %JOB_ID`: continue suspended job in background
- `fg %JOB_ID`: bring background job, suspended or running, into current terminal and resume
- `nohup COMMAND`: will not end process if sent a `SIGHUP`,  which happens when terminal windows is closed

### Terminal Multiplexers

- Terminal multiplexer: allows you to use multiple terminal windows via tabs/panes, attach/detach, etc. `tmux` is a popular example
- `tmux` is controlled via keyboard commands, which are triggered by a prefix key, which by default is `ctrl-b`, expressed as `C-b` in their notation
- Sessions
    - `tmux`= starts a new session
    - `tmux new -s NAME`= new session with specified name
    - `C-b` + `d` = detach from current session
    - `tmux ls`= view active sessions
    - `tmux attach -t NUM_OR_NAME` = attach to session
    - `tmux rename -t NUM NAME` = rename session of index `NUM` to `NAME`
- Panes
    - `C-b` + `%` = split left-right
    - `C-b` + `“` = split top-bottom
    - `C-b` + `ARROW` = navigate panes
- Windows (aka tabs)
    - `C-b` + `c` = new window
    - `C-b` + `p` = prev window
    - `C-b` + `n` = next window
    - `C-b` + `NUM` = go to window of index `NUM`
- All commands can be viewed inside `tmux` by pressing `C-b` + `?`
- Create file `~/.tmux.conf` to make it more usable/intuitive  
    ```
    # remap prefix from 'C-b' to 'C-a'
    unbind C-b
    set-option -g prefix C-a
    bind-key C-a send-prefix
    
    # split panes using | and -
    bind | split-window -h
    bind - split-window -v
    unbind '"'
    unbind %
    
    # switch panes using Alt-arrow without prefix
    bind -n M-Left select-pane -L
    bind -n M-Right select-pane -R
    bind -n M-Up select-pane -U
    bind -n M-Down select-pane -D
    
    # enable mouse mode (tmux 2.1 and above)
    set -g mouse on
    
    # don't rename windows automatically
    set-option -g allow-rename off
    ```  

### Aliases

- Aliases allow you to assign lengthier commands to shorter strings:  
     `alias ALIAS_NAME="COMMAND_STRING [ARGS] ..."`  
    - If a string is assigned as via `alias`, its raw string can be accessed by prepending with `\` or running `unalias ALIAS_NAME`
    - `alias ALIAS_NAME` reveals definition
- Aliases do not persist across sessions, so place in `~/.bashrc`

### Dotfiles

- Files that start with `.`, hidden by `ls` by default
- Examples
    - `bash`: `~/.bashrc`, `~/.bash_profile`
    - `git`: `~/.gitconfig`
    - `vim`: `~/.vimrc` and the `~/.vim` directory
    - `ssh`: `~/.ssh/config`
    - `tmux`: `~/.tmux.conf`
- For portability, place them all in a single directory with version control, symlinked to the correct places with a script
    - Symlink: `ln -s FILE_OR_DIRECTORY_PATH LINK_PATH`
- If you want different programs to share configurations, put those in their own file, then source the file in each program’s dotfile

### Remote Machines

- Secure Shell (SSH) is used to access remote machines:  
    `ssh USER@IP_ADDRESS_OR_URL [COMMAND]`  
    - add a `COMMAND` at the end to just run it directly
- SSH keys allow you to forego password use each time you log into remote
    - Generated in pairs, public and private, i.e. `id_ed25519` and `id_ed25519.pub` - public is passed to remote, private is kept locally to as a method of authentication
    - Passphrase ensures that if private key file is obtained by someone else, they can’t use it
    - Remote machine
        - Copy to remote with `ssh-copy-id -i .ssh/id_ed25519.pub USER@IP_ADDRESS_OR_URL`
    - GitHub/GitLab
        - `cat ~/.ssh/id_ed25519.pub`, then copy output and paste it into text field on website
- `rsync -avP FILE_OR_DIRECTORY_PATH USER@IP_ADDRESS_OR_URL:DESTINATION` syncs files and directories between two hosts or machines
- List remote devices in `~/.ssh/config` and you can connect by simply typing `ssh HOST_NAME`  
    ```
    Host HOST_NAME
    	User USER
    	Hostname IP_ADDRESS_OR_URL
    	IdentityFile ~/.ssh/id_ed25519
    	LocalFoward 9999 localhost:8888  # see port forwarding below
    ```  
    - [SSH config options](https://www.ssh.com/academy/ssh/config)
- `tmux` works well on SSH connections, because detached sessions will persist even if connection falters, and can be picked back up
- Other shell aternatives for accessing remote machines are [Mosh](https://mosh.org/) and [SSHFS](https://github.com/libfuse/sshfs)

### Port Forwarding

- Computer handles many incoming/outgoing requests by placing them on ports and assigning a port number - software will listen to specific ports on a machine to receive info
- If you want to reach a remote server without directly accessible ports (via network/internet, etc.), you can do local port forwarding, which connects an accessible local port to the remote port via SSH, and so when the local port is accessed, it “redirects” to the remote instead
    - If Jupyter Notebook is run on remote server which listens on  port `8888`,  and we want to access it locally on port `9999`, command is  
        `ssh -L 9999:localhost:8888 USER@IP_ADDRESS_OR_URL`  
- Conversely, if youwant a remote port to provide access to a port locally, you can do remote port forwarding
    - If remote port `8888` needs to reroute to local port `9999`, command is  
        `ssh -R 8888:localhost:9999 USER@IP_ADDRESS_OR_URL`  
- [Helpful Stack Exchange post](https://unix.stackexchange.com/questions/115897/whats-ssh-port-forwarding-and-whats-the-difference-between-ssh-local-and-remot)
