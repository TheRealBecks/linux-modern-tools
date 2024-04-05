# Linux Modern Tools

These are the tools and configurations I use for openSUSE Tumbleweed. Check the project GitHub pages to get installation instructions for your OS.

## Overview of all installed Tools
- Nerd Fonts: [GitHub](https://github.com/ryanoasis/nerd-fonts), [Website](https://www.nerdfonts.com/): [FiraCode Nerd Font v3.1.1](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.1.1/FiraCode.zip)
- Bash -> Fish: [GitHub](https://github.com/fish-shell/fish-shell), [Website](https://fishshell.com/)
- Bash prompt -> Starship: [GitHub](https://github.com/starship/starship), [Website](https://starship.rs/)
- `ls` -> `lsd`: LSD (LSDeluxe) - [GitHub](https://github.com/lsd-rs/lsd)
- `dig`, `host` -> `q`: [GitHub](https://github.com/natesales/q)
- `cd` -> `z`: zoxide - [GitHub](https://github.com/ajeetdsouza/zoxide)
- `find` -> `fd`: [GitHub](https://github.com/sharkdp/fd)
- `history` -> `atuin`: [GitHub](https://github.com/atuinsh/atuin)
- `diff` (and `git diff`) -> `delta`: [GitHub](https://github.com/dandavison/delta)
- `top`, `htop` -> `btop`: [GitHub](https://github.com/aristocratos/btop)
- `jq` -> `yq`: [GitHub](https://github.com/mikefarah/yq)
- `cheat`: [GitHub](https://github.com/cheat/cheat)
- `gping`: [GitHub](https://github.com/cheat/cheat)
- `jq` -> `yq`: [GitHub](https://github.com/mikefarah/yq)
- `ps` -> `proc`: [GitHub](https://github.com/dalance/procs)
- `cat` -> `bat`: [GitHub](https://github.com/sharkdp/bat)
- `du` -> `dust`: [GitHub](https://github.com/bootandy/dust)
- `df` -> `dysk`: [GitHub](https://github.com/Canop/dysk)
- `grep` -> `ripgrep`: [GitHub](https://github.com/BurntSushi/ripgrep)
- `cut` -> `choose`: [GitHub](https://github.com/theryangeary/choose)

## Additional Tools
These tools have not been installed as I don't need them.

- `sed` -> `sd`: [GitHub](https://github.com/chmln/sd)
- `cheat` -> `tldr`: [GitHub](https://github.com/tldr-pages/tldr)

# Prerequisites
```
sudo zypper install -y cargo go
```

# Installation
## Nerd Font: FiraCode Nerd Font
Nerd Fonts ([GitHub](https://github.com/ryanoasis/nerd-fonts), [Website](https://www.nerdfonts.com/)) serves many modern fonts with unicode symbols that will be used by the (console) tools.

Install instructions for openSUSE can be found [here](https://en.opensuse.org/Fonts).

### Installation
```
mkdir -p ~/.local/share/fonts
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v3.1.1/FiraCode.zip -O ~/.local/share/fonts/firacode.zip
unzip ~/.local/share/fonts/firacode.zip -d ~/.local/share/fonts/firacode
rm ~/.local/share/fonts/firacode.zip
```

### Configuration
- Enable the font in the KDE menu, search for 'fonts'
- Restart `Konsole` and edit the profile. Change the fonts settings under `Appearance` -> `Color and Font`

## Fish
Fish will replace Bash as command line shell. It has colors, a tree-view, formatting options and a configurations file.

### Installation
```
sudo zypper install -y fish
```

### Configuration
Add the command into `~/.config/fish/config.fish` at the end:
```
fish_add_path ~/go/bin
```

## Starship
Starship ([GitHub](https://github.com/starship/starship), [Website](https://starship.rs/)) is a prompt with a way better overview and has some nice features for `git`.

### Installation
```
sudo zypper install -y starship
```

### Configuration
```
starship preset bracketed-segments -o ~/.config/starship.toml
```

Add into `~/.config/fish/config.fish` in the `if status is-interactive` block:
```
starship init fish | source
```

## LSD - LSDeluxe
`lsd` ([GitHub](https://github.com/lsd-rs/lsd) will replace `ls`. It has colors, a tree-view, formatting options and a configurations file.

### Installation
```
sudo zypper install -y lsd
```

### Configuration
```
mkdir ~/.config/lsd
echo 'date: "+%Y-%m-%d %H:%M:%S"' > ~/.config/lsd/config.yaml
```

Add the commands into `~/.config/fish/config.fish` at the end:
```
alias ll='lsd -al'
alias llt='lsd -a --tree'
```

## q
`q` has way more features than `dig`, but will also replace `host`

### Installation
```
go install github.com/natesales/q@latest
```

### Configuration
Add the commands into `~/.config/fish/config.fish` at the end:
```
alias q='q -R'
```

## z - zoxide
Zoxide ([GitHub](https://github.com/ajeetdsouza/zoxide)) with its `z` command replaced `cd`. It will remember the already used pathes and has also.

### Installation
```
go install github.com/junegunn/fzf@latest
sudo zypper install -y zoxide
```

### Configuration
Add into `~/.config/fish/config.fish` in the `if status is-interactive` block:
```
zoxide init fish | source
```

Add the commands into `~/.config/fish/config.fish` at the end:
```
alias q='q -R'
```

## fd
`fd` ([GitHub](https://github.com/sharkdp/fd)) is a fast and intuitive replacement for `find`.

### Installation
```
go install github.com/junegunn/fzf@latest
sudo zypper install -y fd
```

### Configuration
Add the commands into `~/.config/fish/config.fish` at the end:
```
set FZF_DEFAULT_COMMAND 'fd --type file --color=always'
set FZF_CTRL_T_COMMAND $FZF_DEFAULT_COMMAND
```

## atuin
`atuin` ([GitHub](https://github.com/atuinsh/atuin)) replaces `history` and stores the command with context into an SQLite database.

### Installation
```
sudo zypper install -y atuin
```

### Configuration
```
mkdir ~/.config/atuin
echo 'auto_sync = true' > ~/.config/atuin/config.toml
echo 'enter_accept = false' >> ~/.config/atuin/config.toml
echo 'secrets_filter = true' >> ~/.config/atuin/config.toml
echo 'show_preview = true' >> ~/.config/atuin/config.toml
echo 'style = "compact"' >> ~/.config/atuin/config.toml
echo 'update_check = false' >> ~/.config/atuin/config.toml
atuin import auto
```

Add into `~/.config/fish/config.fish` in the `if status is-interactive` block:
```
atuin init fish | source
```

## delta
Delta ([GitHub](https://github.com/dandavison/delta)) replaces `diff` (and also changes `git diff`).

### Installation
```
sudo zypper install -y git-delta
```

### Configuration
Add into `~/.gitconfig`:
```
[core]
    pager = delta

[interactive]
    diffFilter = delta --color-only

[delta]
    navigate = true    # use n and N to move between diff sections

    # delta detects terminal colors automatically; set one of these to disable auto-detection
    # dark = true
    # light = true

[merge]
    conflictstyle = diff3

[diff]
    colorMoved = default
```

## btop
Delta ([GitHub](https://github.com/aristocratos/btop)) replaces `top` and `htop`.

### Installation
```
sudo zypper install -y btop
```

## yq
`yq` ([GitHub](https://github.com/mikefarah/yq)) replaces `jq`. It supports not only JSON, but also YAML, XML, CSV, TOML and properties.

### Installation
```
go install github.com/mikefarah/yq/v4@latest
```

## cheat
`cheat` ([GitHub](https://github.com/cheat/cheat)) can display cheatsheets for commands.

### Installation
```
sudo zypper install -y cheat
git clone https://github.com/cheat/cheatsheets.git ~/Entwicklung/Sonstige/cheatsheets
mkdir ~/.config/cheat
```

### Configuration
Add the commands into `~/.config/cheat/conf.yml`:
```
---
cheatpaths:
  - name: community                   # a name for the cheatpath
    path: ~/Entwicklung/Sonstige/cheatsheets # the path's location on the filesystem
    tags: [ community ]               # these tags will be applied to all sheets on the path
    readonly: true                    # if true, `cheat` will not create new cheatsheets here
```

Add the commands into `~/.config/fish/config.fish` at the end:
```
set CHEAT_USE_FZF true
```

## gping
`gping` ([GitHub](https://github.com/orf/gping)) is an ICMP `ping` with a statictics graph.

### Installation
```
wget -O ~/Programme/bin/gping-Linux-x86_64.tar.gz https://github.com/orf/gping/releases/latest/download/gping-Linux-x86_64.tar.gz
tar -xzf ~/Programme/bin/gping-Linux-x86_64.tar.gz -C ~/Programme/bin
rm ~/Programme/bin/gping-Linux-x86_64.tar.gz
```

### Configuration
Add the command into `~/.config/fish/config.fish` at the end:
```
fish_add_path ~/Programme/bin
```

## procs
`procs` ([GitHub](https://github.com/dalance/procs)) replaces `ps`.

### Installation
```
sudo zypper install -y procs
```

### Configuration
Not yet finished:
https://github.com/dalance/procs?tab=readme-ov-file#shell-completion
https://github.com/dalance/procs?tab=readme-ov-file#configuration

## bat
`bat` ([GitHub](https://github.com/sharkdp/bat)) replaces `cat`.

### Installation
```
sudo zypper install -y bat
```

## dust
`dust` ([GitHub](https://github.com/bootandy/dust)) replaces `du`.

### Installation
```
sudo zypper install -y dust
```

## dysk
`dysk` ([GitHub](https://github.com/Canop/dysk)) replaces `df`.

### Installation
```
sudo cargo install dysk --root /usr/local/
```

## ripgrep
`ripgrep` ([GitHub](https://github.com/BurntSushi/ripgrep)) replaces `grep`.

### Installation
```
sudo zypper install -y ripgrep
```

## choose
`choose` ([GitHub](https://github.com/theryangeary/choose)) replaces `cut`.

### Installation
```
sudo zypper install -y choose
```
