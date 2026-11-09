# VR/AR - Projekt

## Syfte

I det här projektet bygger ni i grupp ett VR-spel med sporttema i Unity 6 för Meta Quest 3. Ni lär er hur en interaktiv 3D-miljö planeras, byggs och testas, och hur man utformar ett gränssnitt när spelarens kropp är en del av det.

En tydligt avgränsad sport som blir riktigt bra är bättre än en stor som aldrig blir klar. Exempel är bowling, dart, pingis och minigolf.

## Koppling till kursen

**Kriterier i vanliga ord**

| Kriterium | Vad det handlar om |
|---|---|
| 1. Projektplan | Ni gör en plan med problemformulering utifrån vad kunden vill, målgrupp och behov samt tekniska förutsättningar, och värderar planen. |
| 2. 3D och interaktivitet | Ni skapar 3D-objekt, gör navigation och interaktivitet i en virtuell miljö och kan redogöra för datakällor som ger användaren information. |
| 3. Design och tillgänglighet | Ni bearbetar gränssnittet enligt principer för visuell design och användbarhet, och gör det möjligt att uppfatta och använda också för personer med funktionsnedsättningar. |

Skolverkets kriterier finns i [kursplanen](../../kursplan.md).

**Centralt innehåll som behandlas**

- begrepp kring virtuell och förstärkt verklighet
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
| [1. Verkligheter att designa för](../../kapitel/01-vr-ar-och-plats.md) | Kursstarten |
| [2. Verktyg för 3D](../../kapitel/02-verktyg-for-3d.md) | Unity, C# och VR-stöd |
| [3. Förstudie och projektplan](../../kapitel/03-forstudie-och-projektplan.md) | Planeringen |
| [4. Navigation och förflyttning](../../kapitel/04-navigation-och-forflyttning.md) | Spelarens plats och komfort |
| [5. Interaktion med 3D-objekt](../../kapitel/05-interaktion-med-3d-objekt.md) | Grepp, kast och träffdetektion |
| [6. Modellering och texturer](../../kapitel/06-modellering-och-texturer.md) | 3D-miljön |
| [7. Text, ljud och datakällor](../../kapitel/07-text-ljud-och-datakallor.md) | UI, ljud och feedback |
| [8. Användbarhet och tillgänglighet](../../kapitel/08-anvandbarhet-och-tillganglighet.md) | Användartest |
| [9. Visuell design, stilguide och överlämning](../../kapitel/09-visuell-design-och-overlamning.md) | Färdigställande och bygge |
| [10. Vardagens datorer, etik och lagar](../../kapitel/10-vardagsdatorer-etik-och-lagar.md) | Assets och användartest |

## Vad du ska göra

- Installera Unity 6 med VR-stöd och lära dig grunderna i Unity och C#.
- Fylla i planeringsmallen med spelidé, skisser, kravlista, arbetsfördelning och tidsplan, och få den godkänd innan ni börjar koda spelet.
- Bygga sportmekaniken: grepp, fysik, träffdetektion, poängregler och vinst- och förlustvillkor.
- Skapa 3D-miljö, UI i World Space, ljud och haptisk feedback samt meny, omstart och resultatskärm.
- Testa på någon utanför gruppen, bygga en `.apk` och se till att alla har commits i repot.

## Krav och leverabler

