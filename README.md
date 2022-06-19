# Software Build Automation Tools

## Requirements

- [Ubuntu](https://wiki.ubuntu.com/Releases) (or other linux) or MacOS
- Your favorite editor: vim/neovim, [vscode](https://code.visualstudio.com/), [atom](https://atom.io/), or [sublime](https://www.sublimetext.com/), or other (e.g., [Kakoune](https://www.redhat.com/sysadmin/kakoune-vi-text-editor))
- Your favorite IDE: PyCharm Community or [vscode](https://code.visualstudio.com/)
- (later) Docker installed

## Program

1. Basics: [manual intro](00_intro/README.md)([pl](00_intro/README_pl.md)) and [manual git](01_exercise/manual.md) ([pl](01_exercise/README_pl.md)) / [slides](01_slides/index.pdf):

   - linux basics
   - bash
   - Git
   - [Makefile](01_exercise/example/)

2. What is CI/CD? - [manual](02_exercise/README.md)([notes pl](02_exercise/README_pl.md)) / [slides](02_slides/index.pdf):

   - Makefile
   - tests
   - linters
   - [Python virtual environment](https://docs.python.org/3/tutorial/venv.html)

3. Docker and packaging - [manual](03_exercise/README.md):

   - Dependency hell
   - Packages
   - Docker

4. Time for your project and versioning conventions - [manual](04_exercise/README.md):

   - versioning conventions

5. Continuous Deployment - [manual](05_exercise/README.md) / [slides](05_slides/index.pdf):

   - Heroku as an example of PaaS
   - Continuous Deployment with Github actions

6. Summary & Exam - [slides](06_slides/)

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

- Python virtual environment:

  ```bash
  # create a venv in the .venv directory
  python3 -m venv .venv

  # activate
  source .venv/bib/activate

  # deactivate
  deactivate
  ```

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
