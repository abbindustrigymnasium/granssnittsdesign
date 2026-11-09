# Kapitel 6: Modellering och texturer

> **I det här kapitlet lär du dig**
> - hur en 3D-modell är uppbyggd
> - vad texturer och material gör
> - hur du räknar på vad en textur kostar i minne
> - varför ljussättningen ofta avgör hur en scen upplevs
> - när du får använda andras modeller och ljud

Ett klot i ett bowlingspel ser ut att vara runt. Det är det inte. Det består av hundratals platta trianglar, en bild som är lindad runt dem och en beräkning av hur ljus studsar mot ytan. När du förstår de tre delarna kan du förklara varför ett spel ser ut som det gör, och varför det ibland går långsamt.

## Från punkter till modell

En 3D-modell är i grunden en samling punkter i rummet.

| Del | Förklaring |
|---|---|
| **Hörn** (*vertex*) | En punkt med position (x, y, z) |
| **Kant** (*edge*) | En linje mellan två hörn |
| **Yta** (*face*) | En platt yta mellan kanterna, ofta en triangel |
| **Mesh** | Hela nätet av hörn, kanter och ytor |
| **Normal** | En riktning som talar om åt vilket håll ytan är vänd |

Grafikkortet ritar i praktiken trianglar. Ju fler trianglar, desto mer detaljerad form men också mer arbete per bild. Lågpolygonmodeller (*low poly*) använder få trianglar och passar därför bra på fristående headset, och de ger dessutom en tydlig stil.

## Sätt att skaffa modeller

| Metod | Fördel | Nackdel |
|---|---|---|
| Inbyggda former (kub, sfär, plan) | Snabbt | Enkelt utseende |
| Bygga i motorn (CSG i Godot, ProBuilder i Unity) | Du blockar ut en bana direkt i scenen | Passar inte för detaljerade figurer |
| Modellera i Blender | Full kontroll | Tar tid att lära sig |
| Hämta färdiga assets | Sparar tid | Du måste kontrollera licens och stil |

Ett bra arbetssätt är att först bygga banan med enkla former, så kallad **gråboxning**, och kontrollera att måtten och spelkänslan fungerar. Sedan byter du ut formerna mot snygga modeller. Det kostar mycket mindre att flytta en grå låda än en färdig modell.

Vanliga filformat är `.glb`/`.gltf` och `.fbx`. Godot hanterar glTF särskilt väl.

## Texturer och material

En **textur** är en bild som läggs på en modell. För att veta var på ytan varje del av bilden hamnar används **UV-koordinater**. Tänk dig att du klipper upp en kartong och lägger den platt, så att du kan måla på den. UV är en sådan utvikning av modellen.

Ett **material** beskriver hur ytan beter sig mot ljus. Dagens motorer använder oftast **PBR** (fysikaliskt baserad rendering), där du ställer in egenskaper som liknar verkliga ytor:

| Egenskap | Betyder | Unity URP | Godot |
|---|---|---|---|
| Grundfärg | Ytans färg utan ljus | Base Map | Albedo |
| Metall | Hur mycket ytan beter sig som metall | Metallic | Metallic |
| Ytjämnhet | Blank eller matt | Smoothness (högt = blankt) | Roughness (högt = matt) |
| Normalkarta | Bild som ger intryck av små ojämnheter | Normal Map | Normal Map |

Lägg märke till att Unity och Godot använder motsatta skalor för ytjämnhet.

## Genomräknat exempel: vad kostar en textur?

Tänk dig en textur på 2048 × 2048 bildpunkter med fyra kanaler (röd, grön, blå, genomskinlighet) på 8 bitar var, alltså 4 byte per bildpunkt.

```
2048 × 2048 = 4 194 304 bildpunkter
4 194 304 × 4 byte = 16 777 216 byte = 16 MiB
```

Motorn sparar dessutom mindre versioner av bilden, **mipmaps**, för föremål långt bort. De lägger till ungefär en tredjedel:

```
16 MiB × 4/3 ≈ 21,3 MiB
```

Med **ASTC**, ett komprimeringsformat som används på Quest, kan du välja hur hård komprimeringen ska vara. Med blockstorleken 6 × 6 använder ASTC 128 bitar för varje block på 36 bildpunkter:

```
128 / 36 ≈ 3,56 bitar per bildpunkt
4 194 304 × 3,56 / 8 ≈ 1,78 MiB (ungefär 2,37 MiB med mipmaps)
```

Det är ett skäl till att kursens krav säger att Texture Compression ska vara ASTC. Skillnaden är ungefär en faktor nio.

Halveras sidorna till 1024 × 1024 minskar minnet till en fjärdedel. Det är ofta det enklaste sättet att spara minne på, och i många fall syns ingen skillnad.

## Ljus

Ljus bestämmer stämningen, men det kan också vara det dyraste i din scen.

- **Realtidsljus** beräknas varje bild och kan följa rörliga föremål. Det är dyrt.
- **Förberäknat ljus** (*baked lighting*) räknas ut en gång och sparas i texturer, så kallade **lightmaps**. Det är billigt under körning, men fungerar bara för saker som inte rör sig.

