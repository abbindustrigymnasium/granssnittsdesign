# Kapitel 4: Navigation och förflyttning

> **I det här kapitlet lär du dig**
> - skillnaden mellan att orientera sig och att förflytta sig
> - hur kameran styr vad spelaren förstår av rummet
> - hur du programmerar rörelse i Godot och vad som kan gå fel
> - varför VR behöver andra förflyttningsmetoder än vanliga spel

Ställ dig i mitten av en stor, grå hall utan fönster. Du kan gå åt alla håll, men du har ingen aning om vart du ska. Så känns en 3D-miljö utan navigation. Att kunna röra sig räcker inte. Spelaren måste också veta var hon är, vart hon är på väg och hur hon tar sig dit.

## Orientering och förflyttning

**Navigation** består av två delar:

- **Orientering** (på engelska *wayfinding*): att förstå var du är och vart du ska. Det är ett tankearbete.
- **Förflyttning** (*travel*): att faktiskt ta sig dit.

Spelare orienterar sig med hjälp av **landmärken**, alltså tydliga föremål som syns långt ifrån och som går att känna igen. Ett högt torn mitt på kartan gör att spelaren alltid vet åt vilket håll det är. Andra hjälpmedel är ljussättning som leder blicken, stigar, färgkoder och en minikarta.

## Kameran

Kameran är spelarens ögon, och den är också ett gränssnitt. Vad du ser avgör vad du förstår.

| Kameratyp | Fördelar | Nackdelar |
|---|---|---|
| **Förstapersons** | Inlevelse, bra precision | Du ser inte din egen kropp, svårare att bedöma hopp |
| **Tredjepersons** | Du ser figuren och omgivningen | Kameran kan fastna i väggar |
| **Fast kamera** | Du styr exakt vad som syns | Spelaren kan tappa riktningen vid kameraklipp |

I Godot löser du väggproblemet för en tredjepersonskamera med noden `SpringArm3D`. Den drar in kameran mot spelaren när något är i vägen.

## Rörelse i 3D-spelet

I Godot 4 använder du `CharacterBody3D` för en figur som spelaren styr. Här är ett fullständigt skript. Det förutsätter att du lagt till åtgärderna `move_left`, `move_right`, `move_forward`, `move_back` och `jump` i projektets Input Map.

```gdscript
extends CharacterBody3D

@export var speed := 5.0
@export var jump_velocity := 4.5
var gravity: float = ProjectSettings.get_setting("physics/3d/default_gravity")

func _physics_process(delta: float) -> void:
    if not is_on_floor():
        velocity.y -= gravity * delta

    if Input.is_action_just_pressed("jump") and is_on_floor():
        velocity.y = jump_velocity

    var input_dir := Input.get_vector("move_left", "move_right", "move_forward", "move_back")
    var direction := (transform.basis * Vector3(input_dir.x, 0, input_dir.y)).normalized()

    velocity.x = direction.x * speed
    velocity.z = direction.z * speed

    move_and_slide()
```

Gå igenom raderna. Först läggs gravitationen på när figuren inte står på marken. Sedan läses inmatningen till en riktning, och `transform.basis` gör att "framåt" betyder figurens framåt, inte världens. `move_and_slide()` flyttar figuren och låter den glida längs väggar.

Koden ligger i `_physics_process` och inte i `_process`, eftersom rörelse med kollisioner ska räknas med fast takt.

### Genomräknat exempel: varför diagonalen är farlig

Säg att spelaren håller ned både framåt och höger, och att du inte normaliserar riktningen. Då blir riktningsvektorn (1, 0, 1). Hastighetens längd får du med Pythagoras sats:

```
längd = √(1² + 1²) = √2 ≈ 1,414
hastighet = 5 m/s × 1,414 ≈ 7,07 m/s
```

Spelaren rör sig alltså ungefär 41 procent snabbare diagonalt. Funktionen `normalized()` gör att riktningen alltid har längden 1, så att hastigheten blir 5 m/s oavsett håll.

