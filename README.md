# dotfiles

Personal Linux dotfiles managed with a simple symlink script — no external tools required.

## Structure

Each tool has its own directory. Files inside mirror the path they should have under `$HOME`:

```
zsh/.zshrc                           -> ~/.zshrc
tmux/.tmux.conf                      -> ~/.tmux.conf
nvim/.config/nvim/init.lua           -> ~/.config/nvim/init.lua
lazygit/.config/lazygit/             -> ~/.config/lazygit/
librewolf/.librewolf/                -> ~/.librewolf/
claude/.claude/                      -> ~/.claude/
```

Only files whose path starts with `.` are linked, so `README.md` files inside tool directories are ignored.

## Installation

Clone the repo and run the install script:

```bash
git clone git@github.com:<your-username>/.dotfiles.git ~/.dotfiles
cd ~/.dotfiles
bash install.sh
```

The script will:
1. Symlink each dotfile into `$HOME` at the correct path
2. Back up any existing file that would be overwritten to `~/.dotfiles_backup/<timestamp>/`

## Adding a new dotfile

Say you want to track Neovim's config, which lives at `~/.config/nvim/init.lua` on your machine.

1. In the **repo**, create a matching directory for the tool:
   ```bash
   mkdir -p nvim/.config/nvim
   ```
2. Copy the file **from your machine** into the repo, keeping the same path relative to `$HOME`:
   ```bash
   cp ~/.config/nvim/init.lua nvim/.config/nvim/init.lua
   ```
3. Run the install script to replace the original file with a symlink back to the repo:
   ```bash
   bash install.sh
   ```

After this, `~/.config/nvim/init.lua` on your machine is a symlink to `nvim/.config/nvim/init.lua` in the repo. Edit either one and the change is reflected in both.

## Tools configured

| Tool | Config |
|------|--------|
| zsh | `.zshrc` with Oh My Zsh + Powerlevel10k |
| tmux | `.tmux.conf` |
| Neovim | `.config/nvim/init.lua` |
| lazygit | `.config/lazygit/` |
| Librewolf | `.librewolf/librewolf.overrides.cfg` |
| Claude Code | `.claude/` (agents, skills, commands, settings) |
