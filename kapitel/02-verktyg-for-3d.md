# Kapitel 2: Verktyg för 3D

> **I det här kapitlet lär du dig**
> - vad en spelmotor gör och hur Unity och Godot skiljer sig åt
> - hur en 3D-scen är uppbyggd av objekt i en hierarki
> - hur koordinater, skala och transformationer fungerar
> - varför bildfrekvens är en designfråga och hur du räknar på den

Du kan skriva ett 3D-program från grunden, men då får du lösa ljussättning, fysik, ljud och inläsning av modeller själv innan du ens börjat på det roliga. En **spelmotor** är ett färdigt ramverk som redan gör allt detta. Du beskriver vad som finns i världen och hur det ska bete sig, och motorn ritar upp det 72 gånger per sekund eller mer.

I kursen använder du två motorer: Unity med C# i VR-projektet och Godot med GDScript i 3D-spelet.

## Två motorer, samma idéer

| | Unity | Godot |
|---|---|---|
| Språk i kursen | C# | GDScript |
| Byggstenar | GameObjects med komponenter | Noder i ett träd |
| Scener | Scener, och prefabs som mallar | Scener, som också fungerar som mallar |
| Körs varje bildruta | `Update()` | `_process(delta)` |
| Körs med fast takt för fysik | `FixedUpdate()` | `_physics_process(delta)` |
| Körs vid start | `Start()` | `_ready()` |
| Koordinatsystem | Y uppåt, +Z framåt | Y uppåt, −Z framåt |

Skillnaden i tänk är värd att förstå. I Unity är ett **GameObject** nästan tomt, och du ger det egenskaper genom att lägga på **komponenter**: en `Rigidbody` för fysik, en `AudioSource` för ljud, ett eget skript för beteende. I Godot har varje **nod** redan en bestämd uppgift. En `Camera3D` är en kamera, en `CollisionShape3D` är en kollisionsform, och du bygger funktioner genom att sätta ihop noder i ett träd.

## Scen och hierarki

Oavsett motor är en 3D-värld ett träd av objekt. Ett **barn** följer alltid sin **förälder**. Flyttar du en bil följer hjulen med, utan att du behöver flytta varje hjul.

I VR-projektet ser det ut ungefär så här:

```
VRPlayer             ← XR Origin, spelarens plats i världen
└── Camera Offset    ← justerar höjden
    ├── Main Camera  ← följer headsetet
    ├── LeftHand     ← följer vänster handkontroll
    └── RightHand    ← följer höger handkontroll
```

När du teleporterar spelaren flyttar du bara `VRPlayer`. Kamera och händer följer med automatiskt, eftersom de ligger under i hierarkin.

## Position, rotation och skala

Varje objekt har en **transform**: position, rotation och skala. Positionen är tre tal (x, y, z). I både Unity och Godot brukar 1 enhet motsvara 1 meter.

Skala är ingen detalj. På en skärm märker ingen om bordet är lite för stort, men i ett headset jämför kroppen allt med sig själv. Ett pingisbord ska vara 2,74 meter långt. Gör du det 4 meter långt känns det fel direkt, även om du inte kan säga varför.

Tänk också på skillnaden mellan **lokala** och **globala** koordinater. Den lokala positionen anges i förhållande till föräldern, den globala i förhållande till hela världen. En hand på position (0, 0, 0) lokalt ligger alltså precis vid sin förälder, inte mitt i världen.

## Bildfrekvens är en designfråga

**Bildfrekvens** mäts i bilder per sekund, FPS. Motorn har en begränsad tid för att räkna ut varje bild, och det kallas **bildbudget**.

### Genomräknat exempel: bildbudget

Tiden per bild får du genom att dela en sekund (1000 millisekunder) med antalet bilder per sekund.

| Bildfrekvens | Beräkning | Tid per bild |
|---|---|---|
| 60 FPS | 1000 / 60 | 16,67 ms |
| 72 FPS | 1000 / 72 | 13,89 ms |
| 90 FPS | 1000 / 90 | 11,11 ms |

