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
Passwordless emlop (Optional but Recommended)
To avoid being prompted for a password twice (once for the update and once for the monitor), add a sudoers rule:

Run sudo visudo -f /etc/sudoers.d/emlop-nopasswd.

Add: your_username ALL=(ALL) NOPASSWD: /usr/bin/emlop.

Installation
Open your ~/.bashrc and paste the following function:

```bash
upd() {
    # Start a tmux session for the update, world update, and depclean
    
    tmux new-session -d -s "gentoo-update" "sudo emaint sync -a && sudo emerge -auDU --quiet-build=y @world && sudo emerge -a --depclean"
    
    # Split for the emlop TUI prediction (Remaining, Total, Average)
    tmux split-window -v -p 30 -t "gentoo-update" "watch -n 5 'sudo emlop predict --show rta'"
    
    # Focus the top pane for password/confirmation
    tmux select-pane -t 0
    
    # Attach to the session
    tmux attach-session -t "gentoo-update"
}
```
Save the file and reload your shell:

Bash
source ~/.bashrc

Usage
Simply type upd in your terminal.

Confirmation: Review the package list and press y to start the compilation.

ETA: Watch the bottom pane for live estimates based on your hardware history.
