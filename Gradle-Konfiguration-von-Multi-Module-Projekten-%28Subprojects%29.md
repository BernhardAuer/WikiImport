# Gradle Konfiguration
Jedes Modul besitzt eine eigene **build.gradle**. Dort werden die Abhängigkeiten zur Kompilierzeit festgelegt. Wird eine Konfiguration vergessen, ist das Programm nicht lauffähig (oder lasst sich erst gar nicht fehlerfrei builden).

Die Abhängigkeiten zu anderen Module sind ja in der **module-info.java** sichtbar - also einfach dort nachschauen, falls man sich nicht sicher ist, ob man etwas vergessen hat.

Im build.gradle des Moduls dann einfach unter dependencies für jedes abhängiges Modul folgendes einfügen (eckige Klammern ersetzen, Doppelpunkt gehört aber dazu!):
```
compile project(':[Modulname (ohne Pfad)]')
```

Auf Root-Ebene gibt es ebenfalls ein build.gradle file. Dort muss unter plugins `id 'application'` eingefügt werden, um den Task "Run" zu erzeugen (evt. Reimport all Gradle Projects nötig). Unter dependencies müssen wieder die abhängigen Module angegeben werden (wie oben beschrieben).

Außerdem muss der Startpunkt der Anwendung definiert werden:
```
application {
    mainModule = '[Modulname (ohne Pfad)]'
    mainClass = '[Klassenname, welche die statische Main-Methode beinhaltet (mit package-pfad)]'
}
```

**Wichtig:** In Gradle scheint es noch einen Bug zu geben (oder ist das gewollt!?), welche es nötig macht folgende Zeilen ebenfalls im root gradle.build file einzufügen:
```
subprojects {
    java {
        modularity.inferModulePath = true

        tasks.withType(JavaCompile) {
            doFirst {
                options.compilerArgs = [
                        '--module-path', classpath.asPath,
                ]
                classpath = files()
            }
        }
    }
}
```

Auf root Ebene gibt es noch ein **settings.gradle** File, welches alle Module angeben muss:
```
include '[Modulname (ohne Pfad)]'

```
Nun sollte gradle build bzw. gradle run funktionieren!

Mehr infos: https://guides.gradle.org/creating-multi-project-builds/