Allt måste hinna klart inom den tiden: spellogik, fysik, grafik och ljud. Dessutom ska bilden i ett headset ritas för båda ögonen. Tar en bild 20 ms klarar du bara 50 FPS (1000 / 20), och det märks.

På en skärm är en hackande bild irriterande. I VR kan den ge illamående, eftersom hjärnan får en bild som inte stämmer med hur huvudet rör sig. Kursens VR-krav är därför en stabil bildfrekvens, och i ett VR-spel behöver den ligga på ungefär 72–90 FPS. Därför används ofta enkla modeller, få ljuskällor och förberäknad ljussättning i VR (se [kapitel 6](06-modellering-och-texturer.md)).

## Unity: så kommer du igång

VR-projektet körs i Unity 6 med mallen **Universal 3D**, som använder renderingsvägen URP. Du behöver också modulen **Android Build Support**, eftersom spelet ska byggas för headsetet.

Ett skript i Unity är en egen komponent. Den här räcker för att se att allt fungerar:

```csharp
using UnityEngine;

public class SpelStart : MonoBehaviour
{
    void Start()
    {
        Debug.Log("Spelet startar!");
    }
}
```

För VR lägger du till **XR Plug-in Management**, **OpenXR** och **XR Interaction Toolkit**. **XR Origin** är den färdiga spelarriggen. Har du inget headset ledigt kan du testa med en simulator som styrs med tangentbord och mus: Unitys **XR Interaction Simulator** är den nyare, och i äldre material kan du se **XR Device Simulator**. Testa alltid i riktigt headset också, för det som ser bra ut på skärmen kan kännas helt fel på huvudet.

## Godot: så kommer du igång

I Godot skapar du en scen med en `Node3D` som rot och lägger till barn. Ett enkelt skript ser ut så här:

```gdscript
extends Node3D

func _ready() -> void:
    print("Spelet startar!")
```

Börja med tutorialen [Your first 3D game](https://docs.godotengine.org/en/stable/getting_started/first_3d_game/index.html) i Godots dokumentation.

Ett varningsord om äldre exempel på nätet och i kursens material: `KinematicBody3D` och `move_and_slide(velocity)` används inte i dagens Godot 4. Där heter noden `CharacterBody3D`, och hastigheten är en egenskap på noden. Du ser hur det ser ut i [kapitel 4](04-navigation-och-forflyttning.md).

## Vad ska jag välja?

Vilken motor du använder bestäms av projektet i den här kursen, men i verkligheten måste du välja själv. Ställ de här frågorna: Vilken plattform ska det köras på? Finns det färdiga verktyg för det du behöver? Vad kan gruppen sedan tidigare? Hur stor är projektfilen, och klarar er versionshantering den?

## Begrepp

- **Spelmotor:** ramverk som sköter grafik, fysik, ljud och inläsning.
- **GameObject:** Unitys grundobjekt, som får egenskaper av komponenter.
- **Komponent:** en del av ett GameObject som ger det en egenskap.
- **Nod:** Godots byggsten, med en bestämd uppgift.
- **Prefab:** Unitys återanvändbara mall för ett objekt.
- **Transform:** position, rotation och skala.
- **Lokala koordinater:** position i förhållande till föräldern.
- **FPS:** bilder per sekund.
- **Bildbudget:** tiden som finns för att räkna ut en bild.

## Koppling till projektet

I [VR/AR - Projekt](../projekt/vr-ar/README.md) går de första lektionerna till att installera Unity, lära sig grunderna och bygga VR-spelaren. I [3D-Spel](../projekt/3d-spel/README.md) repeterar du Godots noder och scener i 3D innan du börjar på tutorialen.

## Läs mer

- [Unity Manual: XR](https://docs.unity3d.com/Manual/XR.html)
- [XR Interaction Toolkit](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@3.2/manual/index.html)
- [Godot: Introduction to 3D](https://docs.godotengine.org/en/stable/tutorials/3d/introduction_to_3d.html)
- [Virtual-Reality](https://github.com/abbjetmus/Virtual-Reality), kursens krav och exempel för Unity

[← Föregående](01-vr-ar-och-plats.md) | [Innehåll](../README.md) | [Nästa →](03-forstudie-och-projektplan.md)
