﻿# Sonnensystem Simulation (Unreal Engine 5.3.2)

Ein interaktives Sonnensystem-Projekt in der Unreal Engine, konzipiert als praktische Einführung in C++, Spielephysik und grundlegende Engine-Konzepte. 
Dieses Repository dient als Plattform, um durch die Entwicklung eines Orbitalsimulationsprojekts tiefe Einblicke in die Programmierung 
mit der Unreal Engine zu gewinnen und dabei sowohl grundlegende als auch fortgeschrittene Konzepte der Spieleentwicklung zu erforschen.

Hinweis: Das Projekt ist in laufender Entwicklung und kann Änderungen und Aktualisierungen unterliegen.

## Inhaltsverzeichnis

- [Einführung](#einführung)
- [Eigenschaften](#eigenschaften)
- [Erste Schritte](#erste-schritte)
#### Grundlegende Klassen
- [Grundlegende Klassen Implementieren](#grundlegende-klassen-implementieren)
  - [CelestialBody Klasse](#celestialbody-klasse)
    - [Properties](#celestialbody-properties)
    - [Mesh Initialisierung](#mesh-initialisierung)
    - [Getter- und Setter-Funktionen](#getter--und-setter-funktionen)
    - [Physikfunktionen](#physikfunktionen)
    - [Gravitationskonstante / Universe Struktur](#gravitationskonstante)
  - [CelestialBodyRegistry Klasse](#celestialbodyregistry-klasse)
    - [Delegaten](#celestialbodyregistry-delegaten)
    - [Properties](#celestialbodyregistry-properties)
    - [Funktionen](#celestialbodyregistry-funktionen)
  - [Game-Mode Klasse](#game-mode-klasse)
    - [Erweiterung der CelestialBody Klasse](#erweiterung-der-celestialbody-klasse)
  - [OrbitSimulation Klasse](#orbitsimulation-klasse)
    - [Properties](#orbitsimulation-properties)
    - [Funktionen](#orbitsimulation-funktionen)
    - [Erweiterung der Game-Mode Klasse](#erweiterung-der-game-mode-klasse)
#### Simulation erstellen
- [Erstellen der Simulation](#erstellen-der-simulation)
  - [Level erstellen](#level-erstellen)
  - [GameMode hinzufügen](#gamemode-hinzufügen)
  - [Post-Processing-Effekte hinzufügen](#post-processing-effekte-hinzufügen)
  - [Himmelskörper hinzufügen](#die-himmelskörper-hinzufügen)
    - [Basis Blueprint erstellen](#basis-blueprint-erstellen)
    - [Basis Material erstellen](#basis-material-erstellen)
    - [Himmelskörper erstellen](#himmelskörper-erstellen)
      - [Sonne erstellen](#sonne-erstellen)
      - [Erde erstellen](#erde-erstellen)
  - [Simulation starten](#simulation-starten)
    - [Simulation konfigurieren](#simulation-konfigurieren)
#### Orbit Debugger
- [Visualisierung der Orbits](#visualisierung-der-orbits)
  - [Orbit-Debugger erstellen](#orbit-debugger-erstellen)
    - [Virtuelle Himmelskörper Struktur](#virtuelle-himmelskörper-struktur)
    - [Virtuelle Himmelskörper Interface](#virtuelle-himmelskörper-interface)
    - [OrbitDebug Komponente](#orbitdebug-komponente)
    - [OrbitDebug Klasse](#orbitdebug-klasse)
    - [OrbitDebug Properties](#orbitdebug-properties)
    - [OrbitDebug Funktionen](#orbitdebug-funktionen)
  - [Orbit-Debugger verwenden](#orbit-debugger-verwenden)
    - [Orbit-Debugger Blueprint erstellen](#orbit-debugger-blueprint-erstellen)
    - [Orbit-Debugger konfigurieren](#orbit-debugger-konfigurieren)
- [Einsatzmittel](#einsatzmittel)

<a name="einführung"></a>
## Einführung

Das Projekt ermöglicht es, die Kernelemente der Unreal Engine wie Gameplay-Framework, Physik, Benutzeroberflächen und Eingabesteuerung praxisnah zu erlernen.
Durch die Implementierung einer Planetensimulation können Programmierer ihre C++-Fähigkeiten verbessern und ein Verständnis für die Architektur und 
Funktionsweise einer Game Engine entwickeln.

Die schrittweise Anleitung führt von den Grundlagen wie dem Aufsetzen eines Projekts und dem Erstellen von C++-Klassen bis hin zu fortgeschrittenen 
Themen wie Physikberechnungen und prozeduraler Generierung. Dabei werden Best Practices und Konventionen für das Programmieren mit der Unreal Engine vermittelt.

Ziel ist es, anhand eines konkreten Projekts ein tiefgehendes Verständnis für die Unreal-Entwicklung zu erlangen, das auch auf andere Anwendungsbereiche übertragbar ist. 
Das Repository soll als Referenz und Ausgangspunkt für eigene Experimente und Erweiterungen dienen.

Grundlegende C++-Kenntnisse, Verständnis für die Entwicklung von Spielen und die Unreal Engine sind notwendig und erforderlich.
<a name="eigenschaften"></a>
## Eigenschaften

- Implementierung einer interaktiven Sonnensystem-Simulation
- Verwendung von C++ für die Programmierung
- Anwendung von Physik und Mathematik für die Simulation von Himmelskörpern
- Tool zur Visualisierung von Orbits und Planeten
- Anpassungsmöglichkeiten für die Simulation
- Integration von Benutzeroberflächen und Eingabesteuerung
- Performance-Optimierung durch z.B. Task Graphs und Multithreading, Allocator-Optimierung und Burst-Compiler

Hinweis: Die Simulation kann durch die Implementierung weiterer Funktionen und Mechaniken erweitert werden, um das Projekt zu personalisieren und zu verbessern. 
Eventuell wird z.B. mit einem Raumfahrzeug und weiterer Physik erweitert, um eine immersive Erfahrung zu schaffen. Es kann sich in der Entwicklung noch viel ändern und wird dokumentiert.

<a name="erste-schritte"></a>
## Erste Schritte

#### Erstellen eines neuen Projekts in der Unreal Engine 5.3.2

1. Starte Unreal Engine und wähle unter Games "Blank" als Projektvorlage und C++ als Projekt Defaults.
2. Wähle einen Speicherort für das Projekt, wähle einen Namen und klicke auf "Create Project".

#### Erstellen einer neuen C++ Klasse

1. In der Engine klicke auf "Tools" → "New C++ Class".
2. Wähle eine Klasse, die von einer Basisklasse abgeleitet ist, z.B. `AActor` oder `None` für eine leere Klasse, praktisch für Utility-Klassen.
3. Wähle Public oder Private für die Zugriffsebene und wähle einen Namen für die Klasse.
4. Klicke auf "Create Class".
5. Klicke auf "Yes" um die Projektdateien neu zu generieren.
6. Klicke auf "Compile" um die Klasse zu kompilieren.

Hinweis 1: Es ist möglich, eine Klasse direkt in der IDE zu erstellen und sie dann dem Projekt hinzuzufügen. 
Es bietet sich auch an eine übersichtliche Ordnerstruktur zu erstellen, um die Klassen zu organisieren.
Die Klasse müssen in einem passenden Ordner abgelegt werden, z.B. `MyGame/Games/MyGame/Source/MyGameClasses` bzw. `MyGame/Source/MyGameClasses`.

Hinweis 2: Die Engine generiert automatisch die Header- und Quelldateien für die neue Klasse und fügt sie dem Projekt hinzu.
Das Kompilieren der Klasse erstellt die Binärdateien und macht die Klasse im Editor verfügbar. In Unreal ist es wichtig, die Klasse nach jeder Änderung neu zu kompilieren.

------------------------------------------------------------------------------------------------------------

<a name="grundlegende-klassen-implementieren"></a>
## Grundlegende Klassen Implementieren

<a name="celestialbody-klasse"></a>
#### CelestialBody Klasse

Als Erstes erstellen wir die Klasse, die als Grundlage für alle Himmelskörper im Sonnensystem dienen wird.
Dazu erstellen wir eine neue C++ Klasse, die von `AActor` abgeleitet ist und fügen die notwendigen Properties und Funktionen hinzu.

Die Header-Datei `CelestialBody.h` sollte wie folgt aussehen:

```cpp
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CelestialBody.generated.h"

UCLASS()
class SOLARSYSTEM_API ACelestialBody : public AActor
{
	GENERATED_BODY()

public:
	ACelestialBody();

protected:
	virtual void BeginPlay() override;
};
```

Um die Quelldatei `CelestialBody.cpp` kümmern wir uns später.


<a name="celestialbody-properties"></a>
##### *CelestialBody Properties:*

Jetzt fügen wir erstmal die Properties hinzu, um die Himmelskörper zu definieren.

Wir benötigen folgende Properties:
- Masse
- Radius
- Initialgeschwindigkeit
- Aktuelle Geschwindigkeit und 
- Linien Farbe für die Orbit-Visualisierung

Die Properties für die Himmelskörper sollten folgendermaßen aussehen:

```cpp
protected:
	virtual void BeginPlay() override;

	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Celestial Body")
	float Mass;

	UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Celestial Body")
	float Radius;

	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Celestial Body")
	FVector InitialVelocity;

	UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Celestial Body")
	FVector CurrentVelocity;
	
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Debug Options")
	mutable FLinearColor LineColor;
```

Die Masse und die Initialgeschwindigkeit sind im Blueprint editierbar, damit wir die Himmelskörper im Editor konfigurieren können.
Die aktuelle Geschwindigkeit ist nur lesbar, da sie sich während der Simulation ändert.
Der Radius ist nur lesbar, da er sich aus der Größe der Mesh-Komponente ergibt.

Die Linienfarbe ist im Blueprint editierbar, um die Orbits zu visualisieren.
Außerdem ist sie mutable, damit sie in einer const-Funktion geändert werden kann.

Außerdem brauchen wir noch eine Mesh-Komponente, um den Himmelskörper im Editor sichtbar zu machen und die Physiksimulation zu ermöglichen, 
in dem wir die Mesh-Komponenten Masse setzen und den Radius der Komponente bekommen.

Die Properties für die Mesh-Komponente sollten folgendermaßen aussehen:

```cpp
protected:
    virtual void BeginPlay() override;

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Celestial Body")
    UStaticMeshComponent* MeshComponent;
```


<a name="mesh-initialisierung"></a>
##### *Mesh Initialisierung:*

Die Mesh-Komponente wird im Konstruktor initialisiert.

Die Konstruktor-Implementierung sollte in der Quelldatei `CelestialBody.cpp` wie folgt aussehen:

```cpp
#include "CelestialBody.h"


ACelestialBody::ACelestialBody()
{
        PrimaryActorTick.bCanEverTick = true;

        MeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("MeshComponent"));
	RootComponent = MeshComponent;
	MeshComponent->SetSimulatePhysics(true);
	MeshComponent->SetEnableGravity(false);
}
```

Der Konstruktor initialisiert die Mesh-Komponente und setzt die Physiksimulation und die Gravitationseinstellungen.
Wir setzen die Physiksimulation auf `true`, damit die Komponente Physiksimulationen durchführt.
Wir setzen die Gravitationseinstellungen auf `false`, da wir unsere eigene Gravitationssimulation implementieren werden.

<a name="getter-und-setter-funktionen"></a>
##### *Getter- und Setter-Funktionen:*

Um auf die Properties der Himmelskörper zuzugreifen und sie zu ändern, erstellen wir Getter- und Setter-Funktionen.

Die Getter- und Setter-Funktionen sollten folgendermaßen aussehen:

```cpp
public:
	float GetMass() const { return Mass; }
	void SetMass(const float& NewMass);

	float GetRadius() const { return Radius; }
	void SetRadius() { Radius = MeshComponent->Bounds.SphereRadius; }

	FVector GetInitialVelocity() const { return InitialVelocity; }
	void SetCurrentVelocity(const FVector& NewVelocity) { CurrentVelocity = NewVelocity; }
```

Bis auf die Funktion `SetMass` sind alle Funktionen inline definiert, da sie nur eine einfache Rückgabe oder Zuweisung durchführen.
Die Funktion `SetRadius` setzt den Radius des Himmelskörpers auf den Radius der Mesh-Komponente, um die Größe des Himmelskörpers zu bestimmen, 
welcher über die größe der Mesh-Komponente definiert wird.

Die Funktion `SetMass` sollte in der Quelldatei `CelestialBody.cpp` wie folgt aussehen:

```cpp
void ACelestialBody::SetMass(const float& NewMass)
{
	Mass = NewMass;
	MeshComponent->SetMassOverrideInKg(NAME_None, Mass, true);
}
```

Die Funktion `SetMass` setzt die Masse des Himmelskörpers und überschreibt die Masse der Mesh-Komponente, um die Masse des Himmelskörpers zu setzen.


<a name="physikfunktionen"></a>
##### *Physikfunktionen:*

Um die Physiksimulation zu implementieren, erstellen wir Funktionen, die die Gravitationssimulation und die Bewegung der Himmelskörper berechnen.

Die Funktionen sollten in der Header-Datei `CelestialBody.h` wie folgt aussehen:

```cpp
public:
	void UpdatePosition(const float& TimeStep) const;
	void UpdateVelocity(const FVector& Acceleration, const float& TimeStep);
	
private:
	void MassCalculation();
```

Die Implementierung der Funktionen sollte in der Quelldatei `CelestialBody.cpp` wie folgt aussehen:

```cpp
void ACelestialBody::UpdateVelocity(const FVector& Acceleration, const float& TimeStep)
{
	CurrentVelocity += Acceleration * TimeStep;
}

void ACelestialBody::UpdatePosition(const float& TimeStep) const
{
	MeshComponent->SetPhysicsLinearVelocity(CurrentVelocity * TimeStep);
}

void ACelestialBody::MassCalculation()
{
	Mass = Radius * Radius / FUniverse::GravitationalConstant;
	MeshComponent->SetMassOverrideInKg(NAME_None, Mass, true);
}
```

Die Funktion `UpdateVelocity` berechnet die Geschwindigkeit des Himmelskörpers basierend auf der Beschleunigung und dem Zeitintervall.

Die Funktion `UpdatePosition` aktualisiert die Position des Himmelskörpers basierend auf der aktuellen Geschwindigkeit und dem Zeitintervall.
Die Geschwindigkeit wird mit dem Zeitintervall multipliziert, um die Position des Himmelskörpers zu aktualisieren und die Bewegung über die Mesh-Komponente zu steuern.

Die Funktion `MassCalculation` berechnet die Masse des Himmelskörpers basierend auf den `Radius` und der Gravitationskonstante<sup>*</sup> `G`.
Die Formel für die Masse-Berechnung lautet:
`m = r² * G` oder `Masse = Radius * Radius * G`.
Das Ergebnis wird in der Masse-Property gespeichert und die Masse der Mesh-Komponente überschrieben.

Jetzt setzten wir in der Funktion `BeginPlay` die aktuelle Geschwindigkeit und den Radius und berechnen die Masse des Himmelskörpers.
Da die Werte im Editor gesetzt werden können, müssen die Funktionen in der `BeginPlay` Funktion aufgerufen werden und nicht im Konstruktor, 
da sonst die Werte nicht richtig übernommen werden.

Die Implementierung der Funktionen sollte in der Quelldatei `CelestialBody.cpp` wie folgt aussehen:

```cpp
ACelestialBody::ACelestialBody()
{
    PrimaryActorTick.bCanEverTick = true;

    MeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("MeshComponent"));
    RootComponent = MeshComponent;
    MeshComponent->SetSimulatePhysics(true);
    MeshComponent->SetEnableGravity(false);
}

void ACelestialBody::BeginPlay()
{
    Super::BeginPlay();
 
    SetCurrentVelocity(InitialVelocity);
    SetRadius();
    MassCalculation();
}
```

------------------------------------------------------------------------------------------------------------

<a name="gravitationskonstante"></a>
#### Gravitationskonstante

<sup>*</sup> Die Gravitationskonstante `G` und die Struktur `FUniverse` definieren wir in der neu erstellten Header-Datei `Universe.h`.

Die Header-Datei `Universe.h` sollte wie folgt aussehen:

```cpp
#pragma once

#include "CoreMinimal.h"

struct FUniverse
{
	static constexpr float GravitationalConstant = 0.1f; // 6.67430e-11f | m^3 kg^-1 s^-2
	static constexpr float TimeStep = 0.1f;
};
```

Die Gravitationskonstante und Zeitschrittgröße wird als `constexpr` definiert, um sie zur Kompilierzeit zu berechnen und als Konstante zu verwenden.

Die Gravitationskonstante wird als `0.1f` definiert, um die Simulation zu vereinfachen und die Werte zu skalieren.

Für die Simulation verwenden wir eine feste Zeitschrittgröße von `0.1f`, um die Simulation zu steuern und die Orbits zu berechnen.


------------------------------------------------------------------------------------------------------------

<a name="celestialbodyregistry-klasse"></a>
#### CelestialBodyRegistry Klasse

Als Nächstes erstellen wir die Klasse, die die Himmelskörper registriert und verwaltet, um sie in der Simulation zu verwenden.
Dazu erstellen wir eine neue C++ Klasse, die von `AActor` abgeleitet ist und fügen die notwendigen Properties und Funktionen hinzu.

Die Header-Datei `CelestialBodyRegistry.h` sollte wie folgt aussehen:

```cpp
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "ACelestialBodyRegistry.generated.h"

UCLASS()
class SOLARSYSTEM_API ACelestialBodyRegistry : public AActor
{
	GENERATED_BODY()

public:
	ACelestialBodyRegistry();
};
```

<a name="celestialbodyregistry-delegaten"></a>
##### *CelestialBodyRegistry Delegaten:*

Der Delegat `FCelestialObjectAddedDelegate` wird definiert, um das Hinzufügen von Himmelskörpern zu ermöglichen.

Die Delegaten-Definition sollte in der Header-Datei `CelestialBodyRegistry.h` direkt über der Klassendefinition wie folgt aussehen:

```cpp
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FCelestialObjectAddedDelegate, ACelestialBody*, CelestialObject);

UCLASS()
class SOLARSYSTEM_API ACelestialBodyRegistry : public AActor
{
	GENERATED_BODY()

public:
	ACelestialBodyRegistry();
	
	UPROPERTY(BlueprintAssignable)
	FCelestialObjectAddedDelegate OnCelestialBodyAdded;
};
```

Die Implementierung des Delegaten sollte in der Quelldatei bzw. Konstruktor `CelestialBodyRegistry.cpp` wie folgt aussehen:

```cpp
#include "ACelestialBodyRegistry.h"


ACelestialBodyRegistry::ACelestialBodyRegistry()
{
	OnCelestialBodyAdded.AddDynamic(this, &ACelestialBodyRegistry::AddCelestialObject);
}
```

Der Delegat `OnCelestialBodyAdded` ist im Blueprint zugänglich und wird im Konstruktor initialisiert, um das Hinzufügen von Himmelskörpern zu ermöglichen.
Wir können den Delegaten verwenden, um Himmelskörper in einer anderen Klasse zu registrieren und zu verwalten.

<a name="celestialbodyregistry-properties"></a>
##### *CelestialBodyRegistry Properties:*

Jetzt fügen wir erstmal die Properties hinzu, um die Himmelskörper zu registrieren.

- Delegaten für das Hinzufügen von Himmelskörpern (siehe oben)
- Array für die Himmelskörper

Die Properties für die Himmelskörper-Registry sollten folgendermaßen aussehen:

```cpp
public:
	ACelestialBodyRegistry();

	UPROPERTY(BlueprintAssignable)
	FCelestialObjectAddedDelegate OnCelestialBodyAdded;

protected:
	UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Celestial Objects")
	TArray<ACelestialBody*> CelestialBodies;
```

Das Array `CelestialBodies` ist nur lesbar und enthält alle registrierten Himmelskörper.

Damit wir die ACelestialBody-Pointer verwenden können, müssen wir die `CelestialBody.h` inkludieren.

Die Include-Direktive sollte in der Quelldatei `CelestialBodyRegistry.h` (evtl. mit Ordnerstruktur) wie folgt aussehen:

```cpp
#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CelestialBody.h"
#include "ACelestialBodyRegistry.generated.h"
```

<a name="celestialbodyregistry-functionen"></a>
##### *CelestialBodyRegistry Funktionen:*

Jetzt fügen wir die Funktionen hinzu, um die Himmelskörper zu registrieren und zu verwalten.

Die Funktionen sollten folgendermaßen aussehen:

```cpp
public:
	UFUNCTION()
	void AddCelestialObject(ACelestialBody* CelestialObject);
	
	void RemoveCelestialObject(ACelestialBody* CelestialObject);
	
	TArray<ACelestialBody*> GetCelestialObjects() const { return CelestialBodies; }
```

Die Getter-Funktion `GetCelestialObjects` ist `inline` und gibt das Array der Himmelskörper zurück, damit wir auf die Himmelskörper zugreifen können.

Die Implementierung der anderen Funktionen sollte in der Quelldatei `CelestialBodyRegistry.cpp` wie folgt aussehen:

```cpp
#include "ACelestialBodyRegistry.h"


ACelestialBodyRegistry::ACelestialBodyRegistry()
{
	OnCelestialBodyAdded.AddDynamic(this, &ACelestialBodyRegistry::AddCelestialObject);
}

void ACelestialBodyRegistry::AddCelestialObject(ACelestialBody* CelestialObject)
{
	if (CelestialObject && !CelestialBodies.Contains(CelestialObject))
	{
		CelestialBodies.Add(CelestialObject);
	}
}

void ACelestialBodyRegistry::RemoveCelestialObject(ACelestialBody* CelestialObject)
{
	if (CelestialBodies.Contains(CelestialObject))
	{
		CelestialBodies.Remove(CelestialObject);
	}
}
```

In der Funktion `AddCelestialObject` wird der Himmelskörper hinzugefügt, wenn er nicht `nullptr` ist und noch nicht im Array enthalten ist.

In der Funktion `RemoveCelestialObject` wird der Himmelskörper entfernt, wenn er im Array enthalten ist.

------------------------------------------------------------------------------------------------------------

<a name="game-mode-klasse"></a>
#### Game-Mode Klasse

Um die Klassen zu erweitern, müssen wir erstmal eine GameMode-Klasse erstellen, in dem wir die Simulation steuern und die Himmelskörper registrieren und verwalten.
In der GameMode-Klasse initialisieren wir die Simulation und fügen die Himmelskörper hinzu, um die Orbits zu berechnen und die Simulation zu steuern.

Dazu erstellen wir eine neue C++ Klasse, die von `AGameModeBase` abgeleitet ist und fügen die notwendigen Properties und Funktionen hinzu.

Die Header-Datei `OrbitSimulation_GameMode.h` sollte wie folgt aussehen:

```cpp
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/GameModeBase.h"
#include "ACelestialBodyRegistry.h"
#include "OrbitSimulation_GameMode.generated.h"

/**
 * 
 */
UCLASS()
class SOLARSYSTEM_API ADemoOrbitSimulation_GameMode : public AGameModeBase
{
	GENERATED_BODY()

protected:

	UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Celestial Objects")
	ACelestialBodyRegistry* CelestialBodyRegistry;


public:
	virtual void StartPlay() override;
	
	ACelestialBodyRegistry* GetCelestialBodyRegistry() const { return CelestialBodyRegistry; }

	
private:
	void Initialize();
	
};
```

Wir haben die `CelestialBodyRegistry`-Property, eine `inline` Getter-Funktion für die Registry und die Funktion `Initialize`, um die Simulation zu initialisieren, hinzugefügt.

Die Implementierung der Funktion sollte in der Quelldatei `OrbitSimulation_GameMode.cpp` wie folgt aussehen:

```cpp
#include "OrbitSimulation_GameMode.h"


void AOrbitSimulation_GameMode::StartPlay()
{
	Super::StartPlay();
	
	Initialize();
}

void AOrbitSimulation_GameMode::Initialize()
{
	UWorld* World = GetWorld();
	if (World)
	{
		CelestialBodyRegistry = World->SpawnActor<ACelestialBodyRegistry>();
		if (!CelestialBodyRegistry)
		{
			UE_LOG(LogTemp, Error, TEXT("Failed to create CelestialObjectManager!")
		}
		else
		{
		    UE_LOG(LogTemp, Display, TEXT("Created CelestialObjectManager!")
		}
	}
}
```

Die Funktion `StartPlay` ruft die `Initialize`-Funktion auf, um die Simulation zu starten.

Die Funktion `Initialize` erstellt die `CelestialBodyRegistry` und gibt eine Meldung aus, wenn die Registry erfolgreich erstellt wurde oder einen Fehler, wenn die Registry nicht erstellt werden konnte.

Jetzt können wir die GameMode-Klasse verwenden, um die Simulation zu steuern und die Himmelskörper zu registrieren und zu verwalten.

------------------------------------------------------------------------------------------------------------

<a name="erweiterung-celestialbody-klasse"></a>
#### Erweiterung der CelestialBody Klasse

Um die Himmelskörper in der Simulation zu verwenden, müssen wir die `CelestialBody`-Klasse erweitern, um die Registrierung und Verwaltung der Himmelskörper zu ermöglichen.

Dazu fügen wir eine Funktion hinzu, um die Himmelskörper zu registrieren und zu verwalten.

Die Funktion sollte in der Header-Datei `CelestialBody.h` und in der Quelldatei `CelestialBody.cpp` wie folgt implementiert werden:

```cpp
	void AddObjectToRegistry();
```

Die Implementierung der Funktion sollte in der Quelldatei `CelestialBody.cpp` wie folgt aussehen:

```cpp
  void ACelestialBody::AddBodyToRegistry()
{
	ADemoOrbitSimulation_GameMode* GameMode = Cast<ADemoOrbitSimulation_GameMode>(GetWorld()->GetAuthGameMode());
	if (GameMode)
	{
		ACelestialBodyRegistry* Registry = GameMode->GetCelestialBodyRegistry();
		if (Registry)
		{
			Registry->OnCelestialBodyAdded.Broadcast(this);
		}
		else
		{
			UE_LOG(LogTemp, Error, TEXT("Failed to get CelestialObjectManager from Game Mode!);
		}
	}
	else
	{
		UE_LOG(LogTemp, Error, TEXT("Failed to cast Game Mode!);
	}
}
```

Die Funktion `AddBodyToRegistry` ruft den GameMode auf, um die `CelestialBodyRegistry` zu erhalten und den Himmelskörper hinzuzufügen, indem der Delegat `OnCelestialBodyAdded` aufgerufen wird.

Dadurch wird der Himmelskörper zur Registry hinzugefügt und kann in der Simulation verwendet werden.

Dafür müssen wir noch die Funktion `AddBodyToRegistry` in der `BeginPlay` Funktion der `CelestialBody`-Klasse aufrufen.

Die Implementierung der Funktion sollte in der Quelldatei `CelestialBody.cpp` wie folgt aussehen:

```cpp
void ACelestialBody::BeginPlay()
{
    Super::BeginPlay();
    
    SetCurrentVelocity(InitialVelocity);
    MassCalculation();
    
    FTimerHandle TimerHandle;
	GetWorldTimerManager().SetTimer(TimerHandle, this, &ACelestialBody::AddBodyToRegistry, 0.5f, false);
}
```

Die Funktion `AddBodyToRegistry` wird nach einer Verzögerung von 0,5 Sekunden aufgerufen, um sicherzustellen, dass die Registry bereit ist, den Himmelskörper zu registrieren.

Jetzt können wir die Himmelskörper in der Simulation verwenden und die Orbits berechnen.

------------------------------------------------------------------------------------------------------------

<a name="orbitsimulation-klasse"></a>
##### OrbitSimulation Klasse

Als Nächstes erstellen wir die Klasse, die die Simulation der Himmelskörper und die Berechnung der Orbits durchführt.
Dazu erstellen wir eine neue C++ Klasse, die von `AActor` abgeleitet ist und fügen die notwendigen Properties und Funktionen hinzu.

Die Header-Datei `OrbitSimulation.h` sollte wie folgt aussehen:

```cpp
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "OrbitSimulation.generated.h"

UCLASS()
class SOLARSYSTEM_API AOrbitSimulation : public AActor
{
	GENERATED_BODY()

public:
	AOrbitSimulation();

protected:
	virtual void BeginPlay() override;
	virtual void Tick(float DeltaTime) override;
};
```

Um die Quelldatei `OrbitSimulation.cpp` kümmern wir uns später.

<a name="orbit-simulation-properties"></a>
##### *OrbitSimulation Properties:*

Jetzt fügen wir erstmal die Properties hinzu, um die Simulation zu definieren.

Wir benötigen folgende Properties:

- Bool für das Einschalten der manuellen Zeitskala (für das Umstellen der Zeitskala (Start, Stop, Beschleunigen))
- Zeitskala

Die Properties für die Simulation sollten folgendermaßen aussehen:

```cpp
protected:
	virtual void BeginPlay() override;
	virtual void Tick(float DeltaTime) override;

	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Physics")
	bool bManualTimeScale;

	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Physics")
	float TimeScale;
	
	UPROPERTY()
	ACelestialBodyRegistry* CelestialBodyRegistry;

```

Die Zeitskala Bool ist im Blueprint editierbar, damit wir die Simulation starten, stoppen und beschleunigen können.

Die Zeitskala ist im Blueprint editierbar, damit wir die Simulation beschleunigen oder verlangsamen können.

Die `CelestialBodyRegistry`-Property wird verwendet, um die Himmelskörper zu registrieren und zu verwalten.

<a name="orbit-simulation-functions"></a>
##### *OrbitSimulation Funktionen:*

Jetzt fügen wir die Funktionen hinzu, um die Simulation zu steuern und die Orbits zu berechnen.

Die Funktionen in der Header-Datei `OrbitSimulation.h` sollten folgendermaßen aussehen:

```cpp
private:

	void UpdateAllObjects(const float& TimeStep) const;
	void UpdateAllPositions(const float& TimeStep) const;
	void UpdateAllVelocities(const float& TimeStep) const;

	FVector CalculateGravitationalAcceleration(const FVector& OtherPosition, const ACelestialBody* Object) const;
	
	void GetCelestialObjectRegistry();
```

Die Implementierung der Update-Funktionen sollte in der Quelldatei `OrbitSimulation.cpp` wie folgt aussehen:

```cpp
void AOrbitSimulation::UpdateAllObjects(const float& TimeStep) const
{
	if (CelestialBodyRegistry)
	{
		UpdateAllPositions(TimeStep);
		UpdateAllVelocities(TimeStep);
	}
	else
	{
		UE_LOG(LogTemp, error, TEXT("CelestialObjectManager is nullptr! In Orbit Simulation!");
	}
	
}

void AOrbitSimulation::UpdateAllPositions(const float& TimeStep) const
{
	for (const auto& Body : CelestialBodyRegistry->GetCelestialObjects())
	{
		Body->UpdatePosition(TimeStep);
	}
}

void AOrbitSimulation::UpdateAllVelocities(const float& TimeStep) const
{
	for (const auto& Body : CelestialBodyRegistry->GetCelestialObjects())
	{
		FVector Acceleration = CalculateGravitationalAcceleration(Body->GetActorLocation(), Body);
		Body->UpdateVelocity(Acceleration, TimeStep);
	}
}
```

Die Funktion `UpdateAllObjects` ruft die Update-Funktionen für die Positionen und Geschwindigkeiten der Himmelskörper auf.

Die Funktion `UpdateAllPositions` aktualisiert die Positionen der Himmelskörper basierend auf der aktuellen Geschwindigkeit und dem Zeitintervall.

Die Funktion `UpdateAllVelocities` aktualisiert die Geschwindigkeiten der Himmelskörper basierend auf der Gravitationsbeschleunigung und dem Zeitintervall.

Die Implementierung der Funktion `CalculateGravitationalAcceleration` sollte in der Quelldatei `OrbitSimulation.cpp` wie folgt aussehen:

```cpp
FVector AOrbitSimulation::CalculateGravitationalAcceleration(const FVector& OtherPosition, const ACelestialBody* Object) const
{
    // g = G * M / r^2 | Gravitational acceleration

	FVector Acceleration = FVector::ZeroVector;
	for (const auto& Obj : CelestialBodyRegistry->GetCelestialObjects())
	{
		if (Obj == Object) continue;

		// Gravitational constant G
		const float G = FUniverse::GravitationalConstant;
		// Mass of the sample object m
		const float M = Obj->GetMass();
		// Distance between two objects r = |r1 - r2| r = R
		FVector R = Obj->GetActorLocation() - OtherPosition;
		// Distance squared
		const float SqrR = R.SizeSquared();
		// Direction of the force
		FVector ForceDir = R.GetSafeNormal();

		Acceleration += ForceDir * G * M / SqrR;
	}
	
	return Acceleration;
}
```

Die Funktion `CalculateGravitationalAcceleration` berechnet die Gravitationsbeschleunigung basierend auf der Gravitationskonstante, der Masse und der Position der Himmelskörper.
Dazu wird die Gravitationskonstante `G`, die Masse `M`, die Distanz `R` und die Distanzquadrate `SqrR` berechnet, um die Gravitationsbeschleunigung zu bestimmen.

Die Gravitationsbeschleunigung wird für jeden Himmelskörper berechnet und aufsummiert, um die Gesamtbeschleunigung zu erhalten.

Als Nächstes fügen wir die Funktion `GetCelestialBodyRegistry` hinzu, um die `CelestialBodyRegistry` zu erhalten und zu initialisieren.

Die Implementierung der Funktion sollte in der Quelldatei `OrbitSimulation.cpp` wie folgt aussehen:

```cpp
void AOrbitSimulation::GetCelestialBodyRegistry()
{
	AOrbitSimulation_GameMode* GameMode = Cast<AOrbitSimulation_GameMode>(GetWorld()->GetAuthGameMode());
	if (GameMode)
	{
		CelestialBodyRegistry = GameMode->GetCelestialBodyRegistry();
		if (!CelestialBodyRegistry)
		{
			UE_LOG(LogTemp, Display, TEXT("Something went wrong! Failed to create CelestialBodyRegistry! In Orbit Simulation!")
		}
	}
	else
	{
		UE_LOG(LogTemp, error, TEXT("Failed to cast Game Mode! In Orbit Simulation!")
	}
}
```

Die Funktion `GetCelestialObjectManager` ruft den GameMode auf, um die `CelestialBodyRegistry` zu erhalten und zu initialisieren.

Die Funktion wird in der `BeginPlay` aufgerufen, um die Registry zu initialisieren.

Die Implementierung der Funktion sollte in der Quelldatei `OrbitSimulation.cpp` wie folgt aussehen:

```cpp
void AOrbitSimulation::BeginPlay()
{
    Super::BeginPlay();
    
    GetCelestialObjectRegistry();
}
```

Als Letztes fügen wir die Funktion `Tick` hinzu, um die Simulation zu steuern und die Orbits zu berechnen.

Die Implementierung der Funktion sollte in der Quelldatei `OrbitSimulation.cpp` wie folgt aussehen:

```cpp
void AOrbitSimulation::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);
	
	DeltaTime = FUniverse::TimeStep;
	const float ScaledDeltaTime = bManualTimeScale ? DeltaTime * TimeScale : DeltaTime;
	UpdateAllObjects(ScaledDeltaTime);
}
```

Die Konstante `FUniverse::TimeStep` wird als Zeitintervall für die Simulation verwendet und kann angepasst werden, um die Simulation zu steuern.

Durch das Setzten der skalierbaren DeltaTime kann die Simulation gesteuert werden, um die Geschwindigkeit der Simulation zu erhöhen oder zu verringern.

Jetzt können wir die Orbits der Himmelskörper berechnen und daraus eine Simulation erstellen.

------------------------------------------------------------------------------------------------------------

<a name="erweiterung-der-game-mode-klasse"></a>
#### Erweiterung der Game-Mode Klasse

Um die Simulation zu starten und die Himmelskörper zu registrieren und zu verwalten, müssen wir die GameMode-Klasse erweitern.

Die Implementierung der Funktion sollte in der Quelldatei `OrbitSimulation_GameMode.cpp` wie folgt aussehen:

```cpp
void AOrbitSimulation_GameMode::Initialize()
{
	UWorld* World = GetWorld();
	if (World)
	{
		CelestialBodyRegistry = World->SpawnActor<ACelestialBodyRegistry>();
		if (!CelestialBodyRegistry)
		{
			UE_LOG(LogTemp, error, TEXT("Failed to create CelestialBodyRegistry! (OrbitSimulation_GameMode)")
		}
		else
		{
			UE_LOG(LogTemp, display, TEXT("Created CelestialBodyRegistry! (OrbitSimulation_GameMode)")
		}
		OrbitSimulation = World->SpawnActor<AOrbitSimulation>();
		if (!OrbitSimulation)
		{
			UE_LOG(LogTemp, error, TEXT("Failed to create OrbitSimulation! (OrbitSimulation_GameMode)")
		}
		else
		{
			UE_LOG(LogTemp, display, TEXT("Created OrbitSimulation! (OrbitSimulation_GameMode)")
		}
	}
}
```

Wir fügen die `OrbitSimulation`-Property hinzu, um die Simulation zu steuern und die Orbits zu berechnen.

------------------------------------------------------------------------------------------------------------

<a name="erstellen-der-simulation"></a>
## Erstellen der Simulation

<a name="level-erstellen"></a>
#### Level erstellen:

In der Engine im Content Browser erstellen wir einen Ordner `Maps`.
In dem Ordner erstellen wir eine neue Level-Datei, z.B. `SolarSystemSimulation`, in dem wir mit Rechtsklick auf den Ordner `Maps` und dann auf `Level` klicken.

![Level erstellen](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/create-level.png)

<a name = "gamemode-hinzufügen"></a>
##### *GameMode hinzufügen:*

Den GameMode können wir in den World Settings des Levels setzen, um die Simulation zu starten und die Himmelskörper zu registrieren und zu verwalten.

![GameMode hinzufügen](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/add-game-mode.png)


<a name = "post-processing-effekte-hinzufügen"></a>
##### *Post-Processing Effekte hinzufügen:*

Um die Szene zu verbessern, fügen wir Post-Processing Effekte hinzu, um die Beleuchtung und die Atmosphäre zu verbessern.

Dazu erstellen wir ein neues Post-Processing Volume, indem wir über das Plus-Symbol im Editor über `Volume` und dann `Post-Processing Volume` klicken.
Das Volume wird automatisch in die Szene hinzugefügt und wir können die Einstellungen im Details Panel konfigurieren.

![Post-Processing Volume hinzufügen](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/add-ppv.png)

Zwei wichtige Einstellungen sind `Unbound` bzw. `Infinite Extent`, da setzen wir den Haken, damit das Volume in der ganzen Szene wirkt.

![Post-Processing Volume konfigurieren 1](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/ppv-unbound.png)

Unter Exposure die Auto-Exposure `Min EV100` und `Max EV100` auf `0` setzen.

![Post-Processing Volume konfigurieren 2](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/ppv-auto-exposure.png)

Die eingestellte Auto-Exposure sorgt dafür, dass die Helligkeit in jeder Szenerie gleich bleibt.


<a name = "die-himmelskoerper-hinzufügen"></a>
### Die Himmelskörper hinzufügen

Um die Himmelskörper in der Simulation zu verwenden, brauchen wir ein Basis-Blueprint und Material für die Himmelskörper.

<a name = "basis-blueprint-erstellen"></a>
##### *Basis Blueprint erstellen:*

Erstellen wir ein Basis-Blueprint für die Himmelskörper, indem wir mit Rechtsklick auf den Ordner `Blueprints` den wir vorher erstellen und dann auf `Blueprint Class` klicken.

![Basis Blueprint erstellen](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/bp-base1.png)

Wir suchen nach `CelestialBody` und wählen die Klasse als Parent Class aus.
Wir benennen die Klasse z.B. `BP_CelestialBodyBase`.

![Suche CelestialBody](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/bp-base2.png)

Als Static Mesh für die Himmelskörper verwenden wir eine Sphere, die wir im Editor erstellen und als Static Mesh für den Himmelskörper setzen.
Im Details Panel unter Physics aktivieren wir `Simulate Physics` und `Mass (kg)`, die Masse wird automatisch beim Start der Simulation berechnet.
Zuletzt deaktivieren wir `Enable Gravity` da wir unsere eigene Gravitationssimulation verwenden.

![Basis Blueprint konfigurieren](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/bp-base3.png)

So müssen wir nicht für jeden Himmelskörper ein neues Blueprint erstellen, sondern können das Basis Blueprint verwenden und die Eigenschaften im Editor konfigurieren.

<a name = "basis-material-erstellen"></a>
##### *Basis Material erstellen:*

Erstellen wir ein Basis-Material für die Himmelskörper, indem wir mit Rechtsklick auf den Ordner `Materials` den wir vorher erstellen und dann auf `Material` klicken.
Wir benennen das Material z.B. `M_CelestialBodySurfaceBase`.

![Basis Material erstellen](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/m-base1.png)

Dem Material fügen wir drei Parameter als absolute Basis hinzu:
- `Base Color`
- `Metallic`
- `Roughness`

![Basis Material konfigurieren](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/m-base2.png)

Das Material wird als Basis für die Himmelskörper verwendet und kann als Instanz für die Himmelskörper im Editor konfiguriert werden.

Hinweis: Es können später auch weitere Parameter hinzugefügt bzw. getauscht werden, um die Oberfläche der Himmelskörper zu konfigurieren und Texturen hinzuzufügen.

<a name = "himmelskoerper-erstellen"></a>
#### *Himmelskörper erstellen:*

Erstellen wir die Himmelskörper im Editor, indem wir das Basis-Blueprint und das Basis-Material verwenden.
Wir brauchen mindestens zwei Himmelskörper, um die Simulation zu starten und die Orbits zu berechnen.

<a name = "sonne-erstellen"></a>
##### *Sonne erstellen:*

Fangen wir mit der Sonne an, indem wir ein neues Blueprint erstellen und das Basis-Blueprint verwenden.
Dazu erstellen wir ein neues Blueprint, indem wir mit Rechtsklick auf den Ordner `Blueprints` und dann auf `Blueprint Class` klicken.
Wir suchen nach `BP_CelestialBodyBase` und wählen die Klasse als Parent Class aus.

![Sonne Blueprint erstellen](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/bp-sun1.png)

Wir benennen das Blueprint z.B. `BP_Sun`.

Für die Sonne brauchen wir noch ein anderes Material, das wir im Editor erstellen und als Material für die Sonne setzen.
Wir benennen das Material z.B. `M_SunSurface`.

Das Material braucht nur ein Parameter: 
- `Emissive Color`.

![Sonne Material erstellen](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/m-sun1.png)

Die Farbe kann nach Belieben eingestellt werden, sollte aber den V-Wert vom HSV-Farbraum auf 10 setzen, damit die Sonne leuchtet.
Außerdem erstellen wir noch eine Instanz des Materials, um die Farbe im Editor zu konfigurieren.
Wir benennen die Instanz z.B. `MI_SunSurface` oder `MI_SunSurface_Inst`.

Die Instanz erstellen wir, indem wir mit Rechtsklick auf das Basis-Material und dann auf `Create Material Instance` klicken.

![Sonne Material Instanz erstellen](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/m-sun2.png)
![Sonne Material Instanz](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/m-sun3.png)
![Sonne Material Instanz konfigurieren](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/m-sun4.png)

Die Skalierung des Meshes setzten wir auf `284,84`, als Material die Instanz von dem gerade erstellten Material.

![Sonne konfigurieren 1](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/bp-sun2.png)

Die Masse (Wichtig: in den Celestial Body und nicht in den Physics Einstellungen) auf `332.946.000` 
und die Initialgeschwindigkeit auf `0`.

Für die Sonne setzen wir die Linienfarbe auf `FLinearColor(1, 1, 0, 1)` um die Orbits zu visualisieren.

![Sonne konfigurieren 2](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/bp-sun3.png)

Zum Schluss platziere die Sonne im Editor, in dem wir sie in die Szene ziehen und die Position im Details Panel auf `0, 0, 0` setzen.
So ist die Sonne im Zentrum der Szene und die Orbits der Himmelskörper werden um die Sonne berechnet.

<a name = "erde-erstellen"></a>
##### *Erde erstellen:*

Erstellen wir die Erde, indem wir ein neues Blueprint erstellen und das Basis-Blueprint verwenden.

Für die Erde verwenden wir das Basis-Material und erstellen eine Instanz des Materials, um die Farbe im Editor zu konfigurieren.
Wir benennen die Instanz z.B. `MI_EarthSurface` oder `MI_EarthSurface_Inst`.
Die Instanz erstellen wir, indem wir mit Rechtsklick auf das Basis-Material und dann auf `Create Material Instance` klicken.

Die Farbe kann nach Belieben eingestellt werden.

die Skalierung des Meshes setzen wir auf `2,61` und die Initialgeschwindigkeit auf `16,7`.
Die wird auf `1000` gesetzt und die Linienfarbe auf `FLinearColor(0, 0, 1, 1)`.

Zum Schluss,
platzieren wir die Erde im Editor, indem wir sie in die Szene ziehen und die Position im Details Panel auf `0, 114242, 0` setzen.

![Erde positionieren](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/bp-earth-location.png)

Hinweis: Die Position, Masse und Initialgeschwindigkeit der Erde ist wichtig, damit die Orbits der Himmelskörper korrekt berechnet werden.
Die Eigenschaftsberechnungen können unter `Einsatzmittel` nachgelesen werden.

------------------------------------------------------------------------------------------------------------

<a name = "simulation-starten"></a>
## Simulation starten

Wenn wir jetzt die Simulation starten, sollten die Himmelskörper um die Sonne kreisen und die Orbits berechnet werden.
Da die Geschwindigkeit der Simulation von der Zeitskala abhängt, können wir die Simulation starten, stoppen und beschleunigen.

<a name="simulation-konfigurieren"></a>
#### Simulation konfigurieren

Momentan ist die einzige Möglichkeit die Zeitskala und Eigenschaften der Himmelskörper zu ändern, 
die Werte im Editor zu konfigurieren, wenn die Simulation läuft.

Das können wir machen, indem wir die Simulation im Editor starten und im Outliner Panel die `OrbitSimulation`-Instanz auswählen.
![Simulation konfigurieren 1](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/sim-config1.png)

Im Details Panel unter Physics können wir die Eigenschaft `Manual Time Scale` auf `true` setzen.
![Simulation konfigurieren 2](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/sim-config2.png)

Die `Time Scale` können wir auf einen höheren Wert setzen, um die Simulation zu beschleunigen oder auf einen niedrigeren Wert setzen, um die Simulation zu verlangsamen.
![Simulation konfigurieren 3](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/sim-config3.png)


------------------------------------------------------------------------------------------------------------

<a name="visualisierung-der-orbits"></a>
## Visualisierung der Orbits

Da wir die Umlaufbahnen der Himmelskörper um die Sonne berechnen, aber die Umlaufbahnen nicht sichtbar sind,
ist es sinnvoll einen Orbit-Visualisierungseffekt hinzuzufügen bzw. einen Debugger zu erstellen.

<a name="orbit-debugger-erstellen"></a>
#### *Orbit Debugger erstellen:*

Für den Debugger brauchen wir vorher noch eine Struktur für die virtuellen Himmelskörper, damit wir nicht die echten Himmelskörper verwenden,
ein Interface für die virtuellen Himmelskörper, um die Eigenschaften der Himmelskörper zu erhalten und in der Actor-Komponente zu setzen.
Die Actor-Komponente wird verwendet, um die Umlaufbahnen der Himmelskörper im Editor-Modus (nicht im Play-Modus) zu visualisieren.

<a name="virtuelle-himmelskoerper-struktur"></a>
##### *Virtuelle Himmelskörper Struktur:*

Die Struktur für die virtuellen Himmelskörper sollte in einer neuen Header-Datei `FVirtualBody.h` wie folgt aussehen:

```cpp
struct FVirtualBody
{
	float Mass;

	FVector Location;
	FVector Velocity;

	explicit FVirtualBody(const ACelestialBody* Body)
	{
		if (Body)
		{
			Mass = Body->GetMass();
			Location = Body->GetActorLocation();
			Velocity = Body->GetInitialVelocity();
		}
	}
};
```

Die Struktur `FVirtualBody` enthält die Masse, Position und Geschwindigkeit der virtuellen Himmelskörper.

Mit dem Konstruktor können wir die Eigenschaften der echten Himmelskörper in die virtuellen Himmelskörper übertragen.

<a name="virtuelle-himmelskoerper-interface"></a>
##### *Virtuelle Himmelskörper Interface:*

Dafür erstellen wir eine neue Unreal C++ Klasse, die von `UInterface` bzw. Interface abgeleitet ist und fügen die notwendigen Properties und Funktionen hinzu.

Das Interface für die virtuellen Himmelskörper besteht nur aus einer Header-Datei `IVirtualBody.h` und sollte wie folgt aussehen:

```cpp
#include "CoreMinimal.h"
#include "UObject/Interface.h"
#include "IVirtualBody.generated.h"

UINTERFACE(MinimalAPI)
class UVirtualBody : public UInterface
{
	GENERATED_BODY()
};

```

Wir fügen `UINTERFACE(MinimalAPI)` hinzu, um das Interface zu definieren.

Im zweiten Schritt fügen wir die Funktionen hinzu, um die Eigenschaften der virtuellen Himmelskörper zu erhalten und zu setzen.

Die Funktionen sollten folgendermaßen aussehen:

```cpp
#include "CoreMinimal.h"
#include "UObject/Interface.h"
#include "IVirtualBody.generated.h"

UINTERFACE(MinimalAPI)
class UVirtualBody : public UInterface
{
	GENERATED_BODY()
};

class SOLARSYSTEM_API IVirtualBody
{
	GENERATED_BODY()

public:
	virtual bool GetDrawOrbitPaths() const = 0;
	virtual void DrawOrbitPaths() = 0;
};
```

Die Funktion `GetDrawOrbitPaths` gibt den Bool zurück, um die Orbit-Visualisierung ein- und auszuschalten.
Die Funktion `DrawOrbitPaths` wird verwendet, um die Umlaufbahnen der Himmelskörper zu visualisieren.

<a name="orbitdebug-komponente"></a>
##### *OrbitDebug Komponente:*

Erstellen wir eine neue Unreal C++ Klasse, die von `UActorComponent` abgeleitet ist und fügen die notwendigen Properties und Funktionen hinzu.

Die Header-Datei `VirtualBodyComponent.h` sollte wie folgt aussehen:

```cpp
#include "CoreMinimal.h"
#include "IVirtualBody.h"
#include "Components/ActorComponent.h"
#include "OrbitDrawComponent.generated.h"


UCLASS(ClassGroup=(Custom), meta=(BlueprintSpawnableComponent))
class SOLARSYSTEM_API UOrbitDrawComponent : public USceneComponent
{
	GENERATED_BODY()

public:
	UOrbitDrawComponent();

private:
	IVirtualBody* OrbitDrawer = nullptr;
	
	void DrawOrbits() const;
	
	virtual void TickComponent(float DeltaTime, ELevelTick TickType,
								FActorComponentTickFunction* ThisTickFunction) override;
};
```

Wir fügen den Raw-Pointer `OrbitDrawer` hinzu, um das Interface für die virtuellen Himmelskörper zu verwenden.

Die Quelldatei `VirtualBodyComponent.cpp` sollte wie folgt aussehen:

```cpp
#include "OrbitDrawComponent.h"

UOrbitDrawComponent::UOrbitDrawComponent() : OrbitDrawer(Cast<IVirtualBody>(GetOwner()))
{
	PrimaryComponentTick.bCanEverTick = true;
	bTickInEditor = true;
}

void UOrbitDrawComponent::TickComponent(float DeltaTime, ELevelTick TickType, FActorComponentTickFunction* ThisTickFunction)
{
	Super::TickComponent(DeltaTime, TickType, ThisTickFunction);

	DrawOrbits();
}

void UOrbitDrawComponent::DrawOrbits() const
{
	if (OrbitDrawer && OrbitDrawer->GetDrawOrbitPaths())
	{
		OrbitDrawer->DrawOrbitPaths();
	}
}
```

Der Konstruktor initialisiert den Raw-Pointer `OrbitDrawer`, indem er das Interface von der OrbitDebug Klasse erhält.

In der `TickComponent`-Funktion wird die Funktion `DrawOrbits` aufgerufen, um die Umlaufbahnen der Himmelskörper zu visualisieren.

<a name="orbit-debug-klasse"></a>
##### *OrbitDebug Klasse:*

Erstellen wir einen Orbit-Debugger, um die Umlaufbahnen der Himmelskörper zu visualisieren.

Dazu erstellen wir eine neue C++ Klasse, die von `AActor` abgeleitet ist und fügen die notwendigen Properties und Funktionen hinzu.

Die Header-Datei `OrbitDebug.h` sollte wie folgt aussehen:

```cpp
#pragma once

#include "CoreMinimal.h"
#include "FVirtualBody.h"
#include "IVirtualBody.h"
#include "OrbitDrawComponent.h"
#include "GameFramework/Actor.h"
#include "OrbitDebug.generated.h"

UCLASS()
class SOLARSYSTEM_API AOrbitDebug : public AActor, public IVirtualBody
{
	GENERATED_BODY()

public:
	AOrbitDebug();
```

Die Header-Dateien für die virtuellen Himmelskörper, das Interface und die Actor-Komponente werden in der OrbitDebug-Klasse verwendet.
Außerdem wird `IVirtualBody` als Interface für die virtuellen Himmelskörper implementiert.


<a name="orbit-debug-properties"></a>
##### *OrbitDebug Properties:*

Jetzt fügen wir erstmal die Properties hinzu, um die Umlaufbahnen der Himmelskörper zu visualisieren.
Dafür brauchen wir folgende Properties:
- OrbitDrawComponent (Actor-Komponente für die Orbit-Visualisierung)
- Bool für das Ein- und Ausschalten der Orbit-Visualisierung
- Linien-Dicke (Für die Visualisierung der Orbits)
- Anzahl der Schritte für die Umlaufbahn (Anzahl der Punkte)
- Zeitintervall für die Umlaufbahn (Abstand zwischen den Punkten)

Die Properties für den Orbit-Debugger sollten folgendermaßen aussehen:

```cpp
protected:
	AOrbitDebug();
	
	UPROPERTY(VisibleDefaultsOnly)
	UOrbitDrawComponent* OrbitDrawComponent;
	
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Orbit Debug")
	bool bDrawOrbitPaths;
	
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Orbit Debug")
	float LineThickness = 1.5f;

	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Orbit Debug")
	int NumSteps = 35000;

	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Orbit Debug")
	float TimeStep = 0.1f;
```

Alle Properties sind im Blueprint editierbar, damit wir die Umlaufbahnen der Himmelskörper konfigurieren können.

Die `OrbitDrawComponent`-Property wird verwendet, um die Umlaufbahnen der Himmelskörper zu visualisieren.

Der `bDrawOrbitPaths`-Bool wird verwendet, um die Orbit-Visualisierung ein- und auszuschalten.

Die `NumSteps`-Property gibt die Anzahl der Punkte an, die für die Umlaufbahn berechnet werden.
Die `TimeStep`-Property gibt das Zeitintervall an, das für die Umlaufbahn verwendet wird.

Die `LineThickness`-Property gibt die Dicke der Linien an, die für die Umlaufbahn verwendet wird.

<a name="orbitdebug-getter-und-setter"></a>
##### *OrbitDebug Getter und Setter:*

Jetzt fügen wir die Getter- und Setter-Funktionen hinzu, um die Properties zu erhalten und zu setzen.
Die Getter- und Setter-Funktionen sollten folgendermaßen aussehen:

```cpp
public:
	virtual bool GetDrawOrbitPaths() const override { return bDrawOrbitPaths; }
	void SetDrawOrbitPaths(const bool& bNewDrawOrbitPaths) { bDrawOrbitPaths = bNewDrawOrbitPaths; }

	float GetLineThickness() const { return LineThickness; }
	void SetLineThickness(const float& NewLineThickness) { LineThickness = NewLineThickness; }

	int GetNumSteps() const { return NumSteps; }
	void SetNumSteps(const int& NewNumSteps) { NumSteps = NewNumSteps; }

	float GetTimeStep() const { return TimeStep; }
	void SetTimeStep(const float& NewTimeStep) { TimeStep = NewTimeStep; }
```

Die Getter- und Setter-Funktionen sind `inline` und geben die Properties zurück bzw. setzen die Properties.

<a name="orbit-debug-funktionen"></a>
##### *OrbitDebug Funktionen:*

Als Nächstes fügen wir die Interface-Funktionen hinzu.

Die Funktionen in der Header-Datei `OrbitDebug.h` sollten folgendermaßen aussehen:

```cpp
	virtual void DrawOrbitPaths() override;
```

Für die Berechnung der Umlaufbahnen der Himmelskörper brauchen wir folgende Funktionen:

```cpp
private:
	TArray<FVirtualBody> InitializeVirtualBodies(const TArray<AActor*>& Bodies);
	void SimulateOrbits(TArray<FVirtualBody>& VirtualBodies, TArray<FVector>& DrawPoints) const;
	void UpdateVelocities(TArray<FVirtualBody>& VirtualBodies) const;
	void UpdatePositions(TArray<FVirtualBody>& VirtualBodies, TArray<FVector>& DrawPoints, const int& Step) const;
	void DrawPaths(const TArray<FVirtualBody>& VirtualBodies, const TArray<FVector>& DrawPoints, TArray<AActor*> Bodies) const;
	FVector CalculateAcceleration(const int& BodyIndex, const TArray<FVirtualBody>& VirtualBodies) const;
```

Die Funktion `InitializeVirtualBodies` initialisiert die virtuellen Himmelskörper basierend auf den echten Himmelskörpern.

Die Funktion `SimulateOrbits` simuliert die Umlaufbahnen der Himmelskörper basierend auf den virtuellen Himmelskörpern.

Die Funktionen `UpdateVelocities` und `UpdatePositions` aktualisieren die Geschwindigkeiten und Positionen der virtuellen Himmelskörper.

Die Funktion `DrawPaths` visualisiert die Umlaufbahnen der Himmelskörper basierend auf den virtuellen Himmelskörpern.

Die Funktion `CalculateAcceleration` berechnet die Beschleunigung der Himmelskörper basierend auf den virtuellen Himmelskörpern.


Fangen wir mit dem Konstruktor in der Quelldatei an, um die `OrbitDrawComponent` zu initialisieren.
Die Implementierung der Funktion sollte in der Quelldatei `OrbitDebug.cpp` wie folgt aussehen:

```cpp
#include "OrbitDebug.h"

#include "OrbitDrawComponent.h"
#include "Kismet/GameplayStatics.h"
#include "SolarSystem/Structs/Universe.h"

AOrbitDebug::AOrbitDebug()
{
	PrimaryActorTick.bCanEverTick = true;
	OrbitDrawComponent = CreateDefaultSubobject<UOrbitDrawComponent>(TEXT("DebugDraw"));
	RootComponent = OrbitDrawComponent;
}
```

Die `OrbitDrawComponent` wird als Subobjekt erstellt und als Root-Komponente gesetzt.

Die Implementierung der Funktion `DrawOrbitPaths` sollte in der Quelldatei `OrbitDebug.cpp` wie folgt aussehen:

```cpp
void AOrbitDebug::DrawOrbitPaths()
{
	const UWorld* World = GetWorld();
	if (World == nullptr) return;
	
	TArray<AActor*> Bodies;
	UGameplayStatics::GetAllActorsOfClass(World, ACelestialBody::StaticClass(), Bodies);
	if (Bodies.Num() == 0) return;
	
	TArray<FVector> DrawPoints;
	DrawPoints.SetNum(Bodies.Num() * GetNumSteps());
	TArray<FVirtualBody> VirtualBodies = InitializeVirtualBodies(Bodies);

	SimulateOrbits(VirtualBodies, DrawPoints);
	DrawPaths(VirtualBodies, DrawPoints, Bodies);
}
```

Es werden alle Himmelskörper in der Scene gesucht und in dem Array `Bodies` gespeichert.
Das Array `DrawPoints` wird initialisiert und die größe wird auf die Anzahl der Himmelskörper multipliziert mit der Anzahl der Schritte gesetzt.
Das Array `VirtualBodies` wird initialisiert, um die virtuellen Himmelskörper zu speichern.

Die Funktion `SimulateOrbits` wird aufgerufen, um die Umlaufbahnen der Himmelskörper zu simulieren.
Die Funktion `DrawPaths` wird aufgerufen, um die Umlaufbahnen der Himmelskörper zu visualisieren.

Die Implementierung der Funktion `InitializeVirtualBodies` sollte in der Quelldatei `OrbitDebug.cpp` wie folgt aussehen:

```cpp
TArray<FVirtualBody> AOrbitDebug::InitializeVirtualBodies(const TArray<AActor*>& Bodies)
{
	TArray<FVirtualBody> VirtualBodies;
	VirtualBodies.Reserve(Bodies.Num());
	
	for (const auto& Body : Bodies)
	{
		ACelestialBody* CelestialBody = Cast<ACelestialBody>(Body);
		if (CelestialBody)
		{
			VirtualBodies.Add(FVirtualBody(CelestialBody));
		}
	}
	
	return VirtualBodies;
}
```

Die Funktion `InitializeVirtualBodies` initialisiert die virtuellen Himmelskörper basierend auf den echten Himmelskörpern.

Die Implementierung der Funktion `SimulateOrbits` sollte in der Quelldatei `OrbitDebug.cpp` wie folgt aussehen:

```cpp
void AOrbitDebug::SimulateOrbits(TArray<FVirtualBody>& VirtualBodies, TArray<FVector>& DrawPoints) const
{
    for (int Step = 0; Step < NumSteps; ++Step)
    {
        UpdateVelocities(VirtualBodies);
        UpdatePositions(VirtualBodies, DrawPoints, Step);
    }
}
```

Die Funktion `SimulateOrbits` simuliert die Umlaufbahnen der Himmelskörper basierend auf den virtuellen Himmelskörpern.

Die Implementierung der Funktion `UpdateVelocities` sollte in der Quelldatei `OrbitDebug.cpp` wie folgt aussehen:

```cpp
void AOrbitDebug::UpdateVelocities(TArray<FVirtualBody>& VirtualBodies) const
{
	for (int i = 0; i < VirtualBodies.Num(); ++i)
	{
		VirtualBodies[i].Velocity += CalculateAcceleration(i, VirtualBodies) * GetTimeStep();
	}
}
```

Die Funktion `UpdateVelocities` aktualisiert die Geschwindigkeiten der virtuellen Himmelskörper basierend auf der Beschleunigung und dem Zeitintervall.

Die Implementierung der Funktion `UpdatePositions` sollte in der Quelldatei `OrbitDebug.cpp` wie folgt aussehen:

```cpp
void AOrbitDebug::UpdatePositions(TArray<FVirtualBody>& VirtualBodies, TArray<FVector>& DrawPoints, const int& Step) const
{
	for (int i = 0; i < VirtualBodies.Num(); ++i)
	{
		VirtualBodies[i].Location += VirtualBodies[i].Velocity * GetTimeStep();
		DrawPoints[i * GetNumSteps() + Step] = VirtualBodies[i].Location;
	}
}
```

Die Funktion `UpdatePositions` aktualisiert die Positionen der virtuellen Himmelskörper basierend auf den Geschwindigkeiten und dem Zeitintervall.

Die Implementierung der Funktion `DrawPaths` sollte in der Quelldatei `OrbitDebug.cpp` wie folgt aussehen:

```cpp
void AOrbitDebug::DrawPaths(const TArray<FVirtualBody>& VirtualBodies, const TArray<FVector>& DrawPoints, TArray<AActor*> Bodies) const
{
	for (int i = 0; i < VirtualBodies.Num(); ++i)
	{
		const ACelestialBody* CelestialBody = Cast<ACelestialBody>(Bodies[i]);
		FColor PathColor = CelestialBody->GetLineColor().ToFColor(true);
		if (CelestialBody == nullptr || CelestialBody->ActorHasTag(CentralBodyTag)) continue;
		for (int Steps = 0; Steps < GetNumSteps() - 1; ++Steps)
		{
			FVector Point = DrawPoints[i * GetNumSteps() + Steps];
			DrawDebugPoint(GetWorld(), Point, GetLineThickness(), PathColor, false, -1.0f);
		}
	}
}
```

Die Funktion `DrawPaths` visualisiert die Umlaufbahnen der Himmelskörper basierend auf den virtuellen Himmelskörpern.

Es wird über alle Himmelskörper iteriert, die Farbe wird vom Himmelskörper genutzt, womit die Umlaufbahn gezeichnet wird.

Die Implementierung der Funktion `CalculateAcceleration` sollte in der Quelldatei `OrbitDebug.cpp` wie folgt aussehen:

```cpp
FVector AOrbitDebug::CalculateAcceleration(const int& BodyIndex, const TArray<FVirtualBody>& VirtualBodies) const
{
	FVector Acceleration = FVector::ZeroVector;

	for (int i = 0; i < VirtualBodies.Num(); ++i)
	{
		if(BodyIndex != i)
		{
			const FVector Direction = VirtualBodies[i].Location - VirtualBodies[BodyIndex].Location;
			const float Distance = Direction.Size();
			const float Force = FUniverse::GravitationalConstant * VirtualBodies[i].Mass * VirtualBodies[BodyIndex].Mass / (Distance * Distance);
			Acceleration += Direction.GetSafeNormal() * (Force / VirtualBodies[BodyIndex].Mass);
		}
	}
	
	return Acceleration;
}
```

Die Funktion `CalculateAcceleration` berechnet die Beschleunigung der Himmelskörper basierend auf den virtuellen Himmelskörpern.

Die Beschleunigung wird für jeden Himmelskörper berechnet, indem die Richtung, die Distanz und die Gravitationskraft verwendet wird.

<a name="orbit-debuger-verwenden"></a>
### Orbit-Debugger verwenden:

<a name="orbit-debugger-blueprint-erstellen"></a>
##### *Orbit Debugger Blueprint erstellen:*

Um den Debugger zu verwenden, erstellen wir eine neues Blueprint, indem wir mit Rechtsklick auf den Ordner `Blueprints` und dann auf `Blueprint Class` klicken.
Wir suchen nach `AOrbitDebug` und wählen die Klasse als Parent Class aus.

![Orbit-Debugger erstellen](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/create-debugger-bp.png)

Das Blueprint können wir jetzt in der Szene platzieren und die Parameter im Editor nach Belieben konfigurieren.

![Orbit-Debugger platzieren](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/set-debugger-bp.png)

<a name="orbit-debugger-konfigurieren"></a>
##### *Orbit-Debugger konfigurieren:*

Die `bDrawOrbitPaths`-Property wird verwendet, um die Orbit-Visualisierung ein- und auszuschalten.
![Orbit-Debugger konfigurieren 1](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/earth-orbit-entry.png)

Die `NumSteps`-Property gibt die Anzahl der Punkte an, die für die Umlaufbahn berechnet werden.
![Orbit-Debugger konfigurieren 2](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/earth-orbit-numsteps.png)

Die `TimeStep`-Property gibt das Zeitintervall an, das für die Umlaufbahn verwendet wird.
![Orbit-Debugger konfigurieren 3](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/earth-orbit-timestep.png)

Die `LineThickness`-Property gibt die Dicke der Linien an, die für die Umlaufbahn verwendet wird.
![Orbit-Debugger konfigurieren 4](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/earth-orbit-linethickness.png)

Nochmal zur Visualisierung des `TimeStep` in Kombination mit der `LineThickness`.
![Orbit-Debugger konfigurieren 5](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/earth-orbit-linethickness-timestep.png)

Beispiele wie der Debugger genutzt werden kann.

![Orbit-Debugger Beispiel 1](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/solarsystem-orbits1.png)

![Orbit-Debugger Beispiel 2](https://github.com/goldbarth/SolarSystem/blob/goldbarth/media/images/solarsystem-orbits2.png)

Es macht absolut Sinn mit den Himmelskörper Werten (Radius, Masse und Initial-Geschwindigkeit) zu experimentieren und sie zu verändern. 
Die Kalkulationen in den [Einsatzmitteln](#einsatzmittel) können dabei helfen eine realistische Simulation zu erstellen.

------------------------------------------------------------------------------------------------------------

Wenn du das Sonnensystem als Modell nachbauen möchtest, kannst du die Himmelskörper und Orbits wie folgt konfigurieren:
[Modell-Kalkulationen](https://github.com/goldbarth/SolarSystem/blob/goldbarth/docs/calc/README.md)

Hier sind alle Werte (Skalierung, Masse, Geschwindigkeit, Abstand zur Sonne) für die Himmelskörper im Sonnensystem aufgelistet.

------------------------------------------------------------------------------------------------------------
<a name="einsatzmittel"></a>
## Einsatzmittel

- Unreal Engine 5.3.2
- Visual Studio 2022, JetBrains Rider oder ein anderer IDE mit C++ Unterstützung
- Unreal Engine 5.3 Dokumentation: [UE 5.3](https://dev.epicgames.com/documentation/de-de/unreal-engine/unreal-engine-5-3-documentation)

- Berechnungen der Eigenschaften von Himmelskörpern und Orbits: [Modell-Kalkulationen](https://github.com/goldbarth/SolarSystem/blob/goldbarth/docs/calc/README.md)