De fullständiga kraven finns i [Virtual-Reality](https://github.com/abbjetmus/Virtual-Reality). Sammanfattat ska ni lämna:

| Del | Innehåll |
|---|---|
| Planering | Ifylld [planeringsmall](https://github.com/abbjetmus/Virtual-Reality/blob/main/PLANERING.md), godkänd innan ni börjar koda spelet |
| VR-grunder | XR Origin, synliga handkontroller, minst ett föremål som går att greppa, rimlig skala |
| Sportmekanik | Fysik, träffdetektion, tydliga regler och vinst- eller förlustvillkor |
| Grafik | 3D-modeller, material och texturer samt ljussättning anpassad för VR |
| UI i VR | Startmeny i World Space, poängtavla och game over-skärm med möjlighet att spela igen |
| Ljud och feedback | Ljudeffekter, bakgrundsljud och haptisk återkoppling |
| Spelflöde | Meny, spel och resultat samt omstart som återställer föremålen |
| Komfort och prestanda | Stabil bildfrekvens och ingen påtvingad kamerarörelse, testat på minst en person utanför gruppen |
| Samarbete | Commits från alla, branches och kommenterad kod |
| Bygge | En `.apk` som går att köra på headsetet utan Unity Editor |

Färdiga 3D-modeller, ljud och Unitys egna paket är okej, men ni måste redovisa var de kommer ifrån. Ett färdigt projekt från nätet får ni inte använda. Läs villkoren i [Virtual-Reality](https://github.com/abbjetmus/Virtual-Reality).

## Arbetsgång

Lektionerna är sammanslagna till faser.

| Lektion | Innehåll |
|---|---|
| 1 | Kursstart: introduktion till 3D, AR och VR och till projektet. Grupperna bildas i basgrupperna. |
| 2–4 | Installera Unity Hub och Unity 6 med Android Build Support och skapa ett URP-projekt. Unity-grunder: editorn, GameObjects, komponenter, scener och prefabs. C#-skript med `Start`, `Update`, `FixedUpdate` och kollisioner. |
| 5–6 | VR-stöd med XR Plug-in Management, OpenXR och XR Interaction Toolkit. Bygg VR-spelaren med XR Origin. Testa i headset och med simulator. Gör ett föremål greppbart med `XRGrabInteractable`. |
| 7–8 | Planering: välj sport, fyll i `PLANERING.md` med spelidé, skisser, spelmekanik, kravlista, arbetsfördelning och tidsplan. Lämna in för godkännande. |
| 9–12 | Sätt upp gruppens repo med Git LFS och branches. Bygg spelplanen i verklig skala. Grepp och kast med `Rigidbody` och colliders. Träffdetektion med kollisioner och triggers. Regelsystem för poäng. |
| 13–14 | 3D-miljö: modeller, material, texturer och ljussättning för VR. Eget arbete enligt tidsplanen och avstämning med läraren. |
| 15–16 | UI i VR: poängtavla i World Space och diskussion om vilka datakällor som kan ge spelaren information. Startmeny med Starta-knapp som går att trycka på med handkontrollen. |
| 17–18 | Ljud och feedback: ljudeffekter, spatialt 3D-ljud och haptisk feedback. Bakgrundsljud och fortsatt eget arbete. |
| 19–20 | Vinst- och förlustvillkor och game over-skärm. Spelflöde med meny, spel, resultat och omstart. Avstämning per grupp. |
| 21–22 | Komfort och prestanda. Bygg en första `.apk` och testa fristående i headsetet. |
| 23–24 | Användartest med någon utanför gruppen, och åtgärda feedbacken, särskilt tydlighet och användbarhet i UI:t. |
| 25–27 | Färdigställande: rätta buggar, kommentera koden, alla har commits. Putsa grafik, ljud och menyer. Bygg slutlig `.apk` och testa hela flödet. |
| 28 | Förbered mässan: hur spelet ska testas, vem som visar vad och ladda headseten. |
| 29–30 | Redovisning. |

## Bedömning

Spelet redovisas på en mässa där andra får testa det i headset. Bedömningen gäller er planering, de 3D-objekt, den navigation och interaktivitet ni skapar i VR-miljön, och hur väl gränssnittet är utformat så att det blir tydligt och användbart för spelaren.

Skolverkets kriterier omfattar också sådant som stilguide, dokumentation och integritet. Fråga läraren hur de delarna bedöms.

## Material

- [Virtual-Reality](https://github.com/abbjetmus/Virtual-Reality): krav, exempelkod och Git LFS
- [Planeringsmall](https://github.com/abbjetmus/Virtual-Reality/blob/main/PLANERING.md)
- [Videoserie om VR i Unity](https://www.youtube.com/playlist?list=PLpEoiloH-4eM15HYUXK_2a6rldDDx8FcF)
- [3D-AR-VR-Interface-Design](https://github.com/abbjetmus/3D-AR-VR-Interface-Design): Unity och C#
- [XR Interaction Toolkit](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@3.2/manual/index.html)

## Tips

- Testa i headsetet ofta, gärna efter varje ny mekanik.
- Bygg en `.apk` tidigt. Bygget brukar ge problem första gången.
- Bestäm vem som äger scenen just nu, och bygg funktioner som prefabs.
- Håll skalan verklig från början: 1 enhet i Unity är 1 meter.
- Be testaren göra en uppgift och var tyst medan hen försöker.
