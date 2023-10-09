### Modal Editing

- Vim is a modal editor - it has different modes
    - Normal: moving around a file, editing
    - Insert: inserting
    - Replace: replacing
    - Visual: selecting blocks of text
    - Command-line: running a command like save, quit, etc.

### Basics

- Run `vimtutor` in terminal to learn/practice! (80x24 terminal recommended)
- `vim FILE` opens up the file
- Vim maintains a set of open buffers (aka files), and on top of that you can have tabs and windows
- Switching modes
    - Pressing `esc` returns to normal mode (consider rebinding `caps lock` to `esc`)
    - From normal, `i` = insert mode, `R` = replace, `v` = visual, `V` = visual line, `^V` = visual block, `:` = command-line
- Command-line mode:
    - `:q` = quit (close window), `:qa` to quit all open windows/tabs
    - `:w` = save (“write”)
    - `:wq` = save and quit
    - `:e FILE` = open file to edit
    - `:help TOPIC` = get documentation on command (if you want help on a command-line command, type with colon, i.e. `:q`)

### Interface

- Movement, aka “nouns”
    - `hjkl` = “arrow keys”
    - `w` = next “word”, `b` = “beginning” of word, `e` = “end” of word
    - `0` = beginning of line, `^` = first non-blank char, `$` = end of line
    - `H` = “highest” line on screen, `M` = “middle” line, `L` = “lowest” line
    - `ctrl-u`, `ctrl-d` = scroll “up”/“down”
    - `gg` = beginning of file, `G` = end of file
    - `f`/`F` + `CHAR` = (”find”) jump forward/backward to next `CHAR`
    - `t`/`T` + `CHAR` = (”to”) jump forward/backward right before next `CHAR`
- Editing, aka “verbs”, which act on nouns
    - `o`/`O` = insert line above/below cursor + enter insert mode
    - `d` + `NOUN` = delete
        - e.g. `dw` = delete word, `d$` = delete from cursor to end of line, etc.
    - `c` + `NOUN` = delete + enter insert mode
    - `x` = delete character (same as `dl`)
    - `r` + `CHAR` = replace cursor character with `CHAR`
    - `u` = undo, `ctrl-r` = redo
    - `y` = copy (”yank”), i.e. `yw` to copy word, `p` = paste
- Visual
    - `v` = select/highlight, navigate around to expand
    - `V` = highlights whole line
    - `ctrl-v` = highlights “ blocks”

### Tools

- Customization
    - Change Vim’s behavior/configuration via `~/.vimrc`,
        - [Example config file](https://missing.csail.mit.edu/2020/files/vimrc) provided by course instructors
    - Extensions also available
        - [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim): fuzzy file finder
        - [ack.vim](https://github.com/mileszs/ack.vim): code search
        - [nerdtree](https://github.com/scrooloose/nerdtree): file explorer
        - [vim-easymotion](https://github.com/easymotion/vim-easymotion): magic motions
- A good rule: whenever you think “there must be a better way of doing this”, there probably is, and you can find it online