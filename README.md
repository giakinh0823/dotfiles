# dotfiles

Cấu hình cá nhân: **zsh (oh-my-zsh + powerlevel10k)**, **tmux (oh-my-tmux)**, **ghostty**, **vim**.

## Cấu trúc

```
dotfiles/
├── zsh/
│   ├── .zshrc               # cấu hình zsh chính
│   ├── .p10k.zsh            # theme powerlevel10k
│   └── custom-example.zsh   # ví dụ custom của oh-my-zsh
├── tmux/
│   ├── tmux.conf.local      # config local cho oh-my-tmux
│   └── cheatsheet.txt       # phím tắt tmux
├── ghostty/
│   └── config               # cấu hình terminal Ghostty
├── vim/
│   ├── vscode.vim           # keybindings vim (VSCode Vim)
│   ├── ideavimrc            # cấu hình IdeaVim (IntelliJ / JetBrains IDEs)
│   └── vimrc                # cấu hình terminal Vim (macOS)
└── git/
    └── .gitconfig
```

## Cài đặt trên máy mới

### 1. Phần mềm phụ thuộc (cài trước)

```sh
# oh-my-zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# powerlevel10k + plugins
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zdharma-continuum/fast-syntax-highlighting \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting
git clone https://github.com/marlonrichert/zsh-autocomplete \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autocomplete

# oh-my-tmux
git clone https://github.com/gpakosz/.tmux.git ~/.local/share/tmux/oh-my-tmux
```

### 2. Tạo symlink (từ thư mục repo)

```sh
cd ~/dotfiles
ln -sf "$PWD/zsh/.zshrc"            ~/.zshrc
ln -sf "$PWD/zsh/.p10k.zsh"         ~/.p10k.zsh
ln -sf "$PWD/git/.gitconfig"        ~/.gitconfig
ln -sf "$PWD/vim/vscode.vim"        ~/vscode.vim
ln -sf "$PWD/vim/ideavimrc"         ~/.ideavimrc   # cần cài plugin IdeaVim trong IDE
mkdir -p ~/.vim/undo
ln -sf "$PWD/vim/vimrc"             ~/.vimrc       # terminal Vim (brew install vim)

mkdir -p ~/.config/tmux
ln -sf ~/.local/share/tmux/oh-my-tmux/.tmux.conf ~/.config/tmux/tmux.conf
ln -sf "$PWD/tmux/tmux.conf.local" ~/.config/tmux/tmux.conf.local
ln -sf "$PWD/tmux/cheatsheet.txt"  ~/.config/tmux/cheatsheet.txt

mkdir -p ~/.config/ghostty
ln -sf "$PWD/ghostty/config"       ~/.config/ghostty/config
```

> **Lưu ý:** `.oh-my-zsh`, `oh-my-tmux`, các plugin và `tmux/plugins/` là code tải về nên **không** lưu trong repo (xem `.gitignore`); cài lại bằng các lệnh ở mục 1.
