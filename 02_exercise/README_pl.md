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
