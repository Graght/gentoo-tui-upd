# gentoo-tui-upd
upd is a simple .bashrc script using tmux to create a pleasant tui for gentoo users when updating the system. Simply type upd to use it instead of the long emerge command.
# Gentoo TUI Update Wrapper

A simple Bash function to automate Gentoo system updates with a clean TUI dashboard using `tmux` and `emlop`.

## Features
* **One-command update:** Syncs repositories and starts a world update.
* **TUI Monitoring:** Automatically opens `emlop` in a split pane to show ETAs and progress.
* **Quiet Builds:** Suppresses compiler noise so you can focus on the progress bar.

## Prerequisites
Ensure you have the necessary tools installed:
```bash
sudo emerge -a app-misc/tmux app-portage/emlop
```
**Installation**
Open your ~/.bashrc (using nvim, hx, or nano).

Copy and paste the following function at the end of the file:

Bash
upd() {
    # Start a tmux session for the update and monitor
    tmux new-session -d -s "gentoo-update" "sudo emaint sync -a && sudo emerge -auDU --quiet-build=y @world"
    
    # Split for the emlop TUI monitor
    tmux split-window -v -p 30 -t "gentoo-update" "emlop -m"
    
    # Focus the top pane for password/confirmation
    tmux select-pane -t 0
    
    # Attach to the session
    tmux attach-session -t "gentoo-update"
}
Save the file and reload your shell:

Bash
source ~/.bashrc
**Usage**
Simply type upd in your terminal.

Enter your password when prompted.

Review the package list and press y to start the compilation.

Watch the emlop TUI at the bottom for real-time ETAs!
