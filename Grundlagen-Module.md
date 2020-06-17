# Grundlagen zu Modulen (in IntelliJ)
Neues Modul in IntelliJ anlegen: 
* Project Reiter
* Rechtsklick auf Projekt (oberste Ebene) -> New -> Module 
* links in der leiste Gradle auswählen, Additional Libraries and Frameworks: Java 
* Namen eingeben und fertig -> Dauert einen Moment, bis IntelliJ die entsprechenden src Folder angelegt hat...

Sobald Modul erstellt, kann ein Package erzeugt werden:
* Project Reiter im entsprechenden Modul
* Rechtsklick auf java ordner -> New -> Package

Die Packages müssen angelegt werden, damit diese dann aus den Modulen exportiert werden können (einzelnen Klassen können nicht exportiert werden).

Außerdem muss für das Modul die **module-info.java** erzeugt werden (sollte dann auf gleicher ebene mit den package(s) liegen: 
* Project Reiter im entsprechenden Modul
* Rechtsklick auf java ordner -> New -> module-info.java

Diese Datei wird benötigt um Abhängigkeiten zwischen Modulen zu definieren.
Grundsätzlicher Aufbau:
```
module [Modulname (ohne Pfad)] {
    ...
}
```
In den geschweiften Klammern kann:
* Ein Package des eigenen Moduls exportiert (= für andere Module sichtbar) gemacht werden `exports [Package (vollständiger Pfad)]; `
* Eine Abhängigkeit zu einem anderen Modul (= importieren) definiert werden `requires [Modulname (ohne Pfad)]`
* 

Jedes Modul kann als eigenständiges (Sub-) Projekt angesehen werden, dementsprechend gibt es auch in jedem Modul einen src ordner (samt main und test) in dem sich der Code befindet. Jedes Module hat auch ein eigenständiges build.gradle file.
Wichtig: Damit das gradle Projekt kompiliert werden kann, müssen dort die richtigen Abhängigkeiten verknüpft werden. Nähere Infos in der "Gradle" Wiki Seite