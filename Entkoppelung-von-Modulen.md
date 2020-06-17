# Entkoppelung von Modulen
Basiert auf folgendem Tutorial: https://www.baeldung.com/java-modules-decoupling-design-strategies

Im Tutorial wurden zwei Entkoppelungsstrategien vorgestellt:
* FactoryClass
* ServiceLoader

Für beide Varianten gibt es einen entsprechenden Branch - dort befinden sich die jeweils lauffähige Programme.

Das Tutorial erklärt auch wie man das ganze unter einem Maven Projekt durchführt, diese Punkte habe ich weggelassen das sie für uns nicht relevant sind. Auch die packages habe ich entsprechend geändert.
## FactoryClass
Die Module werden mittels eigens implementierter Service Provider Factory entkoppelt.
Vorteil: nur 2 Module (service/consumer) nötig
Nachteil: es muss immer eine eigene FactoryClass programmiert werden, welche dem consumer die richtige Implementierung des service zurückgibt.

Deshalb ist die zweite Variante mMn. sinnvoller, auch wenn sie etwas komplexer ist:

## ServiceLoader
Bietet eine "out of the box" Entkoppelung durch entsprechende Konfiguration der div. module-info.java Dateien - d.h. die FactoryClass entfällt.

Die vollständigen module-info.java Dateien befinden sich im ServiceLoader branch, hier ein Auszug der wichtigen Konfiguration:
* ServiceModule:
    * `**exports** [Package, welches Interface beinhaltet]`
* ProviderModule:
    * `**provides** [Interface] **with** [Class welche die Implementierung des Interface enthält];`
* ConsumerModule:
    * `**uses** [Interface];`