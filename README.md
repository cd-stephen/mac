# mac_devel_setup
## References:
https://sourabhbajaj.com/mac-setup/SystemPreferences/
https://www.atpeaz.com/macos-set-up-for-coding-and-development-2021-edition/
https://brew.sh
https://medium.com/ayuth/iterm2-zsh-oh-my-zsh-the-most-power-full-of-terminal-on-macos-bdb2823fb04c
https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins
https://www.atpeaz.com/macos-set-up-for-coding-and-development-2021-edition/

## System Preferences
1. **System Update**:  Apple Menu > About This Mac > Software Update
2. **Users and Groups**
- [ ] Login Options: Change fast user switching menu as Icon
- [ ] Set up Password, Apple ID Profile
3. **Trackpad (optional)**
- [ ] Point and Click
	- Enable Tap to click with one finger
	- Change Secondary click to Right corner
	- Uncheck Three Finger Drag
- [ ] Scroll and Zoom
	- Uncheck all apart from Zoom in and out
4. **Dock**
- [ ] Visual settings: Change position to Left and make the size of icons Small
- [ ] Remove workspace auto-switching by running the following command.

```shell
defaults write com.apple.dock workspaces-auto-swoosh -bool NO
killall Dock # Restart the Dock process
```

5. **Finder**
* General
- [ ] Change New finder window show to open in your Home Directory
* Sidebar
- [ ] Add Home and your Code Directory
- [ ] Uncheck all Shared boxes

6. **Menubar**
- [ ] Remove the Display and Bluetooth icons
- [ ] Change battery to Show percentage symbols
7. **Spotlight**
- [ ] Uncheck fonts, images, files etc.
- [ ] Uncheck the keyboard shortcuts as we'll be replacing them with Alfred
8. **User Defaults**
- [ ] Enable repeating keys by pressing and holding down keys: 
`defaults write NSGlobalDomain ApplePressAndHoldEnabled -bool false` 
- [ ] Change the default folder for screenshots: run the following commads:
```shell
mkdir -p /path/to/screenshots/
defaults write com.apple.screencapture location /path/to/screenshots/ && killall SystemUIServer
```

## Xcode (required for Homebrew) ##

Xcode is an integrated development environment for macOS containing a suite of software development tools developed by Apple for developing software for macOS, iOS, watchOS and tvOS.

Download and install it from the App Store or from Apple's website.

For installing Xcode command line tools run:
`xcode-select --install`

## Homebrew ##
Homebrew calls itself The missing package manager for macOS and is an essential tool for any developer.
`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

### brew usage
Install a package (formula)
`brew install <formula>`

Update brew directories or packages
`brew update`

To see if any of your formulas need to be updated:
`brew outdated`

Homebrew keeps older versions of packages installed on your system, in case you want to roll back to an older version. That is rarely necessary, so you can do some cleanup to get rid of those old versions:
`brew cleanup`

To see what you have installed (with their version numbers):
`brew list --versions`

To uninstall a formula you can run:
`brew uninstall <package>`



Search for Packages
`brew search <package>`
### Install brew packages
```
brew install \
ack \
awscli \
curl \
docker \
fzf \
git \
mplayer \
openconnect \
openvpn \
terraform \
tree \
vim \
wget \
whois \
```


### Install Quick Look Plugins (omit)
These plugins add support for the corresponding file type to Mac Quick Look (In Finder, mark a file and press Space to start Quick Look). The plugins includes features like syntax highlighting, Markdown rendering, preview of JSON, patch files, CSV, ZIP files and more.
```shell
brew install --cask \
    qlcolorcode \
    qlstephen \
    qlmarkdown \
    quicklook-json \
    qlprettypatch \
    quicklook-csv \
    betterzip \
    webpquicklook \
    suspicious-package
```

## Homebrew-Cask
Homebrew-Cask extends Homebrew and allows you to install large binary files via a command-line tool. You can for example install applications like Google Chrome, Dropbox, VLC and Spectacle. No more downloading .dmg files and dragging them to your Applications folder!
### Application Installs  (Additional Documentation Below)
```shell
brew install --cask \
alfred \
android-file-transfer \
appcleaner \
caffeine \
dd-utility \
dropbox \
firefox \
google-chrome \
iterm2 \
joplin \
rectangle \
slack \
sublime-text \
transmission \
vagrant \
virtualbox \
visual-studio-code \
vlc \
```

### Install and Configure Terminal

#### Install iterm2, zsh, and oh-my-zsh
```shell
brew install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

#### Download iTerm color profile
.itermcolors file
https://github.com/mbadolato/iTerm2-Color-Schemes/tree/master/schemes

ie.
```shell
cd Downloads
curl -O https://raw.githubusercontent.com/MartinSeeler/iterm2-material-design/master/material-design-colors.itermcolors
```

