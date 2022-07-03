# WIP - Notes

1. Cel: nowe repozytorium gita na twoim koncie o nazwie `hello_world_app` z zawartością - https://github.com/wojciech11/se_software_build_automation_tools/tree/master/02_exercise/hello_world

   Podpowiedź 1:

   1. Utwórz folder `hello_world_app` i zainicjalizuj lokalne repozytorium git
   2. W innej lokalizacji, np., `tmp`, sklonuj repozytorium z plikami.
   3. Znajdź w `se_software_build_automation_tools` folder z plikami `02_exercise/hello_world` zanotuj ścieżkę (`pwd`).
   4. Wróć do katalogu `hello_world_app`.
   5. Przekopiuj pliki z użyciem `cp -R`.

   Podpowiedź 2:

   ```bash
   cd
   mkdir tmp
   cd tmp

   # klonowanie
   # pobieranie kodu na lokalny komputer
   git clone https://github.com/wojciech11/se_software_build_automation_tools
   
   cd se_software_build_automation_tools
   ls
   
   cd 02_exercise/hello_world
   ls
   
   pwd
   ```

   ```bash
   cd
   mkdir hello_world_app
   cd hello_world_app
   git init

   cp -r SCIEZKA_DO_SKLONOWANE_REPO/02_exercise/hello_world/* .
   
   git status
   git add PLIK
   git commit -m "init"
   git push
   ```

2. Dodajmy automatyzacje (na podstawie [manuala](https://github.com/wojciech11/se_software_build_automation_tools/blob/master/02_exercise/README.md#continuous-integration-with-github-actions)):

   0. Jeśli nie masz kopi swojego projektu lokalnie, sklonuj go:

      ```bash
      # opcjonalnie:
      mkdir workspace

      git clone ADRES_REPOZYTORIUM_NA_GITHUBIE
      ```

   1. Github oczekuje deklaracji automatyzacji w określonym katalogu:
   
      ```bash
      # jesteś w głównym katalogu projektu
      mkdir -p .github/workflows
      ```

   2. Utwórz plik w `ci.yaml`:

      ```bash
      touch .github/workflows/ci.yaml
      ```

   3. W ci.yaml utwórz pierwszą deklarację pipeline-u:

      ```yaml
      name: Package Project
      
      # Controls when the workflow will run
      on: [ push ]
      
      jobs:
        build:
          runs-on: ubuntu-latest
      
          steps:
            # get the code under $GITHUB_WORKSPACE directory
            - uses: actions/checkout@v2
            # get the python
            - name: Set up Python 3
              uses: actions/setup-python@v3
            # zainstaluj wymagane biblioteki
            - name: Install deps
              run: pip3 install -r requirements.txt
            # dla kazdej zmiany, uruchom testy
            - name: Run tests
              run: PYTHONPATH=. py.test --verbose -s
      ```

   4. Dodaj plik `ci.yaml` to repozytorium githuba (zauważ token musi być utworzony z zaznaczeniem workflow).

   5. Przejdź do zakładki `Actions` w interfejscie webowym githuba na stronie twojego projektu.