I VR-projektet är förberäknat ljus att föredra. Det motsvarande verktyget i Godot heter `LightmapGI`.

Tänk också på vad ljuset gör för förståelsen. Ett ljust område i en mörk hall drar blicken dit du vill ha spelaren, vilket hjälper orienteringen. Skuggor under föremål hjälper också hjärnan att bedöma var saker står.

## Prestanda: draw calls och detaljnivå

Varje gång motorn säger åt grafikkortet att rita något kallas det ett **draw call**. Många små föremål med olika material ger många draw calls. Slå därför gärna ihop saker och återanvänd material.

**Detaljnivå** (*level of detail*, LOD) innebär att modellen byts mot en enklare version när den är långt bort, eftersom ingen ändå ser skillnaden.

## Andras modeller och ljud

Du får bara använda något som någon annan skapat om licensen tillåter det. Det gäller också sådant som är gratis att ladda ner. Vanliga licenser:

| Licens | Vad du får göra |
|---|---|
| **CC0** | I princip vad du vill, utan krav på att nämna upphovspersonen |
| **CC BY** | Använda, men du måste ange vem som skapat verket |
| **CC BY-NC** | Bara icke-kommersiellt, och du måste ange vem som skapat verket |
| **Asset Store-licens** | Enligt butikens villkor |

Kursens krav är att du redovisar varifrån dina assets kommer. Skriv upp källa och licens direkt när du laddar ner, annars glömmer du. Läs mer om upphovsrätten i [kapitel 10](10-vardagsdatorer-etik-och-lagar.md).

Bra platser att leta på är [Kenney](https://kenney.nl/assets), [Poly Pizza](https://poly.pizza/), [Freesound](https://freesound.org/), [Unity Asset Store](https://assetstore.unity.com/) och [Godot Asset Library](https://godotengine.org/asset-library/asset). Kontrollera licensen för varje enskild fil.

## Begrepp

- **Mesh:** nätet av hörn, kanter och ytor som bildar en modell.
- **Low poly:** modell med få trianglar.
- **Gråboxning:** att bygga banan med enkla former först.
- **Textur:** bild som läggs på en modell.
- **UV-koordinater:** utvikning som talar om var texturen hamnar.
- **PBR:** material som efterliknar hur ljus beter sig mot verkliga ytor.
- **Mipmap:** mindre version av en textur.
- **ASTC:** format för att komprimera texturer.
- **Lightmap:** förberäknat ljus sparat i en textur.
- **Draw call:** instruktion till grafikkortet att rita något.
- **LOD:** enklare versioner av en modell på avstånd.

## Testa dig själv

1. Vad är skillnaden mellan en mesh och ett material?
2. Vad används UV-koordinater till?
3. Varför är high poly-modeller ett problem på ett fristående headset?
4. Vad händer med minnet om du halverar sidorna på en textur?
5. Vad är skillnaden mellan realtidsljus och förberäknat ljus?
6. Vad betyder CC BY, och vad måste du göra då?
7. Varför är gråboxning värt besväret?

## Övningar

**Grund.** Skapa ett material i Unity eller Godot. Ändra grundfärgen och ytjämnheten och beskriv vad som händer med en kula i scenen.

**Vidare.** En textur är 1024 × 1024 bildpunkter och har 4 byte per bildpunkt. Hur många MiB är den okomprimerad? Hur mycket blir det med mipmaps?

<details><summary>Svar</summary>

1024 × 1024 × 4 = 4 194 304 byte = 4 MiB. Med mipmaps ungefär 4 × 4/3 ≈ 5,33 MiB.

</details>

**Utmaning.** Räkna ut minnet för en textur på 2048 × 2048 med ASTC 4 × 4 och ASTC 8 × 8. Blocken är alltid 128 bitar. Vad vinner du och vad förlorar du om du väljer 8 × 8?

<details><summary>Svar</summary>

4 × 4: 128 / 16 = 8 bitar per bildpunkt, alltså 4 194 304 × 8 / 8 = 4 MiB. 8 × 8: 128 / 64 = 2 bitar per bildpunkt, alltså 1 MiB. Med 8 × 8 sparar du minne, men bilden får sämre kvalitet.

</details>

## Koppling till projektet

I [VR/AR - Projekt](../projekt/vr-ar/README.md) skapar ni 3D-miljön med modeller, material, texturer och ljussättning anpassad för VR, och redovisar var era assets kommer ifrån. I [3D-Spel](../projekt/3d-spel/README.md) bygger du en bana med 3D-modeller, material och texturer. Egna enkla former duger bra.

## Läs mer

- [Godot: Standard Material 3D](https://docs.godotengine.org/en/stable/tutorials/3d/standard_material_3d.html)
- [Blender](https://www.blender.org/)
- [Creative Commons: om licenserna](https://creativecommons.org/share-your-work/cclicenses/)

[← Föregående](05-interaktion-med-3d-objekt.md) | [Innehåll](../README.md) | [Nästa →](07-text-ljud-och-datakallor.md)