1. Go to iTerm2 > Preferences > Profiles > Colors Tab
2. Click Color Presets… at the bottom right
3. Click Import…
4. Select the material-design-colors.itermcolors file
5. Select the material-design-colors from Load Presets…

#### Enable zsh plugins and permanent alias (for docker)
`vim ~/.zshrc`
`/plugins`
```
# Which plugins would you like to load? (plugins can be found in ~/.oh-my-zsh/plugins/*)
# Custom plugins may be added to ~/.oh-my-zsh/custom/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(
  git
  docker
)
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"
alias dkps="docker ps"
alias dkst="docker stats"
alias dkpsa="docker ps -a"
alias dkimgs="docker images"
alias dkcpup="docker-compose up -d"
alias dkcpdown="docker-compose down"
alias dkcpstart="docker-compose start"
alias dkcpstop="docker-compose stop"
```

#### ZSH Themes
future version

## git Config
Git and GitHub
`brew install git`

When done, to test that it installed properly you can run:
`git --version`

And `which git` should output `/usr/local/bin/git.`

Next, we'll define your git user (should be the same name and email you use for GitHub):
```
git config --global user.name "Your Name Here"
git config --global user.email "your_email@youremail.com"
```
They will get added to your `.gitconfig` file.

To push code to your GitHub repositories, we will use the recommended HTTPS method. There are also instructions for using SSH. To prevent git from asking for your username and password every time you push a commit you can cache your credentials by running the following command, as described in the [instructions](https://docs.github.com/en/get-started/getting-started-with-git/updating-credentials-from-the-macos-keychain).

`git config --global credential.helper osxkeychain`

## Using HTTPS for GitHub (recommended)
These instructions are from the [official documentation](https://help.github.com/en/github/using-git/which-remote-url-should-i-use#cloning-with-https-urls-recommended).

Clone repositories using HTTPS
After creating a new repo on GitHub, clone it using:

`git clone https://github.com/<username>/<repo-name>.git`
- if you had initialized with a README.

If you did not, follow the instructions in the section below.

### Set up a new or existing repo with HTTPS for GitHub
If you are setting up a new repo, add at least one file and commit first. Then, configure the remote and push to GitHub by running:

```
git remote add origin https://github.com/<username>/<repo-name>.git
git push -u origin master
```

## SSH Config for GitHub
These instructions are for those who wish to use SSH and not HTTPS, and are from the [official documentation](https://help.github.com/articles/generating-ssh-keys).

### Check for existing SSH keys
First check for existing SSH keys on your computer by running:

`ls -al ~/.ssh`
# Lists the files in your .ssh directory, if they exist
Check the directory listing to see if you have files named either id_rsa.pub or id_dsa.pub. If you don't have either of those files then read on, otherwise skip the next section.

### Generate a new SSH key
If you don't have an SSH key you need to generate one. To do that you need to run the commands below, and make sure to substitute the placeholder with your email. The default settings are preferred, so when you're asked to enter a file in which to save the key, just press Enter to continue.

```
ssh-keygen -t rsa -C "your_email@example.com"
# Creates a new ssh key, using the provided email as a label
```
### Add your SSH key to the ssh-agent
Run the following commands to add your SSH key to the ssh-agent.

`eval "$(ssh-agent -s)"`
If you're running macOS Sierra 10.12.2 or later, you will need to modify your `~/.ssh/config` file to automatically load keys into the ssh-agent and store passphrases in your keychain:

```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```
No matter what operating system version you run you need to run this command to complete this step:

`ssh-add -K ~/.ssh/id_rsa`

### Adding a new SSH key to your GitHub account
The last step is to let GitHub know about your SSH key so GitHub can recognize you. Run this command to copy your key to your clipboard:

`pbcopy < ~/.ssh/id_rsa.pub`
Then go to GitHub and input your new SSH key.[https://github.com/settings/ssh/new](https://github.com/settings/ssh/new) 
Paste your key in the "Key" text-box and pick a name that represents the computer you're currently using.

We are now ready to use SSH with GitHub!

#### gitignore
Generate gitignore
[gitignore.io](https://www.toptal.com/developers/gitignore)
(macos, linux, terraform, python)

`git config --global core.excludesfile ~/.gitignore`


### Chrome Extentions
https://chrome.google.com/webstore/detail/json-formatter/bcjindcccaagfpapjjmafapmmgkkhgoa?hl=en

https://chrome.google.com/webstore/detail/dailydev-the-homepage-dev/jlmpjdjjbgclbocgajdjefcidcncaied?hl=en

### VS Code Extentions
https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers

https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker

https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense


vs-code-icons:  vscode-icons-team.vscode-icons

docker ms-azuretools.vscode-docker

formulahendry.docker-explorer
chef-software.chef
tomaciazek.ansible
