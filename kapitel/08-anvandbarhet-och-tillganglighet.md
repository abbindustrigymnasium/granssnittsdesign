# Kapitel 8: Användbarhet och tillgänglighet

> **I det här kapitlet lär du dig**
> - vad människa–datorinteraktion, användbarhet och tillgänglighet är
> - hur kognitiv belastning påverkar en design
> - hur du räknar ut kontrast mellan text och bakgrund
> - hur du testar ditt gränssnitt på riktiga människor

Du har arbetat i veckor med ditt spel och vet precis vilken knapp som gör vad. Sedan sätter du headsetet på en kompis, och hon står stilla i tio sekunder och frågar "vad ska jag göra?". Det är inte hennes fel. Det är ett designproblem som du inte hade kunnat upptäcka själv, och det är därför det här kapitlet finns.

## Människa–datorinteraktion

**Människa–datorinteraktion** (HCI, *human–computer interaction*) är forskningsområdet om hur människor använder datorer och hur datorer bör utformas för människor. Det bygger på psykologi, design och datavetenskap.

**Användbarhet** beskrivs i standarden ISO 9241-11 ungefär så här: i vilken mån en produkt kan användas av bestämda användare för att nå bestämda mål på ett ändamålsenligt, effektivt och tillfredsställande sätt i ett bestämt sammanhang. Lägg märke till att användbarhet alltid beror på vem användaren är och vad hon ska göra.

| Del | Fråga att ställa |
|---|---|
| Ändamålsenlighet | Kan användaren nå målet? |
| Effektivitet | Hur mycket tid och ansträngning krävs? |
| Tillfredsställelse | Hur känns det? |

**Tillgänglighet** handlar om att så många som möjligt ska kunna använda produkten, också personer med funktionsnedsättningar.

## Principer för användbarhet

Jakob Nielsens tio tumregler, så kallade **heuristiker**, används mycket. Här är fem av dem i 3D-sammanhang:

| Princip | I ett 3D-spel |
|---|---|
| Visa systemets status | Spelaren ser att bollen är greppad, och poängen uppdateras |
| Följ verklighetens logik | Du greppar ett klot med greppknappen, inte med en menyknapp |
| Ge användaren kontroll | Det går att starta om och gå tillbaka |
| Var konsekvent | Samma knapp gör samma sak överallt |
| Förebygg fel | Det går inte att tappa bollen utanför banan utan att den kommer tillbaka |

**Konventioner** är vedertagna lösningar som användarna redan känner till. WASD för att gå, en stor Starta-knapp i menyn, grepp med kontrollens sidoknapp i VR. Följer du konventionerna behöver spelaren inte lära sig något nytt. Bryter du mot dem bör du ha ett bra skäl.

## Kognitiv belastning

**Kognitiv belastning** är hur mycket hjärnan måste arbeta för att förstå och använda något. Arbetsminnet räcker bara till några få saker samtidigt.

- Visa inte allt på en gång. Lägg vanliga val först och ovanliga längre in.
- Låt spelaren känna igen i stället för att komma ihåg. En ikon på kontrollen är bättre än en instruktion som lästes för tio minuter sedan.
- Lär ut en sak i taget. Börja med att greppa, sedan att kasta.

Det här är också en tillgänglighetsfråga. Lägre kognitiv belastning hjälper alla, och särskilt personer med till exempel lässvårigheter eller koncentrationssvårigheter.

## Tillgänglighet i praktiken

Webbens riktlinjer **WCAG** är den vanligaste standarden. Den utgår från fyra principer som är användbara också för spel:

| Princip | Betydelse | Exempel i 3D |
|---|---|---|
| Möjlig att uppfatta | Informationen kan tas in på mer än ett sätt | Ljud kompletteras med text eller bild |
| Möjlig att använda | Styrningen går att klara av | Går att spela sittande eller med en hand |
| Begriplig | Det går att förstå | Tydligt språk, förutsägbara menyer |
| Robust | Fungerar med olika hjälpmedel | Går att ändra knappar |

W3C har också skrivit **XR Accessibility User Requirements**, som tar upp behov i just XR. Några saker som är rimliga att tänka på i ett VR-spel är att kunna spela sittande, att kunna välja vilken hand man använder, att slippa snabba kamerarörelser, och att information inte bara ges med färg. Färgblindhet gör att röd och grön kan vara svåra att skilja åt, så använd också form eller text.

### Genomräknat exempel: kontrast

Kontrasten mellan två färger beräknas med deras **relativa luminans** L, ett tal mellan 0 (svart) och 1 (vit):

```
kontrast = (L_ljus + 0,05) / (L_mörk + 0,05)
```

WCAG kräver för nivån AA minst **4,5:1** för vanlig text och **3:1** för stor text. Här är tre beräkningar med vit text (L = 1,0):

