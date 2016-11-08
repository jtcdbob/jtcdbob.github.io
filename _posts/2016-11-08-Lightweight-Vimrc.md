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
