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
