# MY SETUP VIM

Teks editor VIM sangat keren dan sangat membantu untuk meningkatkan produktivitas kita.

Disini saya ingin membagikan beberapa plugin tambahan yang saya gunakan sehari hari,
mungkin beberapa plugin ini sangat membantu untuk kita apabila ingin belajar menjadi Frontend Web Developer, Backend Web Developer maupun Fullstack Web Developer.

> [!NOTE]
> Saya menggunakan Terminal emulator (Termux), Sesuaikan beberapa perintah yang mungkin tidak berfungsi dengan terminal anda.

[Tutorial youtube](https://www.youtube.com)

[![Vim](https://img.shields.io/badge/--019733?logo=vim)](https://www.vim.org/) [![Visual Studio Code](https://img.shields.io/badge/--007ACC?logo=visual%20studio%20code&logoColor=ffffff)](https://code.visualstudio.com/)

---

&nbsp;

## Memulai

### Packages

#### Update Packages

```sh
pkg update -y && pkg upgrade
```

#### Install NodeJS & Yarn

```sh
pkg install nodejs yarn -y
```

#### Install GIT

```sh
pkg install git -y
```

#### Install VIM

```sh
pkg install vim -y
```

### Plugins

#### Install [Vim Plug](https://github.com/junegunn/vim-plug#installation)

```sh
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

Setelah proses instalasi vim plug selesai, Buat file baru `~/.vimrc` Dan tambahkan kode dibawah ini:

```vim
set encoding=UTF-8 nobackup nowritebackup nocompatible background=dark termguicolors autoindent expandtab tabstop=2 shiftwidth=2
syntax on

call plug#begin()
Plug 'lissaferreira/dalton-vim'
Plug 'vim-airline/vim-airline'
Plug 'preservim/nerdtree'
Plug 'ryanoasis/vim-devicons'
Plug 'kassio/neoterm'
Plug 'alvan/vim-closetag'
Plug 'jiangmiao/auto-pairs'
Plug 'sheerun/vim-polyglot'
Plug 'othree/html5.vim'
Plug 'pangloss/vim-javascript'
Plug 'gutenye/json5.vim'
Plug 'elzr/vim-json'
Plug 'HerringtonDarkholme/yats.vim'
Plug 'maxmellon/vim-jsx-pretty'
Plug 'godlygeek/tabular'
Plug 'preservim/vim-markdown'
Plug 'lifepillar/pgsql.vim'
Plug 'StanAngeloff/php.vim'
Plug 'vim-python/python-syntax'
Plug 'neoclide/coc.nvim', {'branch': 'release'}
call plug#end()

colorscheme dalton
let g:airline_theme='dalton'
let NERDTreeShowHidden=1
nnoremap <leader>n :NERDTreeFocus<CR>
nnoremap <C-n> :NERDTree<CR>
nnoremap <C-t> :NERDTreeToggle<CR>
nnoremap <C-f> :NERDTreeFind<CR>
" Start NERDTree when Vim is started without file arguments.
autocmd StdinReadPre * let s:std_in=1
autocmd VimEnter * if argc() == 0 && !exists('s:std_in') | NERDTree | endif


" filenames like *.xml, *.html, *.xhtml, ...
" These are the file extensions where this plugin is enabled.
"
let g:closetag_filenames = '*.html,*.xhtml,*.phtml,*.js,*.ts,*.jsx,*.tsx'
" filenames like *.xml, *.xhtml, ...
" This will make the list of non-closing tags self-closing in the specified files.
"
let g:closetag_xhtml_filenames = '*.xhtml,*.jsx,*.tsx'
" filetypes like xml, html, xhtml, ...
" These are the file types where this plugin is enabled.
"
let g:closetag_filetypes = 'html,xhtml,phtml'
" filetypes like xml, xhtml, ...
" This will make the list of non-closing tags self-closing in the specified files.
"
let g:closetag_xhtml_filetypes = 'xhtml,jsx,tsx'
" integer value [0|1]
" This will make the list of non-closing tags case-sensitive (e.g. `<Link>` will be closed while `<link>` won't.)
"
let g:closetag_emptyTags_caseSensitive = 1
" dict
" Disables auto-close if not in a "valid" region (based on filetype)
"
let g:closetag_regions = {
\ 'typescript.tsx': 'jsxRegion,tsxRegion',
\ 'javascript.jsx': 'jsxRegion',
\ 'typescriptreact': 'jsxRegion,tsxRegion',
\ 'javascriptreact': 'jsxRegion',
\ }
" Shortcut for closing tags, default is '>'
"
let g:closetag_shortcut = '>'
" Add > at current position without closing the current tag, default is ''
"
let g:closetag_close_shortcut = '<leader>>'

let g:vim_jsx_pretty_colorful_config = 1 " default 0
let g:python_highlight_all = 1 " Dissable 0

inoremap <silent><expr> <CR> coc#pum#visible() ? coc#pum#confirm()
\: "\<C-g>u\<CR>\<c-r>=coc#on_enter()\<CR>"
function! CheckBackspace() abort
let col = col('.') - 1
return !col || getline('.')[col - 1]  =~# '\s'
endfunction

" Use <c-space> to trigger completion
if has('nvim')
inoremap <silent><expr> <c-space> coc#refresh()
else
inoremap <silent><expr> <c-@> coc#refresh()
endif

" Use `[g` and `]g` to navigate diagnostics
" Use `:CocDiagnostics` to get all diagnostics of current buffer in location list
nmap <silent> [g <Plug>(coc-diagnostic-prev)
nmap <silent> ]g <Plug>(coc-diagnostic-next)

" GoTo code navigation
nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gi <Plug>(coc-implementation)
nmap <silent> gr <Plug>(coc-references)

" Use K to show documentation in preview window
nnoremap <silent> K :call ShowDocumentation()<CR>

function! ShowDocumentation()
if CocAction('hasProvider', 'hover')
call CocActionAsync('doHover')
else
call feedkeys('K', 'in')
endif
endfunction

" Highlight the symbol and its references when holding the cursor
autocmd CursorHold * silent call CocActionAsync('highlight')
```

Buka teks editor vim, dengan cara menggunakan perintah `vi` pada terminal.
Lalu jalankan perintah `:PlugInstall` pada teks editor vim.

#### Install extensions Coc

Setelah kita menginstall beberapa plugin vim, Kita perlu menginstall beberapa [extensions (like VSCode)](https://github.com/neoclide/coc.nvim/wiki/Using-coc-extensions) yang disediakan oleh plugin [Coc.nvim](https://github.com/neoclide/coc.nvim).

Buka teks editor vim, lalu jalankan perintah sebagai berikut:

```vim
:CocInstall coc-json coc-highlight coc-html coc-emmet coc-htmlhint coc-css coc-cssmodules @yaegassy/coc-tailwindcss3 coc-tsserver coc-tslint-plugin coc-prettier coc-html-css-support coc-phpls coc-blade @yaegassy/coc-laravel coc-eslint
```

Setelah proses instalasi selesai, Kita perlu merubah/menambahkan file konfigurasi. Buka teks editor vim, lalu jalankan perintah sebagai berikut:

```vim
:CocConfig
```

Lalu tambahkan kode dibawah ini:

```json
{
  "colors.enable": true,
  "emmet.includeLanguages": {
    "vue-html": "html",
    "javascript": "javascriptreact",
    "typescript": "typescriptreact"
  },
  "emmet.excludeLanguages": ["markdown"],
  "html-css-support.enabledLanguages": [
    "html",
    "vue",
    "blade",
    "htmldjango",
    "typescriptreact",
    "javascriptreact"
  ],
  "html-css-support.styleSheets": [
    "https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css",
    "/style.css",
    "style.css",
    "./*.css",
    "./**/*.css"
  ],
  "cssmodules.camelCase": true,
  "cssmodules.hintName": "cssmodules",
  "coc.preferences.formatOnSave": true,
  "coc.preferences.formatOnType": true
}
```

### Font

Kita perlu merubah font default Termux, Agar tampilan Nerdtree lebih keren dan plugin vim-devicons berfungsi dengan baik.

[Referensi font](https://github.com/ryanoasis/nerd-fonts?tab=readme-ov-file#patched-fonts)

[Download font](https://terabox.com/s/1j4jYjg4DwE7XeeuGA1SzCw)

Setelah font berhasil didownload, Sekarang kita perlu merubah font default termux dengan cara memindahkan font yang berhasil kita download ke directory termux. Jalankan perintah sebagai berikut:

**Izinkan termux untuk mengakses penyimpanan internal(Internal storage):**

```sh
termux-setup-storage
```

**Merubah dan Memindahkan font:**

```sh
mkdir $HOME/.termux && mv /sdcard/Download/font.ttf $HOME/.termux/font.ttf
```

&nbsp;

---

## Sosial Media

[![Youtube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@BayuMahadika)
[![Instagram](https://img.shields.io/badge/Instagram-%23E4405F.svg?style=for-the-badge&logo=Instagram&logoColor=white)](https://www.instagram.com/bayu.mahadika)
[![TikTok](https://img.shields.io/badge/TikTok-%23000000.svg?style=for-the-badge&logo=TikTok&logoColor=white)](https://www.tiktok.com/@bayu.mahadika)

&nbsp;

---

## Referensi

**Plugins:** [https://vimawesome.com](https://vimawesome.com)\
**Color Schemes:** [https://vimcolorschemes.com](https://vimcolorschemes.com)
**Fonts:** [https://]

&nbsp;
