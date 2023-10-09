### Git’s Data Model

- Commits act as “snapshots” of a collection of folders and files
- Example  
    ```
    <root> (tree)
    |
    +- foo (tree)
    |  |
    |  + bar.txt (blob, contents = "hello world")
    |
    +- baz.txt (blob, contents = "git is wonderful")
    ```  
    - Git calls what we call folders trees and files as blobs
- Git history modeling, in the form of pseudocode  
    ```
    // a file is a bunch of bytes
    type blob = array<byte>
    
    // a directory contains named files and directories
    type tree = map<string, tree | blob>
    
    // a commit has parents, metadata, and the top-level tree
    type commit = struct {
        parents: array<commit>
        author: string
        message: string
        snapshot: tree
    }
    ```  
- Object is a blob, tree, or commit, all of which are stored and “addressed” using SHA-1 hash, aka a 40 character hexadecimal
    - `git cat-file -p SHA-1_HASH` will show contents of that object
- References are mutable (changeable) pointers to specific commits
    - `master`: most recent commit in main development branch
    - `HEAD`: where we currently are, so a new commit is generated with correct `parents` struct member
- Remotes have their own references too, and are maintained separately
    - To correspond local branches to remote branches: `git branch --set-upstream-to=REMOTE/REMOTE_BRANCH`

### Configuration

- Configure git behavior with `git config` command or by editing `~/.gitconfig` file
- `.gitignore` tells Git which files to disregard when committing changes