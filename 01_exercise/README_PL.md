# Ćwiczenia 1

Proszę bez kopiuj&wklej. Czytaj uważnie instrukcję. Wersja po angielsku - [manual.md](manual.md).

## Podstawy pracy z Gitem

System kontroli wersji (SCM – Source Controll Management), jest podstawą każdego projektu.
Możesz używać gita do zachowywania aplikacji i skryptów rozwijanych w czasie zajęć.

1. Utwórz konto na githubie -  https://github.com/join

2. Zmieniła się̨ polityka GitHub i nie można już̇ logować́ się̨ hasłem od konta, dlatego sprawdź́ w dokumentacji jak wygenerować́ token i go użyć - [oficjalna dokumentacja](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). Zaznacz dwa zakresy dla tokena:

   - repository
   - workflow

3. Jeśli pracujesz na współdzielonej maszynie to utwórz folder o nazwie takiej jak Twój użytkownik gita (którego właśnie utworzyłeś) – jeśli pracujesz na swojej maszynie, utwórz folder workspace:

   ```bash
   # na swoim laptopie
   mkdir -p workspace/nauka_gita
   cd workspace/nauka_gita
   ```

   ```bash
   # na wspołdzielonym komputerze
   # uzywamy nazwe githuba, aby uniknac kolizji
   mkdir -p workspace/NAZWA_UZTYK_GITHUB/nauka_gita
   cd workspace/NAZWA_UZTYK_GITHUB/nauka_gita
   ```

4. Skonfiguruj git-a (zastąp **wojciech11** swoim użytkownikiem githuba):

   ```bash
   # make L
   git config -l
   git config --global user.name "wojciech11"

   # nie lubimy spamerów
   # (email jest dołączony do zapisów w git/githubie)
   git config --global user.email "wojciech11@users.noreply.github.com"

   # zauważ, że cała globalna konfiguracja jest w następującym pliku
   cat ~/.gitconfig
   ```


4. Zainicjuj repozytorium git-a:

   ```bash
   # sprawdź, czy jesteś we właściwej ścieżce
   pwd

   # powinienies zobaczyc
   # sciezke konczaco sie nauka_gita

   # utworz repozytorium
   git init

   # zawuaz
   # ze repozytorium jest w .git/
   ls .git/

   # zauwaz ze repozytorium ma swoj
   # plik konfiguracyjny
   cat .git/config
   ```

6. Podążając za wskazówkami wykładowcy, utwórz `README.md` za pomocą atom (packages -> Markdown Preview -> Toggle).

   ```bash
   touch README.md

   # otwórz edytor atom w katalogu glownym
   # repozytorium
   atom .
   ```

   Dodaj kilka sekcji, obrazów, listy... pobaw się formatem Markdown podążając za wskazówkami z [dokumentacji](https://guides.github.com/features/mastering-markdown/).

7. Jak jest rola pliku `README.md`? Dlaczego plik README jest tak istotny?

8. Nauczymy się jak używać Gita. Podążaj za wskazówkami wykładowcy, aby nauczyć się o komendach git działających na lokalnym repozytorium:

   ```bash
   git status
   git add README.md
   git status
   git commit -m "My N commit" # N=1,2,3
   git status
   git log
   ```

   Zmodyfikuj README.md i umieść zmiany w repozytorium. Powtórz 3 razy.

9. Przyglądnij się, jak wygląda historia z pomocą graficznych programów `gitk` i `gitg`:

   ```bash
   gitk
   gitg
   ```

   Doskonałymi graficznymi środowiskami do pracy z gitem jest [sourcetree](https://www.sourcetreeapp.com) i [gitkraken](https://www.gitkraken.com).

 10. Czas umieścić nasz projekt na githubie. Utwórz repozytorium w githubie, przez przeglądarkę, używając interfejsu webowego - `nauka.gita`:

     ```bash
     # tak jak podpowiada wam github.com
     git remote add origin https://.../learning_git.git

     # **przeczytaj**
     # na co git "narzeka"
     # po wykonaniu następującej
     git push

     # podazajac za wskazowka
     # pelna komenda:
     git push --set-upstream origin master
     ```

     Jak nasze lokalne repozytorium jest połączone ze zdalnym repozytorium:

     ```bash
     # aby zobaczyc jak nasze lokalne repozytorium w katalogu .git
     # ma swoj odpowiednik w githubie
     git remote -v
     ```

     Wizualizacja:

     ```mermaid
     flowchart BT
     l(local\n.git) -- origin --> H(remote\ngithub)
     ```

11. Wróćmy do naszej mantry ale tym razem dodamy  `git push`:

    ```bash

    git status

    # zmien README.md
    git status
    git add README.md

    # bez -m,
    # git otworzy domyslny edytor
    git commit
    git log
    git push

    # odswiez w przeglarce swoje repozytorium
    # nauka_gita
    ```

    Proszę wykonaj wszystkie kroki przynajmniej 3 razy.

12. Boże! Ile razy mam podawać hasło (token). Jest na to rozwiazanie. Powinieneś włączyć `credential.helper`:

    ```bash
    git config --global credential.helper store
    ```

    Now, git will remember your token.

    If you want to disable the helper, run the following commands:

    ```bash
    git config --global --unset credential.helper
    rm ~/.git-credentials
    ```

13. A co gdy ma repozytorium na githubie i chce zacząć z nim pracować lokalne. Ściągnąć repozytorium? Zobaczmy jak to zrobić:

    ```bash
    # przejdzmy do innego katalogu
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
