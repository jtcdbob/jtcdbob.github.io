---
title:  "VIMRC-LITE"
excerpt: "light-weight vimrc file for quick configuration on alien machines"
categories:
  - Utility
tags:
  - CODE_DEBUG_LIFE
use_math: false
---

A quick file for vim key remapping.

```
set antialias
set backspace=2    " Backspace for dummies
set linespace=0    " No extra spaces between rows
set scrolloff=999  " Minimum lines to keep above and below cursor
set listchars=tab:›\ ,trail:•,extends:#,nbsp:. " Highlight problematic whitespace
set splitbelow
set splitright
set hidden " When a buffer is brought to foreground, remember undo history and marks.
set history=100 " Increase history from 20 default to 1000
set laststatus=2 " Always show status line
set nocompatible " Make vim more useful
set noerrorbells " Disable error bells.
set nostartofline
set ruler " Show the cursor position
set title " Show the filename in the window titlebar.
set background=dark
set tabstop=2
set mouse=a
set softtabstop=2
set expandtab
set number
set showcmd
set cursorline
set wildmenu
set lazyredraw
set showmatch
set incsearch
set hlsearch
set foldenable
set foldlevelstart=10
set foldnestmax=10
set foldmethod=indent

set clipboard=unnamed

syntax enable

scriptencoding utf10
" Disable the scrollbars
set guioptions-=r
set guioptions-=L
set encoding=utf-8
" set nobackup
" set noswapfile
" set pastetoggle=<F2>

" Map Leader
let mapleader = "\<Space>"
nnoremap <Leader>w :w<CR>
nnoremap <Leader><space> za
nmap <leader>cd :cd %:h<CR>
nmap <leader>lcd :lcd %:h<CR>
nmap <silent> <leader>vimrc :e ~/.vimrc<CR>
map <leader>y "*y
map <leader>p "*p
vmap <Leader>y "+y
vmap <Leader>d "+d
nmap <Leader>p "+p
nmap <Leader>P "+P
vmap <Leader>p "+p
vmap <Leader>P "+P
vnoremap <silent> y y`]
vnoremap <silent> p p`]
nnoremap <silent> p p`]
" nnoremap <leader>u :GundoToggle<CR>
" nnoremap <leader>s :mksession<CR>

" Better search and replace using /keyword + cs + .n
vnoremap <silent> s //e<C-r>=&selection=='exclusive'?'+1':''<CR><CR>\:<C-u>call histdel('search',-1)<Bar>let @/=histget('search',-1)<CR>gv
omap s :normal vs<CR>

" Key remapping
nnoremap <CR> G
nnoremap <BS> gg
nnoremap ; :
nnoremap j gj
nnoremap k gk
nnoremap B ^
nnoremap E $
nnoremap J 10j
nnoremap K 10k
nnoremap $ <nop>
nnoremap ^ <nop>
nnoremap gV `[V`]
inoremap jk <esc>

```

For `.tmux.conf` file:

```
# Change Keybind to C-a
unbind C-b
set -g prefix C-a
bind C-a send-prefix

# Use vim keybindings in copy mode
setw -g mode-keys vi

# Large history
set-option -g history-limit 10000

# Basic settings
set-window-option -g xterm-keys on # for vim
set-window-option -g mode-keys vi # vi key
set-window-option -g monitor-activity on
set-window-option -g window-status-current-fg white

# Status Bar
set-option -g status-utf8 on
set-option -g status-justify right
set-option -g status-bg black # colour213 # pink
set-option -g status-fg cyan
set-option -g status-interval 5
set-option -g status-left-length 30
set-option -g status-left '#[fg=magenta]» #[fg=blue,bold]#T#[default]'
set-option -g status-right '#[fg=red,bold][[ #(git branch) branch ]] #[fg=cyan]»» #[fg=blue,bold]###S #[fg=magenta]%R %m-%d#(acpi | cut -d ',' -f 2)#[default]'
set-option -g visual-activity on

# Titles (window number, program name, active (or not)
set-option -g set-titles on
set-option -g set-titles-string '#H:#S.#I.#P #W #T'

#################### Bindings #####################
# reload tmux conf
bind-key r source-file ~/.tmux.conf
# new split in current pane (horizontal / vertical)
unbind '"' # unbind horizontal split
unbind %   # unbind vertical split
bind-key v split-window -v # split pane horizontally
bind-key b split-window -h # split pane vertically
# list panes
bind-key Space list-panes
# break-pane
bind-key Enter break-pane
# Navigation ---------------------------------------------------------------
# # use the vim motion keys to move between panes
bind-key h select-pane -L
bind-key j select-pane -D
bind-key k select-pane -U
bind-key l select-pane -R
# Resizing ---------------------------------------------------------------
bind-key C-h resize-pane -L
bind-key C-j resize-pane -D
bind-key C-k resize-pane -U
bind-key C-l resize-pane -R

# Navigation for windows
bind-key -n C-k prev
bind-key -n C-h prev

bind-key -n C-l next
bind-key -n C-j next

# use vim motion keys while in copy mode
setw -g mode-keys vi

# Copy-paste integration
 set-option -g default-command "reattach-to-user-namespace -l zsh"

# # Use vim keybindings in copy mode
 setw -g mode-keys vi

# # Setup 'v' to begin selection as in Vim
 bind-key -t vi-copy v begin-selection
 bind-key -t vi-copy y copy-pipe "reattach-to-user-namespace pbcopy"

# # Update default binding of `Enter` to also use copy-pipe
 unbind -t vi-copy Enter
 bind-key -t vi-copy Enter copy-pipe "reattach-to-user-namespace pbcopy"

# # Bind ']' to use pbpaste
 bind ] run "reattach-to-user-namespace pbpaste | tmux load-buffer - && tmux paste-buffer"

```

A light-weight `.zshrc`, commented out some sections for more general `.bashrc` use.

```
# You may need to manually set your language environment
# export LANG=en_US.UTF-8

alias clc='clear'
alias ls='ls -sFC'
alias ll='ls -a'
alias l='ls'
alias vi='vim'
alias grep="grep --color=auto"
alias gitst='git status'
alias -s py=vi
alias -s c=vi
alias -s txt=vi
alias -s gz='tar -xzvf'
alias -s tgz='tar -xzvf'
alias -s zip='unzip'
alias -s bz2='tar -xjvf'
export TERM=xterm-256color
export CLICOLOR=1
zstyle ':completion:*:default' list-colors ''


# To reload the .zshrc command
# alias reload=". ~/.zshrc && echo 'ZSH config reloaded from ~/.zshrc'"

```
