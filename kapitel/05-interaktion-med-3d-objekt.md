# Kapitel 5: Interaktion med 3D-objekt

> **I det här kapitlet lär du dig**
> - vilka sätt som finns att peka på, greppa och trycka på saker i 3D
> - vad signaler och återkoppling betyder för interaktionen
> - hur kollisioner och triggers skiljer sig åt
> - hur du undviker att snabba föremål åker rakt igenom väggar

Sträck ut handen och ta en mugg. Det tar en halv sekund, och du har inte tänkt på det. Ändå har din hand bedömt avståndet, formats efter muggen och känt när den träffat. I en 3D-miljö ska du bygga allt detta själv: spelaren ska förstå att muggen går att ta, kunna ta den, och märka att det hände.

## Tre frågor för varje interaktion

Oavsett plattform kan du ställa samma tre frågor:

1. **Vad kan jag göra här?** Saker måste se ut som att de går att använda. Den egenskapen kallas **signal** (*signifier*): en knapp som ser nedtryckbar ut, ett handtag som ser greppbart ut.
2. **Hur gör jag det?** Den fysiska handlingen, som att trycka in greppknappen.
3. **Hände det?** Utan **återkoppling** (*feedback*) vet spelaren inte om handlingen fungerade. Ljud, vibration och visuell förändring är olika sorters återkoppling.

Ett ord du ofta stöter på är **affordans**: vilka handlingar som faktiskt är möjliga med ett föremål. En signal berättar om affordansen.

## Sätt att interagera i VR

| Metod | Hur det går till | Bra för | Sämre för |
|---|---|---|---|
| **Direkt grepp** | Handen rör föremålet och du håller in greppet | Racket, klot, pil | Saker långt bort |
| **Strålpekning** | En stråle från handen pekar ut ett mål | Menyer, föremål på avstånd | Finmotorik |
| **Tryck** (*poke*) | Fingret eller kontrollen trycker på en yta | Knappar nära kroppen | Ytor långt bort |

