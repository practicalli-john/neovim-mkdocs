# NeoVim on Termux

A smart phone and an external keyboard can make an excellent ultra-portable development environment, especially when travelling with limited space or restricted weight constraints.

![Ultra-mobile development environment - android with Termux and NeoVim with Keyboardio Atreus keyboard](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/ultra-mobile-development--android-termux-neovim-keyboardio-atreus.jpg)

No special permissions are required to set up Termux and installation is made very simple by first installing FDroid marketplace.

## Android app Install 

FDroid from Google play store

Termux from F-Droid store

NOTE: Termux in Android Play store is out of date and not recommended


## Managing Termux 

Termux provides a CLI experience for Linux and the common development tools are easily installed

`pkg` command will add tools and libraries to the Linux environment from the currated packages in the software center.

`apt-cache search --names-only` - search for packages.

`apt-cache show package-name` - shows detail of package-name, including a description

?? - is package installed


> `pkg` is an alias for `apt`


### Keyboard 

Termux provides an extended keyboard with common key bindings for convienience and for combinations not possible with an on-screen keyboard, i.e `Ctrl-c  

For the best experience, especially when a lot of typing is required, pluy in a hardware keyboard.  

The on-screen keyboard is swiched off when a hardware keyboard it plugged in, although the extended keyboard is still displayer.

`Volume Up < q` toggles the extended keyboard, so more screen is available when using a hardware keyboard.

> An android setting to display to display of the on-screen keyboard when a physical keyboard is present


## Supporting tools

* `wget` and `curl` - download tools not packaged
* `git` - clone configuration files and projects
* `wget` - download files, i.e. clojure lsp binary
* `byobu` - multiple shell tabs in on frame


### Tools outside packages

Tools such as `clojure-lsp` are not part of the Termux Linux package system and can be downloaded from GitHub releases page via wget or curl

```
pkg install wget curl
```


### Git version control

Practicalli keeps several editor configurations in shared repositories on GitHub and GitLab

Instazll a git client

```
pkg install git
```

Clone the practicalli/dotfiles repository

```
git clone https...
```

Edit the `.config/git/config` and update identity


### Add a developer token

A developer token {or ssh key} is required to access GitHub {and far more secure over password}

Should the android device become lost or compromised, the developer token can be deleted to protect the repositories from any malicious access.  The developer token should be limited to the minimal access.  The developer token does not give access to the GitHub or GitLab account.

> HTTPS URLs should be used wiht a developer token.  git@git.com URLs are for SSH keys only.

Visit GitHub / GitLab settings for your account

Create a new developer token specifically for Termux

Add a descriptive name for the token, based on the device Termuxc is runniung on, e.g. `Termux Pixel2XL`

Check the public_repo and status repo scopes

Generate button creates a new token.  

Copy the token using the copy icon.

Edit the `.config/git/config` file and add a github section with the GitHub account name and token

```
[github]
	name = practicalli
	token = ghp_************************************
```

> Add a gitlab secion with the same keys if using GitLab 


### SSH Keys 

To add an ssh key to Termux reqiures a package installed that contains the ssh-keygen command, used to generate a new public/private key combinations
```
pkg install openssh
```

>  TODO: confirm openssh is the correct package for ssh-keygen


### byobu

A text window manager in a terminal to run multiple shell tabs, handy for opening multiple instances of neovim

```
pkg install byobu
 ```

`F2` to create a new tab
`F3` to select previous tab
`F4` to select next tab

> TODO: configure byobu to run by default (so I dont forget to run it)


ohmybash - a nice command line experience, shows completionms better, nice themes
- curl command from website
- customise by editing `.bashrc` file

?- tab completions like zsh and prezto?
?- powerline10k

Alternatively, install pkg zsh and clone prezto


## Install neovim
version 7 availabe as current package
```
pkg install neovim
```

## Neovim treesitter
treesitter provides excellent language syntax parsing and highlighting and is a very attractive feature of the recent neovim releases.  Treesitter is a major attraction, bringing in a new audience for Neovim.

### nodejs 

```
pkg install nodejs
```


install compiler for neovim-treesitter, to compile some packages

```
pkg install clang 
```

> `gcc` is not packaged for Termux, although there are guides to install gcc if preferred. clang seems to be working fine for now though


### install Java

Open JDK install supported, used to host Clojure code 

```
pkg install java-17
```

## Install Clojure

Linux install instructions with prefix
```
linux-install-1.11.113.sh --prefix /data/..../usr/

clojure install will add to the esisting bin, lib and share dorectories in ..../usr/

test by running basic built in repl
```
clojure 
```

> optionally install rlwrap - although Practicalli used Rebel Readline instead


## Install Clojure LSP

Visit GitHub releases page and download the `clojure-lsp` file 
- visit the relases page in firefox and copy the link to the file.
- use wget and paste the link to the file to download 
- make executable `chmod 755 clojure-lsp`
- test locally `./clojure-lsp --version` - should print clojure-lsp version and clj-kondo version
- copy or move file to path `mv clojure-lsp $PATH`



### Using newovim

`:!` for a shell command, e.g. to create a new directory
