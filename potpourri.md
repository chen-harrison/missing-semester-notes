### Keyboard

- Keyboard modification can improve coding efficiency
    - Remapping keys, e.g. `caps lock` to `ctrl` or `esc`
    - Mapped commands to new terminal, sleeping computer, etc.
- Keyboard software
    - Linux: [xmodmap](https://wiki.archlinux.org/index.php/Xmodmap) or [Autokey](https://github.com/autokey/autokey)
    - Windows: built-in in Control Panel, [AutoHotkey](https://www.autohotkey.com/) or [SharpKeys](https://www.randyrants.com/category/sharpkeys/)
    - [QMK](https://docs.qmk.fm/)

### Daemons

- Daemons: processes always running in the background, names often end with “d”
    - e.g. `sshd` is the SSH daemon, listens to incoming requests
- `systemd`: system daemon, can be used to run/set up daemon processes
    - `systemctl status` = list currently running daemons
    - `systemctl` also has `enable`, `disable`, `start`, `stop`, `restart`
    - Accessible interface to enable or configure new daemons
- `cron`: daemon that can perform scheduled tasks

### FUSE

- FUSE: filesystem in user space, allows user level code to be execute arbitrary actions during filesystem operations
    - [sshfs](https://github.com/libfuse/sshfs): open locally remote files/directory through an SSH connection
    - [rclone](https://rclone.org/commands/rclone_mount/): mount cloud storage services like Dropbox and Google Drive, and open data locally
    - [gocryptfs](https://nuetzlich.net/gocryptfs/): encrypted overlay system.\ - files are stored encrypted but once the FS is mounted they appear as plaintext in the mountpoint
    - [kbfs](https://keybase.io/docs/kbfs): mistributed filesystem with end-to-end encryption. You can have private, shared and public directories
    - [borgbackup](https://borgbackup.readthedocs.io/en/stable/usage/mount.html): mount your deduplicated, compressed and encrypted backups for ease of browsing

### Backups

- Every file you care about should have a backup, can disappear at any moment
    - Hardware failure (don’t store backup on same drive)
    - External drive can be lost due to property damage
    - Synchronization/mirroring, e.g. Dropbox will not protect against file corruption or deletion, since changes will be reflected on service
- Features of a good backup
    - Versioning: able to access history of changes, allowing for recovery
    - Deduplication: only store incremental changes to reduce storage use
    - Security: what info would someone need to have in order to read data or modify/delete it?
- Verify regularly that backups can be used to recover data, don’t blindly trust
- Backups should also be used for cloud data, info attached to online accounts
    - Maintain offline copies of this info

### APIs

- Services you interact with on day-to-day usually have APIs that allow you to programatically access their data
- API format is usually a structured URL, like `api.service.com`
    - Can be queried via GET request with `curl`
    - Responses usually come in JSON form and can be piped through `jq` to get what you want
- Some use authentication methods, usually “OAuth”, to distribute tokens that can only be used for specific purposes
- [IFTTT](https://ifttt.com/) allows chaining services together

### Common Command-line Flags/Patterns

- `--help` = usage info/documentation
- `--version`, `-V` = display program version info
- `--verbose`, `-v` = more output, i.e. debug; more `v`’s mean more output (`-vvv`)
- `--quiet`, `--silent` = opposite of `--verbose`
- `-r` = opt into recursive behavior
- `-` = provided instead of file name, meaning `stdin` or `stdout` instead of file
- `--` = tells command that everything after should not be read as a flag, so flag-like inputs will be read as inputs
- “Dry run” flag = representation will vary; runs tool without making changes, saying what it would have done
- “Interactive” mode = sometimes `-i`; will give confirmation prompt before it does an action that can’t be undone

### Window Managers

- “Tiling” window managers make sure windows never overlap, and are instead arranged as tiles on the screen (like `tmux`)
    - Windows can be toggled through with keyboard shortcuts, allowing for minimal/no use of mouse

### VPNs

- VPN best-case: change internet service provider, make traffic seem like it’s coming from somewhere else
- Overall not that secure; instead of trusting internet service provider, trusting the provider of VPN

### Desktop Automation

- [Hammerspoon](https://www.hammerspoon.org/) is a desktop automation framework for macOS allowing you to hook Lua scripts into OS functionality
    - e.g. bind hotkeys to window movement, create a menu bar button, etc.
- Linux will have equivalents for most things

### GitHub

- Contributions to GitHub repos come in the form of issues or pull requests
    - Issues: usually reporting bugs or requesting a new feature, no reading or writing code
    - Pull request: usually done by forking a repo that you don’t have write permissions to, implementing desired changes, then creating a pull request to hopefully merge changes into upstream repo