## Förflyttning i VR

I ett vanligt spel kan du trycka framåt och kameran glider iväg. I ett headset är det annorlunda. Dina ögon ser rörelse, men balansorganet i innerörat känner ingen. Den krocken kan ge **åksjuka** (cybersickness), och känslan av att röra sig utan att göra det kallas **vektion**.

| Metod | Hur det fungerar | Komfort | Passar till |
|---|---|---|---|
| **Stillastående** | Spelaren står på en plats | Mycket bra | Sportspel, som dart och bowling |
| **Rumsskala** | Spelaren går på riktigt inom ett begränsat område | Mycket bra | Små miljöer |
| **Teleportering** | Peka och hoppa direkt till platsen | Bra | Större miljöer, delar av banan |
| **Snap turn** | Vrid i fasta steg | Bra | Spel där spelaren sitter eller står still |
| **Mjuk förflyttning** | Styrspaken glider dig framåt | Kan ge illamående | Vana spelare, gärna som tillval |

Metas riktlinjer rekommenderar att begränsa acceleration, hålla hastigheten nära verklig gång och att erbjuda mjuk vridning bara som ett tillval. Regeln som står i kursens krav är enkel: **flytta aldrig spelarens vy utan att spelaren själv styr det.**

I XR Interaction Toolkit finns färdiga delar för detta: **Teleportation Provider** med teleporteringsytor, **Snap Turn Provider**, **Continuous Turn Provider** och **Continuous Move Provider**. **Locomotion Mediator** ser till att de inte krockar med varandra.

### Genomgånget exempel: välj förflyttning för en sport

Tänk att du gör minigolf, med flera hål på rad.

1. Vid varje hål ska spelaren stå still och koncentrera sig. Det ger stillastående spel.
2. Mellan hålen behöver spelaren flytta sig många meter. Att gå räcker inte i ett vanligt rum.
3. Mjuk förflyttning är riskabel för ovana. Teleportering till fasta punkter mellan hålen är säkrare.

Resultatet blir: stillastående vid varje hål och teleportering mellan dem. Sporten styr valet, inte vad som är roligast att programmera.

## Att hitta rätt i rummet i VR

Orientering behövs också i VR. Eftersom spelaren kan vända sig åt alla håll kan du inte räkna med att något syns bara för att det ligger i scenen. Placera viktiga saker ungefär i ögonhöjd och framför spelaren, och använd ljud för att rikta uppmärksamheten bakåt.

## Begrepp

- **Navigation:** orientering och förflyttning tillsammans.
- **Landmärke:** tydligt föremål som hjälper dig att hitta.
- **Normalisera:** göra en vektor längden 1 men behålla riktningen.
- **Vektion:** känslan av att röra sig utan att kroppen gör det.
- **Åksjuka (cybersickness):** illamående som orsakas av krock mellan syn och balans.
- **Teleportering:** direkt förflyttning till en utpekad plats.
- **Snap turn:** vridning i fasta steg.
- **Rumsskala:** spelaren rör sig fysiskt i ett avgränsat område.

## Koppling till projektet

I [3D-Spel](../projekt/3d-spel/README.md) bygger du spelarens rörelse, en kamera som följer spelaren och kollisioner. I [VR/AR - Projekt](../projekt/vr-ar/README.md) bygger du en sport där du väljer förflyttning med hänsyn till komforten.

## Läs mer

- [Meta: Locomotion Best Practices](https://developers.meta.com/horizon/design/locomotion-best-practices/)
- [XR Interaction Toolkit: Locomotion](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@3.2/manual/locomotion.html)
- [Godot: CharacterBody3D](https://docs.godotengine.org/en/stable/classes/class_characterbody3d.html)

[← Föregående](03-forstudie-och-projektplan.md) | [Innehåll](../README.md) | [Nästa →](05-interaktion-med-3d-objekt.md)
