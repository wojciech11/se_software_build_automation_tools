# EX1

Please remember: do not copy&paste.

## Working with Git Basics

1. Please create a github user.

2. Generate a personal access token that works as a password, follow [the offical instructions](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

3. Create on your machine a directory:

   ```bash
   mkdir learning_git
   cd learning_git
   ```


4. Configure your git client to attach the right infromation to the commits (**replace** `wojciech11` with your github user):

   ```bash
   # small L
   git config -l
   git config --global user.name "wojciech11"

   # we do not like spammers
   git config --global user.email "wojciech11@users.noreply.github.com"

   # notice, that the complete configuration is stored
   # in the config
   cat ~/.gitconfig
   ```


4. Initilize the git repository:

   ```bash
   # check where you are
   pwd

   # initilize
   git init

   # notice
   # you will find the git repository in .git/
   ls .git/

   # you can also have your local
   # configuration
   cat .git/config
   ```

6. Create the first version of your `README.md`, please follow [the guide](https://guides.github.com/features/mastering-markdown/) to add sections, images, and lists. 

7. What is the role of `README.md`? Why is it important?

8. Let's learn how to use Git. We will practice the git mantra modifing README.md and saving every version of the file git. Please do 3 iterations:

   ```bash
   git status
   git add README.md
   git status
   git commit -m "My N commit" # N=1,2,3
   git status
   git log
   ```

9. Please see how the git history looks with a visual tools:

   ```bash
   gitk
   gitg
   ```
 
 10. Please create an empty github repository `learning_git`, follow the instructions:

     ```bash
     # the right path, you will find in the github instructions
     git remote add origin https://.../learning_git.git

     # run, it will fail
     git push

     # only once, later you can just call `git push`
     git push --set-upstream origin master
     ```

11. Let's go back to our git mantra and add one more step `git push`:

    ```bash
    git status
    # modify README.md
    git status
    git add README.md

    # without -m, git will open a text editor
    # for you to provide the message
    git commit
    git log
    git push

    # refrash the browser and check whether
    # you see your changes there
    ```

    Please do the git matra at least 3 times.

12. Too tired to copy&paste your token? You should enable the `credential.helper`:

    ```bash
    git config --global credential.helper store
    ```

    Now, git will remember your token.

    If you want to disable the helper, run the following commands:

    ```bash
    git config --global --unset credential.helper
    rm ~/.git-credentials
    ```


13. What if I want to clone (download) my code? Let's have a short exercise that shows how to do it:

    ```bash
    mkdir ~/tmp
    cd ~/tmp

	# url z github.com
    git clone https://github.com/<TWOJ_GITHUB_USER>/nauka_git
    ```

14. Draw a schema that shows how the process of adding changes to remote git repo works (in our case github).

## Git branches

1. Git branches? Pull request?

    ```bash
    # equivalent of `git status` but for braches
    git branch

    git checkout -b add-documentation

    git branch

    # add two or three commits
    # e.g.,
    mkdir docs
    touch docs/README.md

    # your fav editor
    atom docs/README.md

    # here comes the git commit mantra
    ```

    ```bash
    # good to see the history
    # in a graphical tool
    gitk
    gitg
    ```

    ```bash
    # let's publish our branch to github
    git push -u origin add-documentation
    ```

    ```bash
    git branch

    # let's see what we have in our directory 
    ls 
      

    # let's change the local branch to `master`
    git checkout master
    # what did change?
    ls


    # let's come back to the branch
    # with documentation
	 git checkout add-documentation

	 ls
    ```

2. Merging:

   ```bash
   git checkout master

   # let's get the changes from the add-documentation branch
   # on our master branch
   git merge add-documentation
   git push
   ```

## Pull Requests / Merge Requests

Follow the instructor.

## Branches and Automations

- feature branch workflow / [github flow](https://guides.github.com/introduction/flow/) / [trunk-based development](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development)
- your own with branches, e.g., `dev` -> the dev environemnt, `prod` -> production
- [git-flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) 

See also [comparing workflows](https://www.atlassian.com/git/tutorials/comparing-workflows).

## Tools

- simple: gitk, gitg; advanced: [sourcetree](https://www.sourcetreeapp.com/) or [kraken](https://support.gitkraken.com/how-to-install/); text-based: [tig](https://jonas.github.io/tig/)
- interesting: [gitmoji-cli](https://github.com/carloscuesta/gitmoji-cli)

## Additional materials

- Git commit messages: [semantic](https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716)/[conventional](https://www.conventionalcommits.org/en/v1.0.0/), imperative ([cbea.ms/git-commit](https://cbea.ms/git-commit/))
- Git style guide, e.g., https://github.com/agis/git-style-guide or https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

