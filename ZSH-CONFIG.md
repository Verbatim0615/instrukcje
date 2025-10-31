

# START
source "$HOME/.zinit/bin/zinit.zsh"
zinit light ohmyzsh/ohmyzsh

# THEME 
zinit light romkatv/powerlevel10k

# Podstawowe, ale kluczowe plugi.
zinit light zsh-users/zsh-autosuggestions   # Podpowiedzi komend
zinit light zsh-users/zsh-history-substring-search # Wyszukiwanie w historii
zinit light zdharma-continuum/fast-syntax-highlighting # Szybkie kolorowanie składni

# FZF. 
zinit light Aloxaf/fzf-tab

# KATALOGI
zinit light agkozak/zsh-z

# Uzupełnianie
zinit light zsh-users/zsh-completions

#CONFIG

# Ustawia domyślny edytor na Vim.
export EDITOR='vim'
export VISUAL="$EDITOR"

# Ustawienie dla `less` - lepsze kolory i obsługa.
export LESS_TERMCAP_mb=$'\e[1;32m'
export LESS_TERMCAP_md=$'\e[1;32m'
export LESS_TERMCAP_me=$'\e[0m'
export LESS_TERMCAP_se=$'\e[0m'
export LESS_TERMCAP_so=$'\e[1;33m'
export LESS_TERMCAP_ue=$'\e[0m'
export LESS_TERMCAP_us=$'\e[1;4;31m'


# ALIASy 


# --- Podstawowe aliasy ---
alias v='$EDITOR'
alias c='clear'
alias ..='cd ..'
alias ...='cd ../..'
alias ls='ls -G' # -G \alias la='ls -la'
alias ll='ls -lh'
alias l.='ls -d .* --color=auto'
alias grep='grep --color=auto'

# Sieć
alias myip='curl -s ifconfig.me; echo'
alias b64enc='base64'
alias b64dec='base64 -d'
alias sha256='openssl dgst -sha256'
alias nmap-top='sudo nmap -sS --top-ports 1000'

# --- Aliasy dla Git ---
alias g='git'
alias ga='git add'
alias gaa='git add -A'
alias gc='git commit -v'
alias gca='git commit -v -a'
alias gs='git status -s'
alias gpl='git pull'
alias gps='git push'
alias glog="git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"


# FUNKCE

# Tworzy katalog i od razu do niego przechodzi.
mkcd() {
  mkdir -p "$1" && cd "$1"
}

# Rozpakowuje dowolne archiwum. Użycie: `extract <plik>`.
extract() {
    if [ -f "$1" ]; then
        case "$1" in
            *.tar.bz2) tar xjf "$1" ;;
            *.tar.gz)  tar xzf "$1" ;;
            *.bz2)     bunzip2 "$1" ;;
            *.rar)     unrar x "$1" ;;
            *.gz)      gunzip "$1"  ;;
            *.tar)     tar xf "$1"  ;;
            *.tbz2)    tar xjf "$1" ;;
            *.tgz)     tar xzf "$1" ;;
            *.zip)     unzip "$1"   ;;
            *.Z)       uncompress "$1" ;;
            *.7z)      7z x "$1"    ;;
            *)         echo "'$1' nie może zostać rozpakowane" ;;
        esac
    else
        echo "'$1' to nie jest prawidłowy plik"
    fi
}

# Szybka funkcja do sprawdzenia, czy DNSy odpowiadają.
checkdns() {
    echo "Pinging Cloudflare DNS (1.1.1.1)..."
    if ping -c 2 1.1.1.1 &> /dev/null; then
        echo "✅ Połączenie z 1.1.1.1 udane."
    else
        echo "❌ BŁĄD: Brak połączenia z 1.1.1.1."
    fi

    echo "\nPinging Google DNS (8.8.8.8)..."
    if ping -c 2 8.8.8.8 &> /dev/null; then
        echo "✅ Połączenie z 8.8.8.8 udane."
    else
        echo "❌ BŁĄD: Brak połączenia z 8.8.8.8."
    fi
    echo "\nTest zakończony. Jeśli widzisz błędy, problem może leżeć w DNS lub połączeniu sieciowym."
}

# Uruchamia prosty serwer HTTP w bieżącym katalogu (port 8000).
py-server() {
  python3 -m http.server "${1:-8000}"
}


# HISTORIA 


HISTFILE=~/.zsh_history
HISTSIZE=10000
SAVEHIST=10000

# Opcje historii - bez duplikatów, współdzielona między terminalami.
setopt APPEND_HISTORY
setopt EXTENDED_HISTORY
setopt HIST_IGNORE_ALL_DUPS
setopt HIST_REDUCE_BLANKS
setopt SHARE_HISTORY

# Inne opcje dla wygody.
setopt AUTO_CD          # Automatyczne `cd`
setopt AUTO_PUSHD       # Automatycznie dodaje katalogi do stosu
setopt PUSHD_IGNORE_DUPS
setopt CORRECT          # Poprawia literówki w komendach
setopt EXTENDED_GLOB    # Zaawansowane wzorce glob


# OPCJE

# Lepsze kolory dla menu uzupełniania (completion menu).
# zstyle ':completion:*' menu select
# zstyle ':completion:*:*:kill:*:processes' list-colors '=(#b) #*0=01;31'
# zstyle ':completion:*' list-colors "${(s.:.)LS_COLORS}"
# zstyle ':completion:*' group-name ''
# zstyle ':completion:*:descriptions' format '%B%d%b'

# Przykładowa konfiguracja dla motywu powerlevel10k.
# Można to wygenerować komendą `p10k configure`.
# typeset -g POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(os_icon dir vcs)
# typeset -g POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status command_execution_time background_jobs time)


