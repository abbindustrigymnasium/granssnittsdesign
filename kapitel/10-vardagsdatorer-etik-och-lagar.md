# Kapitel 10: Vardagens datorer, etik och lagar

> **I det här kapitlet lär du dig**
> - vad ubicomp är och hur det syns i vardagen
> - vilka integritetsfrågor plats och sensorer väcker
> - hur etik påverkar designbeslut
> - vilka lagar som är viktigast för den som bygger gränssnitt

Hur många datorer har du använt i dag? Telefonen, förstås. Men också klockan, bussens kortläsare, skolans dörr, kassan i affären, bilens instrumentpanel. Du märkte de flesta inte ens. Precis det är poängen med det här kapitlet: datorer finns numera i bakgrunden, och den som utformar deras gränssnitt har makt över andras vardag.

## Ubicomp: datorer som försvinner in i vardagen

**Ubicomp**, av engelskans *ubiquitous computing*, betyder datorer som finns överallt. Begreppet förknippas med forskaren Mark Weiser, som i en känd artikel 1991 beskrev en framtid där tekniken smälter in i vardagen så att vi slutar tänka på den.

| Exempel | Inmatning | Utmatning |
|---|---|---|
| Smartklocka | Puls, rörelse, tryck | Vibration, liten skärm |
| Röstassistent | Tal | Tal |
| Passersystem | Kort, telefon | Lampa, ljud, lås |
| Bilens förarstöd | Kameror, radar | Ljud, ratten vibrerar |
| VR-headset | Huvud, händer, kameror | Bild, ljud, vibration |

I ett sådant system finns ofta ingen skärm, och användaren har inte valt att "börja använda en dator". Det ställer höga krav på att systemet är begripligt, och på att det går att stänga av. Ett gränssnitt kan vara en lampa som lyser grönt, och då måste du fundera på vad den betyder för en färgblind person.

## Integritet

**Integritet** är rätten att bestämma över sina egna uppgifter och att få vara ifred. Tekniken i den här kursen är särskilt känslig eftersom den samlar in data om kroppen och omgivningen.

| Datatyp | Vad den kan avslöja |
|---|---|
| Plats | Var du bor, går i skolan och vilka du träffar |
| Kameror i headset | Hur ditt hem ser ut och vilka som finns där |
| Rörelsedata | Hur du rör dig, vilket kan säga något om din kropp |
| Röst | Vem du är och hur du mår |
| Användningsmönster | När du är vaken, vad du gillar |

Tjänster utformade efter geografisk kontext är ett tydligt exempel. En app som vet var du är just nu ger nytta, men en historik över var du varit under ett år är en mycket detaljerad bild av ditt liv.

Tänk också på **dem som inte valt att vara med**. Den som bär AR-glasögon med kamera kan fånga människor i omgivningen, utan att de har sagt ja.

Bra principer i designen:

- **Samla bara in det du behöver.** Behövs inte platsen, fråga inte efter den.
- **Spara så kort tid som möjligt.**
- **Bearbeta lokalt** i apparaten när det går.
- **Var tydlig** med vad som samlas in och varför, när det är relevant för användaren.
- **Ge kontroll**, till exempel ett enkelt sätt att stänga av eller radera.

## Etik

Lagen sätter gränsen för vad du måste göra. Etiken handlar om vad du borde göra. Några frågor som är relevanta för den här kursen:

- **Manipulerande design** (*dark patterns*): gränssnitt som lurar användaren, till exempel en "Avsluta prenumeration"-knapp som är gömd.
- **Beroendeskapande design:** belöningar som är gjorda för att du inte ska kunna sluta.
- **Trygghet i VR:** i sociala VR-miljöer kan trakasserier upplevas mer påträngande än på en skärm. Det är en anledning till att sådana miljöer ofta har funktioner för att hålla andra på avstånd.
- **Utestängning:** om en lösning kräver dyr utrustning eller god syn och hörsel, vem hamnar då utanför?
- **Fysiska risker:** en spelare med headset ser inte möbler eller människor i rummet, och kan bli illamående.

Ett enkelt sätt att granska ett designbeslut är att fråga sig: *Skulle jag vilja att det här gjordes mot mig?* Och: *Hade jag kunnat förklara det här beslutet öppet för användaren?*

## Lagar och andra bestämmelser

Här är de regler som oftast berör den som bygger digitala gränssnitt i Sverige. Lagar ändras, så kontrollera alltid vad som gäller när du arbetar med en verklig produkt.

