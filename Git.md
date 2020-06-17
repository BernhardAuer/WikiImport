### Infos zu .gitignore
Folgende Ordner/Dateien sollten wir nicht ins Repo pushen:

* IDE-spezifische Files (.idea Ordner bei IntelliJ) könnte man teilweise einchecken, bringt uns aber (derzeit) keinen Mehrwert und birgt eine potentielle Fehleranfälligkeit -> also vorerst ins gitignore aufnehmen
* Alle build Ordner (von jedem Modul also -> `build/`)
* .gradle
