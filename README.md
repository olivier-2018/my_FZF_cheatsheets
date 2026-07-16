# fzf-cheatsheets

Use [fzf](https://github.com/junegunn/fzf) to search through "cheatsheets" of
useful commands.

![Demo of the features, showing selecting commands from the cheatsheets in various ways](demo.gif?raw=true "Demo")

## Installation

### Requirements: zsh (or better oh-my-zsh)

- Install: [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh)
- Use the fzf plugin --> .zshrc line 75 --> plugins=(fzf ...)

The "fzf-cheatsheets" repo folder is used as a oh-my-zsh plugin just like fzf, so just

    git clone git@github.com:olivier-2018/my_FZF_cheatsheets.git  ~/.oh-my-zsh/plugins/fzf-cheatsheets

### Requirements: fzf

Clone the FZF repo 

    git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf


Install FZF: 

    ~/.fzf/install
    # Note: No need to update your shell configuration files


Enable Fuzyy search by adding the following to the ~/.zshrc:

    # FUZZY-SEARCH
    # ---------
    # source: https://github.com/junegunn/fzf#using-git
    # activate with Ctrl-t (files), ALT-c (folder),  Ctrl-r (history)
    if [[ ! "$PATH" == *${HOME}/.fzf/bin* ]]; then
    PATH="${PATH:+${PATH}:}${HOME}/.fzf/bin"
    fi
    export FZF_DEFAULT_OPTS="--height 80% --preview 'batcat --style=numbers --color=always --line-range=:500 {}' --preview-window=right:60%"
    export FZF_CTRL_T_OPTS="--height 80% --preview 'batcat --style=numbers --color=always --line-range=:500 {}' --preview-window=right:60%"
    export FZF_ALT_C_OPTS="--height 80% --preview 'tree -C {} | head -200' --preview-window=right:60%"
    source <(fzf --zsh)


### fzf-cheatsheets

Once Fuzyy search is enabled, add the following to the ~/.zshrc:

    # FZF_CHEATSHEETS
    # activate: Ctrl-x Ctrl-y   OR fzf-cheatsheets <cmd>
    FZF_CHEATSHEETS_DIR=${HOME}/.oh-my-zsh/plugins/fzf-cheatsheets
    export PATH="$PATH:${FZF_CHEATSHEETS_DIR}/bin"
    source ${FZF_CHEATSHEETS_DIR}/shell/fzf-cheatsheets.zsh


Then restart your shell.


## Usage

The default binding is `Ctrl-x Ctrl-p` (i.e. hit one then the other).

You will be prompted to select the cheatsheet to use, and then to select
the command that you want.

Hitting `Enter` at the command listing will place that command in to your
prompt for you to change or execute.

Hitting `Ctrl-e` will open your editor to edit the command. There
will be comments to help you understand what the command does, and you
can leave those there. Once you are happy then quit your editor and
your command line will contain the command ready to run.

If you have some text in your prompt already then that will be used to
pre-filter the options.

The first word in the command line will select the cheatsheet, so if you have

    > git 

when you activate the plugin it will immediately offer you the commands from
the cheatsheet for `git`.

If you have

    > git push

when you activate the plugin it will select the `git` cheatsheet, and put
`push` as the query in the command selector, hopefully taking you to the
commands that you are interested in. You can amend the query however you like
at this point.

You can also use the command directly if you prefer:

    fzf-cheatsheets
    fzf-cheatsheets git

In this case the command will be executed when you have finished, it won't be
added to your command line.


## Available Cheatsheets

The cheatsheets directory includes **6000+ commands** across **51 CLI tools** organized for quick reference:

### Cloud & Infrastructure (900+ commands)
- **aws** — Amazon Web Services; 50+ services (S3, EC2, Lambda, RDS, IAM, CloudWatch, etc.)
- **az** — Microsoft Azure CLI; 30+ services (VMs, Storage, SQL, AKS, Key Vault, etc.)
- **gcp** — Google Cloud Platform CLI; 30+ services (Compute, Storage, BigQuery, Vertex AI, etc.)

### Text Processing & Search (250+ commands)
- **grep** — Search text with patterns and regex filters
- **find** — Locate files by name, size, date, and other properties
- **sed** — Stream editing for text transformation and substitution
- **awk** — Pattern scanning and text processing language

### Data & Web Tools (200+ commands)
- **jq** — JSON query and manipulation language
- **curl** — HTTP client for transferring data with URLs
- **xargs** — Build and execute commands from standard input

### Text Manipulation (110+ commands)
- **cut** — Extract columns or fields from text
- **sort** — Sort, merge, and organize text data

### Linux Networking & Security (2300+ commands)
- **netstat** — Display network connections and statistics
- **ping** — Test host reachability with ICMP
- **traceroute** — Show network path to destination
- **ip** — Modern network configuration and routing
- **ss** — Socket statistics (netstat replacement)
- **dig** — DNS query tool for domain lookups
- **nmap** — Network scanner for port discovery
- **whois** — Query domain and IP registration
- **curl** — HTTP client for web requests (also listed above)
- **wget** — File download utility (also listed above)
- **ftp** — File transfer protocol client
- **ssh-keygen** — OpenSSH key generation and management
- **iptables** — IP packet filtering and firewall
- **ufw** — Uncomplicated firewall (iptables wrapper)
- **firewalld** — Dynamic firewall manager
- **fail2ban** — Intrusion prevention (brute force blocking)
- **arping** — ARP ping for MAC discovery
- **bmon** — Bandwidth monitor
- **who/whoami/w** — User login and activity monitoring

### Linux System & Administration (1400+ commands)
- **ps** — Process snapshot and listing
- **top** — Interactive process monitor
- **kill** — Send signals to terminate processes
- **sudo** — Execute with superuser privileges
- **free** — Display memory usage and statistics
- **systemctl** — Systemd service and unit manager
- **passwd** — Change user passwords
- **usermod** — Modify user account properties
- **crontab** — Schedule recurring tasks
- **shutdown** — Halt, power-off, or reboot system
- **nice** — Adjust process priority
- **time** — Measure command execution time
- **screen** — Terminal multiplexer/session manager
- **history** — Shell command history navigation
- **lsof** — List open files and network connections
- **vmstat** — Virtual memory and performance statistics

Each cheatsheet includes:
- **Curated `--help` header** — Usage synopsis and key options at the top of the file
- **Practical examples** — Real-world usage patterns organized by functionality
- **Grouped categories** — Commands sorted by purpose for easy navigation
- **Extended descriptions** — 1-3 line explanations optimized for the fzf preview pane


## Adding cheatsheets

You can add your own cheatsheets.

You can set `CHEATSHEETS_DIR` environment variable to point to a set of
cheatsheet files, or you can send PRs here.

The files should be named after the command that they should be used for.

The cheatsheet files are pretty simple, with a command per line.

    git status

Comments can be added after the command

    git status # Shows the status of the repo

For more complex commands you can add comments on following lines to expand
further.

    git status # Shows the status of the repo
    # Here is some more information

Everything up to the next command will be considered comments for that
command.


### Awesome Cheatsheets

You can also use the [awesome-cheatsheets](https://github.com/LeCoupa/awesome-cheatsheets)
repo directly, though the formatting is not consistent there and so the help
messages will be less useful.

Simply checkout that repo somewhere:

    git clone git@github.com:LeCoupa/awesome-cheatsheets.git path/to/awesome-cheatsheets

and point your `FZF_CHEATSHEETS_DIR` to that directory in your `zshrc` or
`bashrc`:

    FZF_CHEATSHEETS_DIR=path/to/awesome-cheatsheets


## Acknowledgements:

[James FZF-cheatsheet](https://github.com/james-w/fzf-cheatsheets)

Reddit user u/techAndLanguage [suggested the idea](https://www.reddit.com/r/vim/comments/g8haqm/question_about_how_to_use_vim_as_a_stream_editor/)

Some of the cheatsheets started from [awesome-cheatsheets](https://github.com/LeCoupa/awesome-cheatsheets)