| Regel | Vad den handlar om | Exempel i din design |
|---|---|---|
| **Dataskyddsförordningen (GDPR)** | Hur personuppgifter får behandlas | Du behöver en laglig grund för att spara spelarens namn och plats på en server |
| **Lag (2018:218)** med kompletterande bestämmelser till GDPR | Bland annat åldersgränsen 13 år för barns samtycke till informationssamhällets tjänster | Tjänster riktade till barn under 13 kräver vårdnadshavares samtycke om samtycke används som grund |
| **Upphovsrättslagen (1960:729)** | Skydd för verk som bilder, musik, texter och program | Du får inte använda modeller och ljud utan tillåtelse |
| **Lag (2018:1937) om tillgänglighet till digital offentlig service** | Offentliga webbplatser och appar ska vara tillgängliga | En kommuns app måste följa kraven |
| **Lag (2023:254) om vissa produkters och tjänsters tillgänglighet** | Krav på tillgänglighet för vissa produkter och tjänster, gäller sedan den 28 juni 2025 | Berör till exempel e-handel och banktjänster |
| **Diskrimineringslagen (2008:567)** | Skydd mot diskriminering, bland annat genom bristande tillgänglighet | Ställer krav på den som erbjuder varor och tjänster i vissa sammanhang |

GDPR gäller när du hanterar **personuppgifter**, det vill säga uppgifter som kan kopplas till en levande person. Det är mer än namn och personnummer. En plats, en bild eller ett användarnamn kan vara en personuppgift.

Några centrala tankar i GDPR är att det måste finnas ett tydligt ändamål, att du inte får samla in mer än du behöver, och att människor har rätt till information om vad som sparas om dem. [Integritetsskyddsmyndigheten](https://www.imy.se/privatperson/dataskydd/introduktion-till-gdpr/) förklarar reglerna på svenska.

### Genomgånget exempel: granska en AR-app

Tänk dig en AR-app som visar historiska byggnader i din stad och samlar in plats, kamerabild och ett användarnamn för en topplista.

| Fråga | Svar |
|---|---|
| Vad samlas in? | Plats, kamerabild, användarnamn |
| Är det personuppgifter? | Ja, platsen och namnet kan kopplas till en person |
| Behövs allt? | Plats behövs för att visa rätt byggnad, men inte att sparas efteråt. Kamerabilden kan behandlas i telefonen. |
| Målgrupp? | Om barn använder appen krävs extra omsorg |
| Tredje man? | Andra människor kan finnas i kamerabilden, därför ska bilden inte sparas |
| Ändring | Spara inte plats och bild. Låt topplistan använda ett självvalt smeknamn. |

Designen blir bättre av granskningen. Den blir enklare, och risken blir mindre.

## Begrepp

- **Ubicomp:** datorer som finns överallt och smälter in i vardagen.
- **Integritet:** rätten att bestämma över sina egna uppgifter.
- **Personuppgift:** uppgift som kan kopplas till en levande person.
- **GDPR:** EU:s dataskyddsförordning.
- **Dark pattern:** gränssnitt som är utformat för att lura användaren.
- **Upphovsrätt:** skydd för den som skapat ett verk.
- **Tredje man:** någon som berörs utan att själv vara användare.

## Koppling till projektet

Du tillämpar det här när du väljer assets och redovisar källa och licens i [VR/AR - Projekt](../projekt/vr-ar/README.md) och [3D-Spel](../projekt/3d-spel/README.md). Du använder det också när du användartestar: fråga om lov och spara inte mer än du behöver. Kapitlets vardagsexempel kan också vara bakgrund till [Spetsteknikens livscykel](../projekt/spetsteknikens-livscykel/README.md).

## Läs mer

- [IMY: Introduktion till GDPR](https://www.imy.se/privatperson/dataskydd/introduktion-till-gdpr/)
- [Lag (2018:218) med kompletterande bestämmelser till EU:s dataskyddsförordning](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/lag-2018218-med-kompletterande-bestammelser_sfs-2018-218/)
- [Upphovsrättslagen](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/lag-1960729-om-upphovsratt-till-litterara-och_sfs-1960-729/)
- [Lag (2018:1937) om tillgänglighet till digital offentlig service](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/lag-20181937-om-tillganglighet-till-digital_sfs-2018-1937/)
- [Lag (2023:254) om vissa produkters och tjänsters tillgänglighet](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/lag-2023254-om-vissa-produkters-och-tjansters_sfs-2023-254/)
- [Diskrimineringslagen](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/diskrimineringslag-2008567_sfs-2008-567/)
- [Ubiquitous computing på Wikipedia](https://en.wikipedia.org/wiki/Ubiquitous_computing)

[← Föregående](09-visuell-design-och-overlamning.md) | [Innehåll](../README.md)