I XR Interaction Toolkit gör du ett föremål greppbart med komponenten `XRGrabInteractable`. Föremålet behöver också en `Collider` och en `Rigidbody`. Du kan reagera på grepp och släpp i kod med `selectEntered` och `selectExited`. [Virtual-Reality](https://github.com/abbjetmus/Virtual-Reality) visar hur.

### Hur föremålet följer handen

`XRGrabInteractable` har inställningen **Movement Type**. Den avgör hur föremålet flyttas när du håller det.

| Movement Type | Vad som händer | När du väljer det |
|---|---|---|
| **Instantaneous** | Föremålet följer handen direkt, men kan passera genom andra föremål | Saker som ska kännas exakta och inte stöta i något |
| **Kinematic** | Föremålet flyttas mot handen under fysikberäkningen | Mellanläge |
| **Velocity Tracking** | Föremålet får en hastighet som drar det mot handen | Redskap som ska slå till något, som en putter eller ett racket |

För kast används **Throw On Detach**, som låter föremålet behålla handens hastighet när du släpper. **Throw Velocity Scale** justerar hur hårt kastet blir. Rätt värden går inte att gissa. Du måste testa i headsetet.

## Kollision eller trigger?

Spelet behöver känna av när saker möts. Det finns två sätt, och valet spelar roll.

| | Kollision | Trigger |
|---|---|---|
| Vad händer fysiskt? | Föremål stöter ifrån varandra | Föremål passerar igenom |
| Metod i Unity | `OnCollisionEnter` | `OnTriggerEnter` |
| Inställning i Unity | Vanlig `Collider` | `Is Trigger` ikryssad |
| Motsvarighet i Godot | `StaticBody3D`, `RigidBody3D` och `move_and_slide()` | `Area3D` och signalen `body_entered` |
| Exempel | Boll mot sarg | Bollen går i hålet, spelaren plockar upp ett mynt |

För att Unity ska registrera en trigger måste minst ett av föremålen ha en `Rigidbody`.

Så här kan en måltrigger se ut i Unity. Skriptet sitter på målet och använder `PoangManager` från kursens [Virtual-Reality](https://github.com/abbjetmus/Virtual-Reality).

```csharp
using UnityEngine;

public class Mal : MonoBehaviour
{
    [SerializeField] private int poang = 10;

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Boll"))
        {
            PoangManager.Instans.LaggTillPoang(poang);
        }
    }
}
```

Samma idé i Godot, som ett samlarföremål. Noden är en `Area3D`, och spelaren ligger i gruppen `player`.

```gdscript
extends Area3D

signal collected

func _ready() -> void:
    body_entered.connect(_on_body_entered)

func _on_body_entered(body: Node3D) -> void:
    if body.is_in_group("player"):
        collected.emit()
        queue_free()
```

Signalen `collected` gör att poängräkningen kan ligga någon annanstans. Samlarföremålet behöver inte veta vem som lyssnar.

## Fysik och fasta steg

Fysiken räknas inte kontinuerligt utan i fasta steg, och i Unity är standardvärdet 0,02 sekunder. Därför ska all påverkan på en `Rigidbody` ligga i `FixedUpdate()`.

### Genomräknat exempel: bollen som åker igenom väggen

En boll flyger med hastigheten 15 m/s. Hur långt hinner den mellan två fysiksteg?

```
sträcka = hastighet × tid
sträcka = 15 m/s × 0,02 s = 0,30 m
```

Bollen hoppar alltså 30 centimeter mellan varje beräkning. Är väggen 5 centimeter tjock kan bollen befinna sig framför väggen i ett steg och bakom den i nästa, och kollisionen registreras aldrig. Det kallas **tunneleffekt** (*tunneling*).

Det finns flera lösningar. Sätt **Collision Detection** på bollens `Rigidbody` till **Continuous**, så kontrollerar motorn vägen mellan stegen. Du kan också göra väggar tjockare eller begränsa maxhastigheten.

## Peka med en stråle

**Raycasting** betyder att du skickar ut en osynlig stråle och frågar vad den träffar. Det används för strålpekning i VR, och för att skjuta eller titta på föremål i ett vanligt 3D-spel. Kursens [raycastShoot.cs](https://github.com/abbjetmus/3D-AR-VR-Interface-Design/blob/main/Code%20Snippets/3D/raycastShoot.cs) visar ett exempel i Unity. Tänk på att det skriptet använder Unitys äldre inmatningssystem, och att VR-projektet i stället läser in handkontrollerna genom XR Interaction Toolkit.

## Begrepp

- **Affordans:** handlingar som är möjliga med ett föremål.
- **Signal (signifier):** något som visar att en handling är möjlig.
- **Återkoppling:** svar från systemet på användarens handling.
- **Collider:** form som används för kollisioner.
- **Rigidbody:** komponent som gör att ett föremål påverkas av fysik.
- **Trigger:** collider som känner av men inte stoppar.
- **Tunneleffekt:** snabbt föremål passerar genom andra föremål mellan fysikstegen.
- **Raycasting:** att skicka ut en osynlig stråle och se vad den träffar.

## Testa dig själv

1. Vilka tre frågor ska varje interaktion kunna svara på?
2. När passar direkt grepp bättre än strålpekning, och tvärtom?
3. Vad är skillnaden mellan kollision och trigger?
4. Varför är Velocity Tracking bättre än Instantaneous för en golfklubba?
5. Vad är tunneleffekt, och vilka lösningar finns?
6. Varför är det smart att ett samlarföremål skickar en signal i stället för att själv räkna poäng?

## Koppling till projektet

I [VR/AR - Projekt](../projekt/vr-ar/README.md) bygger ni grepp, kast, träffdetektion och regelsystem. I [3D-Spel](../projekt/3d-spel/README.md) hanterar du kollisioner, mål, samlarföremål och fiender.

## Läs mer

- [XR Grab Interactable](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@3.2/manual/xr-grab-interactable.html)
- [Unity: Rigidbody](https://docs.unity3d.com/6000.0/Documentation/Manual/class-Rigidbody.html)
- [Unity: Colliders](https://docs.unity3d.com/Manual/CollidersOverview.html)

[← Föregående](04-navigation-och-forflyttning.md) | [Innehåll](../README.md) | [Nästa →](06-modellering-och-texturer.md)
