# Linux basics

If you are looking for the manual in Polish, you will find it [here](README_pl.md).

## Survival

1. From GUI to Terminal:

   <img src="img/ubuntu_open_terminal.png" width="40%" />

2. From terminal to GUI:

   ```bash
   ls
   xdg-open .
   ```

3. Explore your home directory:

   ```bash
   #
   ls

   # $HOME stores
   # path to your home directory
   ls $HOME

   echo $HOME
   ```

4. Survival 1 - where am i? Why I get `No such file or directory` or `Permission denided`? Twese two commands will help you:

   ```bash
   pwd

   ls
   ```

5. Survival 2 - how can I come back to my home directory?

   ```bash
   # main directory in linux is: /  the same as C: in Windows
   cd /
   pwd

   # come back home with one command
   cd

   # let's do it again
   cd /
   pwd
   ls

   # ~ means my home directory
   # change the directory to ~
   cd ~
   ```

6. Before learning how to work with directories, let's install `tree`:

   ```bash
   sudo apt-get update
   sudo apt install tree
   ```

   Sudo? [We have xkcd for that!](https://xkcd.com/149/).

7. Working with the directories:

   ```bash
   mkdir poland
   cd poland
   mkdir cities
   cd cities
   mkdir gdansk
   ls
   mkdir warszawa
   mkdir wroclaw
   mkdir krakow
   ls
   cd ..
   pwd
   cd ..

   tree

   tree ../poland
   ```

   You should see:

   ```
   poland
   \- cities/
      |- gdansk/
      |- warszawa/
      |- wroclaw/
      \- krakow/
   ```

8. Traverse the directories `cd PATH`:

   ```bash
   # go in
   pwd
   cd cities/krakow
   pwd

   # go out
   cd ../..
   ```
9. Notice:

   ```bash
   ls cities
   ls /home/
   ls ~
   ```

10. Please add a directory `villages` that contains directories for small settlements in Poland:

    ```
    poland
     |- cities/
     |   |- gdansk/
     |   |- krakow/
     |   |- warszawa/
     |   \- wroclaw/
     |
     \- villages/
        |- nowawies
        \- starawies
    ```

11. Survival 3 - vim:

    - install vim:

      ```bash
      sudo apt-get install vim
      ```

    - go back to your home dir: `cd`

    - let's start vim:

      ```bash
      vim learning_vim.txt
      ```

    - How to exit:

      1. ESC ESC
      2. :q
      3. ENTER

    - iii! I added a text (insert mode: `ESC ESC i`), but I just want to exit the vim without saving the content!

      1. ESC ESC
      2. :q!
      3. ENTER

    - ok. Now I would like to add something to my file:

      1. `vim learning_vim.txt`
      2. ESC ESC
      3. i
      4. Please add sth, e.g., `I love vim!`
      5. ESC ESC
      6. :wq
      7. ENTER
      8. Let's see whether we saved the content:

         ```bash
         cat learning_vim.txt
         ```

12. Survival 4 - emacs / nano:

    ```bash
    nano
    ```

    Notice, `^` means CTL/CONTROL.

13. If you look for sth like notebook: `gedit p.txt`

## Remember

1. If the command does not print anything, it means it succeeded
2. Use: `TAB` `TAB` to get your commands autocompleted

## Working with files

1. Let's go back to your home dir and create a dedicated directory for the exercises:

   ```bash
   cd
   mkdir workspace
   cd workspace
   ```

2. Creating files with `touch` ([to remember it](https://cdn.britannica.com/77/2577-004-DA7549AE/The-Creation-of-Adam-ceiling-fresco-Michelangelo.jpg?s=1500x700&q=85)) and writing to them with `echo`:

   ```bash

   touch myfile.txt # create an empty file

   echo "Ubuntu 18.04" > myfile.txt
   echo "Ubuntu 20.04" >> myfile.txt

   cat myfile.txt
   echo "Mint" >> myfile.txt
   echo "Debian" >> myfile.txt
   echo "Redhat" >> myfile.txt
   echo "Linux" >> myfile.txt

   cat myfile.txt
   ```

3. Ofc, you can use the graphical editor or vim to change the file content:

  ```bash
  atom myfile.txt
  ```

4. `grep` is a basic CLI tool for the automation. Notice it is case sensitive:

   ```bash
   grep Linux myfile.txt

   grep Ubuntu myfile.txt
   # compare with:
   grep ubuntu myfile.txt
   ```

   ```
   grep -i ubuntu myfile.txt
   ```

5. A common use case, we have logs to analyze:

   ```bash
   grep -i Error /var/log/*log
   # alternative to `wc -l`
   grep -c -i Error /var/log/*log
   ```

6. How to copy files, use `cp`:

   ```
   cp myfile.txt myfile2.txt

   ls

   # we can `grep` all files
   # that ends with `.txt`
   grep Linux *.txt
   ```

7. How to move file (or rename file) from one directory to another?

   ```bash
   mkdir mydirectory
   mv myfile2.txt mydirectory
   ls mydirectory
   tree ../

   # let's move the file back
   # to the current directory `.`
   $ mv mydirectory/myfile2 .
   ```

8. We also use `mv` to rename files, let's go back to our directories for Polish cities and villages:

   ```bash
   cd ~
   cd poland
   ls
   # sb asked us to use Polish word for cities
   # - miasta
   mv cities miasta
   ls
   tree ../poland
   ```

9. What if we need to have both, a directory with Polish name and English:

   ```bash
   cp -r miasta cities
   cd ..
   tree poland
   ```

   You should see `miasta` and `cities`.

10. Use `rm` to remove a file:

    ```bash
    cd
    cd workspace
    rm myfile2.txt
    ```

11. ... or to delete a directory with content:

    ```bash
    cd
    ls poland
    rmdir poland/cities/warszawa

    # does it work?
    rmdir poland/cities

    # if not, try this command:
    rm -r poland/cities
    ```

12. To close this section, create in your home directory (`*.txt` are files):

    ```
    biology/
    |- trees
    |      |- deciduous.txt
    |      \- coniferous.txt
    |
    \- animals
        |- predators
        |   \- cats.txt
        \- herbivorous
            \- cows.txt
    ```

    Tasks (use `tree` to check whether you completed the task):
    1. Move files `cats.txt` and `cows.txt` under `animals/`,
    2. Copy `coniferous.txt` to your home directory, check with `ls ~` whether you succeeded,
    3. Delete the `animals` directory,
    4. Delete the `biology` directory.

## Useful

1. We have in Linux hidden files. The hidden files starts with `.`:

   ```bash
   cd
   ls -a
   ls -la
   ls -la | grep bash
   ```

2. Environment variables, we use in every automation. Let's find out what the value is for the `HOME` and `LANG` variables:

   ```bash
   printenv
   printenv | grep HOME=
   printenv | grep LANG=

   echo $HOME
   ```

3. Printing environment variables:

   ```bash
   # compare
   $ echo "$HOME"
   $ echo '$HOME'

   # recommendation:
   # always with { and }
   $ echo "${HOME}"
   ```

4. Printing env variable to file:

   ```bash
   cd ~
   mkdir tmp
   cd tmp

   echo "$HOME" > home.txt
   cat home.txt
   ```

5. Adapt your command line interface with $HOME/.bashrc

   ```bash
   atom $HOME/.bashrc
   ```

   Add at the end of the `~/.bashrc`:

   ```bash
   echo "Hi ${USER}!"
   export MY_PHONE=9999
   ```

   Open another terminal window or run `bash` in the exiting terminal window.

   ```bash
   # notice TAB TAB works
   echo $MY_PHONE
   ```

6. You can define a new env variable ad hoc in your terminal:

   ```bash
   export SHOP_USER=natalia
   echo "$SHOP_USER"
   ```

7. Create your first bash script `my_script.sh` with the following content:

   ```bash
   #!/bin/bash

   echo "Hi ${USER}! Nice to meet you!"
   echo "Your home directory is ${HOME}"
   echo "Your configured language is ${LANG}"
   ```

   and run it:

   ```bash
   bash my_script.sh
   ```

## Where can I find X?

```bash
cd
find . -iname *.txt

# ensure we get the file:
find . -iname *.txt -type f

# find in the home directory `~`
# a directory `-type d`
# with name `poland`
find ~ -iname poland -type d
```

### Working with text files

1. You got an export from your ecommerce shop `koszyk1.txt`:

   ```
   milk,10,1zl
   bread,1,4zl
   ```

   Using `cut`:

   ```bash
   cut -d',' -f1 koszyk1.txt
   cat koszyk1.txt | cut -d',' -f1
   ```

   extract:

   ```
   1zl
   4zl
   ```

   Bonus task:

   1. Print the user names from `/etc/passwd`
   2. Extract month and days from `/var/log/syslog`

2. Another day, another weird export from an online shop `koszyk2.txt`:

   ```

   product=mleko
   price=1
   product=chleb
   price=4
   ```

   With help of `cut` and `paste`, print on the screen:

   ```

   mleko 1
   chleb 4
   ```

   Hint:

   ```bash
   cat koszyk2.txt | paste - -
   ```

3. Let's learn how to replace strings, assuming we have `koszyk3.txt` with the following content:

   ```
   product_category: mleczne
   ```

   Our task is to replace `mleczne` (Polish word for the diary products) with the category ID `M0`:

   ```
   product_category: M0
   ```

   Hint:

   ```bash
   sed 's/category/cat/g'
   ```

4. `tr` is very useful when you need to replace a single character:

   ```bash
   cat koszyk3.txt | tr ':' '='
   ```
   
   or remove it:

   ```bash
   cat koszyk3.txt | tr -d ':'
   ```

5. Please find out what `head`, `tail`, and `less` do:

   ```bash
   less /var/log/syslog
   tail /var/log/syslog
   head /var/log/syslog
   head -n 10 /var/log/syslog
   ```

6. Given the following basket export structure (notice `*.txt` are files):

   ```
   basket
   |- chocolates
   |   \- products.txt
   |      wedel,2
   |      goplana,3
   |
   |- dairy
       \- products.txt
          mlekovita,5
          zimnemleko,4
   ```

   1. With one command print the price for each of the item:

      ```
      2
      3
      5
      4
      ```

   2. With one command (find it with help of Google on stackoverflow), calculate the basket value:

      ```
      14
      ```

   Notice how easy is to find a solution for a common problem in bash.

## Homework

Install one from these two:

- [ohmybash](https://ohmybash.nntoan.com/) / [bash-it](https://github.com/Bash-it/bash-it) if you are on Linux
- [ohmyzsh](https://github.com/ohmyzsh/ohmyzsh) if you are on Macos ([a blog post for MacOS](https://towardsdatascience.com/the-ultimate-guide-to-your-terminal-makeover-e11f9b87ac99?gi=5b5538f07a5d#367b)) or you are on Linux ([blog post](https://vitux.com/ubuntu-zsh-shell/))

There are many plugins that gives you super powers in your terminal, you can check the top plugins on [this page](https://safjan.com/top-popular-zsh-plugins-on-github-2021/).

## Additinal materials

- [better bash scripting in 15 minutes](http://robertmuth.blogspot.com/2012/08/better-bash-scripting-in-15-minutes.html)
