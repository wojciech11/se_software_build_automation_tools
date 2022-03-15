# Software Build Automation Tools

## Requirements

- [Ubuntu](https://wiki.ubuntu.com/Releases) (or other linux) or MacOS
- Your favorite editor: vim/neovim, [vscode](https://code.visualstudio.com/), [atom](https://atom.io/), or [sublime](https://www.sublimetext.com/), or other (e.g., [Kakoune](https://www.redhat.com/sysadmin/kakoune-vi-text-editor))
- Your favorite IDE: PyCharm Community or [vscode](https://code.visualstudio.com/)
- (later) docker installed

## Program

1. Basics: [manual intro](00_intro/README.md) and [manual git](01_exercise/manual.md) / [slides](01_slides/index.pdf):

   - linux basics
   - bash
   - Git
   - [Makefile](01_exercise/example/)

2. What is CI/CD? - [manual](02_exercise/README.md) / [slides](02_slides/index.pdf):

   - Makefile
   - tests
   - linters
   - [Python virtual environment](https://docs.python.org/3/tutorial/venv.html)

3. Docker and packaging - [manual](03_exercise/README.md):

   - Dependency hell
   - Packages
   - Docker

4. Other tools <!-- [12/15] -->

5. Summary & Exam  <!-- [15/15] -->

## Useful commands

- Text editors:

  ```bash
  # 
  sudo apt update
  
  # choose your own adventure!
  
  # vim
  sudo apt-get install vim
  
  # neovim
  sudo apt install neovim
  
  # vscode
  sudo snap install code --classic
  
  # atom
  sudo snap install atom --classic
  
  # sublime
  # follow instructions from:
  # https://www.sublimetext.com/docs/linux_repositories.html
  ```

- IDE

  - Pycharm - see the [installation guide](https://www.jetbrains.com/help/pycharm/installation-guide.html#toolbox))
  - vscode - `sudo snap install code --classic`

- Docker (after [how to install Docker on ubuntu](https://docs.docker.com/engine/install/ubuntu/#installation-methods)):

   ```bash
   # install docker
   sudo su

   apt-get update ;
   apt-get install -qq apt-transport-https ca-certificates curl software-properties-common ;
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - ;
   add-apt-repository 'deb [arch=amd64] https://download.docker.com/linux/ubuntu '$(lsb_release -cs)' stable' ;
   apt-get update ;
   apt-get install -qq docker-ce ;

   # do not forget to exit
   exit
   ```

## Optional materials

- https://missing.csail.mit.edu/