| Bakgrund | Luminans | Beräkning | Kontrast | Resultat |
|---|---|---|---|---|
| Mörkblå `#1F4E79` | 0,0712 | 1,05 / 0,1212 | 8,66:1 | Godkänt |
| Grå `#808080` | 0,2159 | 1,05 / 0,2659 | 3,95:1 | Bara för stor text |
| Ljusblå `#7FB3D5` | 0,4156 | 1,05 / 0,4656 | 2,26:1 | Underkänt |

Grått ser ofta "tillräckligt" ut på din skärm men blir svårläst i ett headset eller på en projektor.

## Användartester

Det enda sättet att veta om något fungerar är att låta någon annan prova.

| Metod | Så går det till | Ger dig |
|---|---|---|
| **Uppgiftstest** | Testaren får en uppgift: "starta spelet och kasta" | Om uppgiften går att lösa |
| **Tänka högt** | Testaren berättar vad hon tänker | Varför något är svårt |
| **Observation** | Du tittar, tiden tas, fel räknas | Mätbara resultat |
| **Heuristisk utvärdering** | Du granskar mot tumreglerna | Problem du kan hitta utan testare |
| **Enkät** | Frågor efteråt | Hur upplevelsen var |

Några regler vid testning: Hjälp inte testaren, det är just tvekan du vill se. Säg att det är spelet som testas, inte hon. Fråga om lov innan du filmar eller skriver upp något, och spara inte mer än du behöver.

### Genomräknat exempel: System Usability Scale

**SUS** är en enkät med tio påståenden som besvaras från 1 (håller inte alls med) till 5 (håller helt med). Så här räknas poängen:

- Udda påståenden (1, 3, 5, 7, 9): svaret minus 1.
- Jämna påståenden (2, 4, 6, 8, 10): 5 minus svaret.
- Summera och multiplicera med 2,5. Resultatet är 0–100.

En testare svarar 4, 2, 5, 1, 4, 2, 4, 3, 4, 2.

```
Udda:  (4−1)+(5−1)+(4−1)+(4−1)+(4−1) = 3+4+3+3+3 = 16
Jämna: (5−2)+(5−1)+(5−2)+(5−3)+(5−2) = 3+4+3+2+3 = 15
SUS = (16 + 15) × 2,5 = 77,5
```

SUS är inget betyg i procent. Det blir mest användbart när du jämför två versioner av samma gränssnitt.

## Från test till åtgärd

Skriv ner varje problem, gradera hur allvarligt det är och fixa det viktigaste först. Att koppla resultatet till teori är också en del av betygskriterierna: du ska kunna säga att spelaren fastnade för att systemets status inte syntes, inte bara att spelaren fastnade.

## Begrepp

- **HCI:** människa–datorinteraktion, forskningsområdet om hur människor och datorer samverkar.
- **Användbarhet:** hur väl en produkt låter en bestämd användare nå sitt mål.
- **Tillgänglighet:** att produkten kan användas av så många som möjligt.
- **Heuristik:** tumregel för att bedöma en design.
- **Konvention:** lösning som användarna redan känner till.
- **Kognitiv belastning:** hur mycket hjärnan måste arbeta.
- **WCAG:** riktlinjer för tillgänglig webb.
- **SUS:** enkät som ger ett användbarhetsvärde mellan 0 och 100.

## Testa dig själv

1. Vilka tre delar ingår i användbarhet enligt ISO 9241-11?
2. Vad är skillnaden mellan användbarhet och tillgänglighet?
3. Ge två exempel på konventioner i spel.
4. Hur minskar du kognitiv belastning i en startmeny?
5. Varför ska information inte bara ges med färg?
6. Varför ska du inte hjälpa testaren?
7. Hur kan du använda ett SUS-värde?

## Koppling till projektet

I [VR/AR - Projekt](../projekt/vr-ar/README.md) låter ni någon utanför gruppen testa spelet och åtgärdar sedan feedbacken. I [3D-Spel](../projekt/3d-spel/README.md) låter du klasskamrater testa och förbättrar sedan tillgängligheten, till exempel kontrast, textstorlek och kontroller.

## Läs mer

- [Nielsens tio heuristiker](https://www.nngroup.com/articles/ten-usability-heuristics/)
- [Thinking aloud](https://www.nngroup.com/articles/thinking-aloud-the-1-usability-tool/)
- [WCAG 2.2](https://www.w3.org/TR/WCAG22/)
- [XR Accessibility User Requirements](https://www.w3.org/TR/xaur/)
- [Game Accessibility Guidelines](https://gameaccessibilityguidelines.com/)
- [System usability scale på Wikipedia](https://en.wikipedia.org/wiki/System_usability_scale)

[← Föregående](07-text-ljud-och-datakallor.md) | [Innehåll](../README.md) | [Nästa →](09-visuell-design-och-overlamning.md)
