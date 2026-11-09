# 3D-Spel

## Syfte

I det här projektet utvecklar du individuellt ett valfritt 3D-spel i Godot med GDScript. Du lär dig hur man skapar en tredimensionell miljö som spelaren kan navigera och interagera i, med ett gränssnitt som är tydligt och lätt att använda.

## Koppling till kursen

**Kriterier i vanliga ord**

| Kriterium | Vad det handlar om |
|---|---|
| 1. Projektplan | Du gör en plan med problemformulering utifrån kundönskemål, målgrupp och behov samt tekniska förutsättningar, och värderar planen. |
| 2. 3D och interaktivitet | Du skapar 3D-objekt, gör navigation och interaktivitet i en virtuell miljö och redogör för datakällor som ger användaren information. |
| 3. Design och tillgänglighet | Du bearbetar gränssnittet enligt principer för visuell design och användbarhet och gör det möjligt att uppfatta och använda också för personer med funktionsnedsättningar. |

Skolverkets kriterier finns i [kursplanen](../../kursplan.md).

**Centralt innehåll som behandlas**

- förstudie, tekniska förutsättningar och mål
- genomförande av ett gränssnittsdesignprojekt, med skisser, prototyp och test
- datorstöd för projekthantering
- utvecklingsverktyg för 3D, modellering och texturer
- samverkan mellan 3D-miljö, text och ljud
- HCI, användbarhet och tillgänglighet
- navigation, förflyttning och interaktion med 3D-objekt

**Kapitel som förbereder**

| Kapitel | Används när |
|---|---|
| [2. Verktyg för 3D](../../kapitel/02-verktyg-for-3d.md) | Projektstart och repetition av Godot |
| [3. Förstudie och projektplan](../../kapitel/03-forstudie-och-projektplan.md) | Projektplanen |
| [4. Navigation och förflyttning](../../kapitel/04-navigation-och-forflyttning.md) | Rörelse, kamera och banans utformning |
| [5. Interaktion med 3D-objekt](../../kapitel/05-interaktion-med-3d-objekt.md) | Kollisioner, mål och samlarföremål |
| [6. Modellering och texturer](../../kapitel/06-modellering-och-texturer.md) | 3D-grafik |
| [7. Text, ljud och datakällor](../../kapitel/07-text-ljud-och-datakallor.md) | Startmeny, HUD och ljud |
| [8. Användbarhet och tillgänglighet](../../kapitel/08-anvandbarhet-och-tillganglighet.md) | Användartest och tillgänglighet |
| [9. Visuell design, stilguide och överlämning](../../kapitel/09-visuell-design-och-overlamning.md) | Export och Git LFS |

## Vad du ska göra

Du får återskapa ett känt spel eller hitta på ett eget, men du får inte hämta färdig kod från nätet.

- Gå igenom Godots tutorial för ditt första 3D-spel.
- Skriva en projektplan med spelidé, målgrupp, skisser, kravlista och tekniska förutsättningar, och få den godkänd.
- Bygga spelet: 3D-modeller och material, rörelse, kamera, kollisioner, mål och vinst- och förlustvillkor.
- Skapa startmeny, HUD och game over-skärm samt ljud, scenbyten och respawn.
- Testa spelet på andra, förbättra det och exportera det till en `.exe`-fil.

## Krav och leverabler

De fullständiga kraven finns i [Godot-3D-Spel](https://github.com/abbjetmus/Godot-3D-Spel). Sammanfattat:

| Del | Innehåll |
|---|---|
| Planering | Dokument med beskrivning och skiss, godkänt av läraren |
| Grundläggande spelmekanik | Rörelse, kollisioner, kamera, ett mål samt vinst- och förlustvillkor |
| 3D-grafik | Modeller för spelare, miljö och fiender, texturer och enkla animationer |
| Användargränssnitt | Startskärm, game over-skärm, gärna HUD |
| Ljud och musik | Ljudeffekter och bakgrundsmusik |
| Spelelement | Enkel fiendeförflyttning, samlarföremål, enkel fysik |
| Scenhantering | Scenövergångar och respawn eller återställning |
| Bygge | `.exe`-fil som andra kan köra |

## Arbetsgång

| Lektion | Innehåll |
|---|---|
| 1 | Projektstart: genomgång av projektet och kraven. Repetition av Godot med noder och scener i 3D (`Node3D`, `Camera3D`). |
| 2 | Starta tutorialen Your first 3D game och få en spelare som rör sig i en 3D-scen. |
| 3–8 | Lektionerna är inte detaljplanerade. Läraren anger innehållet. Enligt projektets gång ska tutorialen vara klar och projektplanen godkänd innan du bygger grundmekaniken. |
| 9 | Bygg grundmekaniken: spelarens rörelse, en kamera som följer spelaren och kollisioner. |
| 10 | 3D-grafik: bygg miljön med 3D-modeller, material och texturer, egna enkla former eller assets. |
| 11 | Inte detaljplanerad. Läraren anger innehållet. |
| 12 | Gränssnitt: startmeny, HUD och game over-skärm. Fundera på vilken information spelaren behöver och var den kommer ifrån. |
| 13 | Eget arbete: fiender som patrullerar eller jagar och enkel fysik som hopp och fall. Avstämning med läraren. |
| 14 | Ljud och spelflöde: ljudeffekter, bakgrundsmusik, scenövergångar och respawn. |
| 15 | Användartest: låt klasskamrater testa ditt spel och anteckna deras feedback om tydlighet och användbarhet. |
| 16 | Åtgärda feedbacken och förbättra tillgängligheten, till exempel kontrast, textstorlek och kontroller. Värdera din projektplan. |
| 17 | Färdigställ spelet: exportera till `.exe`, pusha till ditt projektrepo med Git LFS och förbered mässan. |
| 18 | Redovisning: mässa där ni testar och ger feedback på varandras spel. |

## Bedömning

Spelet redovisas på en mässa där ni testar varandras spel. Bedömningen gäller din projektplan och hur du värderar den, dina 3D-objekt och hur navigation och interaktivitet fungerar, samt hur du arbetat med visuell design, användbarhet och tillgänglighet i gränssnittet.

Skolverkets kriterier omfattar också sådant som stilguide, dokumentation och integritet. Fråga läraren hur de delarna bedöms.

## Material

- [Godot-3D-Spel](https://github.com/abbjetmus/Godot-3D-Spel): guide, krav och Git LFS
- [Godot Docs: Your first 3D game](https://docs.godotengine.org/en/stable/getting_started/first_3d_game/index.html)
- [Exportera för Windows](https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_windows.html)
- [Godot-VR-AR](https://github.com/abbjetmus/Godot-VR-AR): om du vill prova VR i Godot. Repots länk går till en äldre version av dokumentationen. Aktuell information finns i [Godots XR-dokumentation](https://docs.godotengine.org/en/stable/tutorials/xr/index.html).

## Tips

- Kursens guide har kodexempel skrivna för en äldre version av Godot. I Godot 4 heter noden `CharacterBody3D`, se [kapitel 4](../../kapitel/04-navigation-och-forflyttning.md).
- Gråboxa banan först och byt ut formerna när spelkänslan sitter.
- Sätt upp Git LFS innan du lägger till stora filer.
- Be testaren göra en uppgift och var tyst medan hen försöker.
