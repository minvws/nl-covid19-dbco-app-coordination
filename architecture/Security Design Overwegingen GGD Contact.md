
# GGD Contact crypto / security informatie
Datum: 17 december 2020
Auteur: Mendel Mobach
Versie: 1.3
Status: Request for Comment - Needs translation.

Deze versie is niet de finale versie, er is expliciet de mogelijkheid
tot commentaar.

*Table 1: Versie historie*
| Versie | Datum | Auteur | Samenvatting | 
|--|--|--|--|
| 0.0 | 2020-10-16 | MM | |
| 0.1 | 2020-10-20 | MM | Commentaar BW verwerkt |
| 0.2 | 2020-10-22 | MM | |
| 0.9 | 2020-10-26 | MM | Commentaar DWG verwerkt |
| 1.0 | 2020-11-02 | MM | Encryptie data toegevoegd |
| 1.1 | 2020-11-11 | MM | In overleg lengte codes en geldigheid aangepast |
| 1.2 | 2020-12-17 | MM | Koppelingscodes aangepast aan de realtiteit. Release.
| 1.3 | 2020-12-18 | MM | MD formaat.

Met dank aan:
- Brenno de Winter
- Dirk-Willem van Gulik
- Ivo Jansch
- Jeen de Swart
- Joris Leker
- Peter Verhage
- Friso van der Kreeft
et. al.

## Definities
**App, applicatie**: Het programma wat de patiënt of mogelijk patiënt
installeert.

**Device**: Apparaat van de gebruikers

**Client**: Device

**Sluis**: Inkomende verkeers-portaal gekoppeld aan het internet.

**Backend**: Niet aan het internet gekoppeld portaal en data services
voor de GGD toegankelijk, haalt data op en bezorgt data op de sluis.

**Authenticatie**: Bewijzen van identiteit

## Koppelingen
In het telefonische BCO gesprek dat de GGD medewerker voert met een
patiënt wordt er volgens de geldende procedure gecontroleerd of de
medewerker de juiste persoon aan de lijn heeft. Op dit moment gebeurt
dat door het verifiëren van de naam en de geboortedatum.

Daarna zijn er in het algemeen zijn er 2 mogelijkheden om een koppeling
te maken:

1.  Een GGD medewerker ontvangt ‘iets’ van een patiënt en voert dat in
2.  Een patiënt voert iets in wat ontvangen is van de GGD medewerker

De 1^e^ weg is zoals het ook werkt bij de corona-melder app. Een
gebruiker krijgt een code op het scherm en leest deze voor aan de GGD
medewerker.

Dit hoeft niet perse een code te zijn die voorgelezen wordt, technisch
kan dit op vele manieren worden gedaan die allemaal voor en nadelen
hebben. Afbeeldingen met QR-codes of zelfs dierenplaatjes zouden ook
kunnen. De technische beperkingen zijn vooral gebonden aan hoe een code
snel, efficiënt en effectief zonder te veel fouten overgedragen kan
worden.

De 2^e^ weg heeft dezelfde mogelijkheden, en is op dezelfde manier
beperkt. Het grootste nadeel hiervan is dat een derde via internet kan
proberen heel veel codes op te sturen en hoopt dat er daarvan 1 of
meerdere worden opgepakt in het proces.

Via de 1^e^ weg kan een patiënt proberen om meerdere codes door te
geven, maar dat zal na een paar echt wel stoppen omdat er arbeid van een
mens aan te pas komt.

### Verschillende methodes van authenticatie
Praktisch zijn er een paar methoden die realistisch lijken:

 1. QR codes, hiervoor moet er een plaatje met een camera worden uitgewisseld, ondanks dat telefoons tegenwoordig deze hardware bezitten en het niet heel moeilijk is is de kans groot dat dit beter werkt als mensen fysiek bij elkaar in buurt zijn (wat in deze corona tijd niet ideaal is). En tevens is dit process relatief afhankelijk van telefoons met (goed) werkende camera’s (wat in bepaalde delen van de samenleving op gespannen voet staat met het dagelijks werk). 
2. Andere plaatjes: hiervoor zal een beschrijving van deze afbeeldingen uitgewisseld moeten worden. Gezien de use-case is dat de gebruiker zelf dingen intypt op de telefoon kan er vanuit gegaan worden dat de 26 plaatjes van het alfabet ook werken.
3. Telefonisch letters doorgeven: Zoals ook gebruikt bij de corona-app. Wel is het zo dat hoe meer letters je gebruikt hoe veiliger en hoe moeilijker het wordt. Idealiter wil je deze code zo klein mogelijk houden om fouten te voorkomen.
4. SMS / E-mail / App: Out-of-band communicatie wordt dit ook wel genoemd, SMS is inherent onveilig, E-mail is soms traag en bij minder mensen aanwezig op hun telefoon. En qua Apps is het landschap van apps zo versnipperd en afhankelijk van externe factoren qua veiligheid dat dit niet een veel gebruikte manier is. Daarbij is het vervelend dat SMS en E-mail relatief ‘stabiele’ identifiers introduceren die een risico  zijn voor de privacy; en vrij zichtbaar zijn voor derden 'en-route’. Dit laatste betekent dat er zeer goede redenen moeten zijn om SMS/E-mail te gebruiken - en dat het niet anders goed kan.

### Levensduur codes
Het is wenselijk vanuit beveiligingsoogpunt om codes zo kort als mogelijk geldig te laten zijn.

Dit beperkt de kans op misbruik omdat de tijdspanne waarin een code onderschept kan worden en misbruikt kan worden veel korter is. Als de code korte tijd geldig is de kans op misbruik via (per ongeluk) lekken (copy-paste, e-mail, verkeerd doorsturen, foto’s etc..) logaritmisch kleiner omdat er aan de ontvangende kant veel sneller actie op
ondernomen zou moeten worden.

Wel is het zo dat hoe korter de codes geldig zijn hoe directer er door de invoerder actie ondernomen zal moeten worden.

Praktisch is een code die door iemand wordt voorgelezen en direct wordt ingevoerd in het systeem meestal slechts zeer korte tijd nodig. (Aanmaken - voorlezen – invoeren – valideren).

Een code die wordt meegegeven om later gebruikt te worden zal vele malen langer gebruikt moeten kunnen worden en daarmee ligt misbruik op de loer. (Praktisch: iemand post een foto van de code op twitter/facebook).

### Mogelijke misbruikscenario’s
Indien de patiënt een code voorleest aan de medewerker kan dit ook geprobeerd worden andere codes te forceren om een ander dossier van foute informatie te voorzien. Gezien hier dan een menselijke handeling aan te pas komt is de doorloopsnelheid van deze actie ‘traag’ in verhouding met geautomatiseerde aanvallen en is de mogelijkheid om dit vaak te proberen beperkt door de welwillendheid van de medewerker.

Indien de patiënt een code invult om deze te valideren tegen een backend kan dit door een bad-actor geautomatiseerd worden. Hier zijn verschillende migraties op mogelijk zoals codes van een controlegetal te voorzien (checksum), maar ook door bijvoorbeeld elke code aan te nemen.

Indien elke code wordt aangenomen kan nog steeds door een bad-actor een heleboel foute data het systeem in worden gezonden en kan deze hopen dat deze data wordt overgenomen. Hoe minder deze 2^e^ weg gebruikt wordt hoe moeilijker het wordt om deze data ook echt bij een medewerker te laten verschijnen.

### Wenselijk oplossing en praktische overwegingen
Het bovenstaande in overweging genomen is het dus wenselijk om zoveel als mogelijk een validatie live door te voeren bijna direct nadat er een validatiecode is aangemaakt.

Indien het mogelijk is om de patiënt vooraf de app te laten installeren en live de code voor te lezen aan de GGD-medewerker is dit, net als bij de corona-app, de wenselijke route.

Nu zal dit niet in alle gevallen mogelijk zijn en zou het voor het proces technisch zeer praktisch zijn om de 2^e^ weg **ook** mogelijk te maken.

## Lengte van de koppelingscodes
Gezien de codes via de telefoon voorgelezen moeten worden vanaf een scherm is het verschil tussen een aantal tekens zoals l, i, en 1; o, O en 0 niet in elk font duidelijk.^[^1]^

Hierdoor zal om praktische redenen niet de gehele 52 letters + 10 cijfers tekenset gebruikt kunnen worden.

Het makkelijkste is af te zien van het gebruik van deze tekens. Wel zal om dezelfde hoeveelheid entropie kwijt te kunnen de lengte van de koppelingscode langer moeten worden.

### Ter vergelijking
Bij coronamelder wordt alleen gebruik gemaakt van “BCFGJLQRSTUVXYZ23456789”, 6 tekens lang. Deze tekenset is kleiner - omdat er rekening mee gehouden worden dat, bijvoorbeeld de A en de E op elkaar kunnen lijken over de telefoon - zeker als het gesprek door beide kanten in een, gedeelde, niet-moederstaal gevoerd moet worden (zoals Engels).

Dit op ruim 2^27^Met alle tekens erbij zou dit uitkomen op 2^47,6^. Om dezelfde entropie kwijt te kunnen zouden er minimaal 11 tekens (2^49,7^) gebruikt moeten worden van de beperkte tekenset.

Deze lengte moet gerelateerd worden aan hoe vaak ze gebruikt kan worden - bij bellen door de GGD zijn de eisen langer dan bij een interactie waar men vrij onbeperkt kan ‘proberen’.

### Birthday attack /  Verjaardagenparadox^[^2]^
Om een succesvolle aanval uit te voeren zal een aanvaller binnen de tijd van de geldigheid een geldige code moeten kunnen aanleveren. Nu gaat een aanval via personen moeilijk en via computers snel en makkelijk. De backend zal vele duizenden verzoeken per dag makkelijk moeten aankunnen en daarmee is de kans op een geldige aanval vele malen groter omdat het probleem niet lineair schaalt.

Bij coronamelder is de geldigheid 1 dag en wordt de code via de telefoon aangeleverd. Bij 5.000 uploads per dag is de kans dan zeer klein < 1.000.000 dat iemand via de telefoon een correcte code kan doorgeven binnen 4 keer claimen het verkeerd te hebben gelezen.
*Table 2: Overzicht pogingen en kans*
|P | Tries |
|--|--|
| 50% | 14400 |
| 10% | 5600 |
| 1% | 1750 |
| 0.1% | 550 (1:1000) |
| 0.01% | 170 |
| 0.0001% | 17 (1:1000000) |

(De laatste 2 mogelijkheden zijn door de gebruikte rekenmethode niet nauwkeurig, maar geven een indicatie van het niveau.)

In de praktijk zal voor een code die meerdere dagen geldig is en door een gebruiker ingevoerd kan worden - en dus automatisch door een computer – met een lengte van 9 tekens uit de bovenstaande tekenset de kans 1:1.000.000 zijn met ongeveer 2000 keer invoeren. Met 12 tekens is de kans 1:10.000.000 met ongeveer 66.000 keer invoeren.

Dat betekent dit dat wanneer een aanvaller elke seconde een nieuwe poging kan ondernemen en daarmee niet door de anti-aanvalsmechanismen gestopt wordt er 18 uur lang geprobeerd dient te worden om deze kans van 1 op 10 miljoen te halen. Bij snellere aanvallen zullen er andere anti-aanvalsmechanismen in kunnen grijpen.

### Conclusie
- Gezien de code slechts geldig zal zijn een zeer korte tijd (minuten) terwijl het gesprek gevoerd wordt (1^e^ weg) en ongeveer 45 minuten (2^e^) zijn de kansen op mogelijk misbruik zeer klein bij een lengte van 6 tekens (1^e^weg) en 12 tekens  (2^e^weg) uit de tekenset “0123456789”
- Een langere code biedt iets meer bescherming bij de 2^e^weg en bijna geen enkele bij de 1^e^weg.
- De keuze voor 6 tekens (1^e^weg) en 12 tekens (2^e^weg) is vanuit de wens om zo min als mogelijke tekens te moeten overbrengen en toch een zekerheid te bieden, meer tekens levert in dat deel van het proces en grotere foutkans.
- Bij 1000 pogingen zal de monitoring en security aan de voorkant van de applicatie al ingegrepen dienen te hebben en is de kans nog steeds zeer klein op een succesvolle pairing.
-  Bij 1000 pogingen met 12 tekens is de kans kleiner dan 1 op een miljoen dat er een goede code gegokt is.
- Hergebruik koppelingscodes en foutmeldingen
- Hergebruik van koppelingscodes binnen een een korte tijd (30 dagen) is niet gewenst, als dit zou voorkomen is het nodig ‘verboden’/gebruikte koppelingscodes bij te houden met verloopdatum en tijd.

Vanuit gebruikersperspectief is het wenselijk om te weten dat men te laat is met een koppelingscode. Om dit te faciliteren mag de API tot 1 dag na het verlopen van de koppelingscode een foutmelding teruggeven.

Gebruikte codes verkleinen per keer de keyspace met 1 code. Zelfs met 17.000.000 koppelingen in 1 maand is de keyspace met slechts 0.0002% verkleind in het geval van de langste code. De impact is dus nihil voor de veiligheid en groot voor het gebruiksgemak.

## Datatransport beveiliging
Het datatransport dient versleuteld zijn met HTTPS TLS 1.3 met de juiste ciphers en PFS (of soortgelijk – dus dat een key compromise op dag 10 niet leidt tot confidentialiteit verlies van dag 1-9). Indien uit oogpunt van gebruikersacceptatie oudere OS versies ondersteund dienen te worden zal daar de TLS versie niet lager mogen zijn dan TLS 1.2. (Android < versie 10, IOS < 12.2). Op de test van Qualys SSL Lab zal een A+ gehaald dienen te worden. Hiernaast zal aan de eisen van de
BIO voldaan moeten worden.

Uit privacy- en security-overwegingen volstaat het niet data slechts op transport-niveau te versleutelen. Op de de endpoint van de bovengenoemde TLS verbinding mag de data niet leesbaar aanwezig zijn. Dit zorgt ervoor at er een gesplitste backend is en daardoor er defense-in-depth ontstaat.

Op de backend zal voor beheer het 4-eyes principe worden toegepast.

Op de devices zelf is dit binnen de applicatie te doen door gebruik te maken van Keystore / Keychain en encryptie van de lokale data op basis hiervan.

Tijdens transport zal de data verpakt moeten zijn in een veilige layer waarbij aan de buitenkant niet efficiënt is op te maken of een gebruiker veel of weinig, zinnige of onzinnige data verstuurd (side-channel analyse – en het tegemoetkomen aan non-functional requirements, zoals de nvermijdelijke (D)DOS attacks, stuffing, etc.). Zo zullen de datastromen dus gevuld moeten worden tot een bepaalde grootte waardoor
het niet voorspelbaar is wat de gebruiker precies deed.

In de designdocumenten wordt daarnaast gesproken over een digitale sluis, deze digitale sluis zal wel data moeten kunnen valideren (b.v. uw pakket is goed ontvangen, we kennen de sleutel waarmee die ontsleuteld kan worden), maar deze sluis mag op geen enkele manier bij de data zelf komen en dus ook niet zien hoe groot de echte data is.

Het is aan te raden om voor elke transactie/gebruiker/app installatie een nieuwe sessiesleutel beschikbaar te hebben zodat het ontsleutelen van de data die door/op de sluis is gegaan nooit gedaan kan worden als er 1 enkele transportsleutel gecompromiteerd is. Tevens is het van waarde indien één van de sleutels een emphemeral sleutel is c.q. eén die perfect-forward-secrecy ondersteund. Dit zodat een key compromise in het relatieve 'exposed' deel van de architectuur niet effectief is terug in de tijd.

Net zoals bij de coronamelder is het vanuit privacy oogpunt handig om ‘decoy’ data te versturen. Zodat na netwerk-analyse niet duidelijk is of iemand nu echt data heeft verzonden naar de GGD of niet. Hierbij gaat het om het non-functional requirement dat een derde, bijvoorbeeld een werkgever of netwerkbeheerder niet met redelijke zekerheid kan stellen dat een bepaalde werknemer al dan niet besmet is door middel van observatie voor het verkeer. Het is hierbij voldoende indien de kans dat
buitenstaander 'juist raadt^[^3]^' klein is, dus onder de 2%.

Routeren van de data: Het kan bijvoorbeeld een mogelijkheid zijn om de data te routeren via open protocollen en andere internet-services. (Signal-app, Tor of iets soortgelijks). Helaas is hiermee de data dan ook afhankelijk van de beveiliging van deze services en de gemiddelde telefoonbezitter doet niks met Tor: dan levert dit verkeer ook al een indicator op dat men deze app gebruikt.

### Conclusie
Goed inpakken, padding, sleutelgeneratie en uitwisseling, decoy packets en de mogelijk de applicatie te installeren zonder hiervoor vooraf toestemming te verkrijgen maken het praktisch onmogelijk om side-channel analyse te doen op het device van de gebruiker, onderweg op het netwerk en op de digitale sluis en verhinderen het makkelijk ontsleutelen in geval van voorgekomen fouten.

## Opslag: device side

### Encryptie
De data zal moeten worden opgeslagen op de telefoon voordat deze verzonden wordt.

Deze data zal versleuteld moeten worden opgeslagen zodat er door andere applicaties niet te lezen is wat er in de database staat. Deze sleutel moet voor elk device uniek zijn, op het device aangemaakt moeten worden en alleen aanwezig zijn op het device zelf.

Android: De encryptie zal bij voorkeur gedaan moeten worden met een door *StrongBox Keymaster* zo breed als mogelijk ondersteunde versleuteling.
Indien *Strongbox* niet beschikbaar is zal er van de *Keystore* gebruik gemaakt moeten worden.

IOS: Voor IOS dient gebruik te worden gemaakt te worden gemaakt van *Keychain*

### Vaste grootte
De versleutelde database zal normaal gesproken altijd even groot moeten zijn.

Daardoor is van buitenaf niet vast te stellen of een gebruiker data heeft ingevoerd en hoeveel data is ingevoerd en op welk moment (groeit de file elke keer). Er zal dus direct na installatie een hoeveelheid ruimte moeten worden gereserveerd en versleuteld om vanaf dat moment geen veranderingen meer te kunnen waarnemen door metadata van het bestand te bekijken.

Indien mogelijk zal ook het tijdstempel van de file (last open, last modified) ook niet beschikbaar mogen zijn voor derden. Ook niet in back-ups van het device.

## Opslag: Server side
De opslag op de server vind plaats in een SQL database en in een in-memory redis database.

Op de database en applicatie servers zal encryption-at-rest (harddisk versleuteling) worden toegepast met een encryptie en sleutelbeheer conform BIO.

In de redis memory database worden de shared-secrets opgeslagen zodat deze door de applicatie te raadplegen zijn.

In de SQL database zal op alle velden die privacy gevoelige informatie bevatten versleuting worden toegepast door de applicatie. De versleuteling is op basis van een X25519 private key en XSalsa20-Poly1305 stream.

De sleutels voor de database encryptie zullen worden opgeslagen op de HSM.

Door middel van een key-rollover proces zal op dagelijkse basis een nieuwe sleutel in gebruik worden genomen. Na het verlopen van de nuttige tijd te weten 3 weken zal deze sleutel in de HSM worden gewist en daarmee decryptie van verwijderde data waarvan wel een backup is ook niet meer leesbaar zijn.

Gezien de data per veld apart encrypted is opgeslagen kan er zonder problemen via de normale gangbare beheersprocessen een backup gemaakt worden. Deze back-ups zullen versleuteld dienen te worden met een public/private encryptiemethode waarvan de private sleutel niet op de servers aanwezig is.

De decryptiesleutel voor backups zal volgens een BIO conform proces gebruikt kunnen worden indien de backups teruggezet dienen te worden.

## Eenrichtingsverkeer
Het zal alleen mogelijk moeten zijn om data naar de GGD op te sturen. Het moet niet mogelijk zijn om eenmaal ingestuurde data terug op te halen voor een gebruiker.

Vanuit het proces lijkt dit niet nodig en is daarmee zeer onwenselijk,
het vergroot het risico op lekken enorm en zou dus een zwaardere
authenticatie vereisen.

### Vragen / opdrachten
Vanuit het proces worden opdrachten/vragen naar het device gestuurd.
Indien mogelijk zal dit via pushberichten dienen te gebeuren. Daarmee is
het niet mogelijk om andere opdrachten ophalen.

Deze pushberichten dienen zoals andere berichten altijd van gelijke
grootte te zijn en encrypted zijn.

Om niet duidelijk te maken met welke client er gecommuniceerd wordt door
de pushberichten te monitoren zullen er vanuit de backend ook random
pushberichten naar telefoons gestuurd moeten worden. (noise). Tevens zal
er van het eerder genoemde 4-eye procedures en operationele split
gebruik gemaakt worden om de IP address zo vroeg mogelijk te ‘strippen’
en niet zichtbaar te maken voor het backend team.

Push notificaties van google en apple vereisen een koppeling tussen het
apple en google waarbij duidelijk is dat de app gebruikt wordt. **Dit
niet te verantwoorden, dus kan niet gebruikt worden.**

### Hoeveelheid leeg verkeer
In het geval van echt gebruik van de app zal er een aantal berichten opdrachten en een aantal keer data versturen plaatsvinden.

Om de kans op ontdekking te minimaliseren zou het het beste zijn om elke installatie elke paar dagen te laten doen alsof er een compleet proces wordt doorlopen.

Dit kost een enorme hoeveelheid dataverkeer ten opzichte van alleen het normale gebruik. Om deze kosten voor de gebruiker en de backend laag te houden is het ook mogelijk om de app een willekeurigheid te geven. Dat slechts een beperkt deel van de installaties doet alsof er een sessie wordt doorlopen in berichtgeving. Zodat het plausibel is dat de app zelf dit verkeer genereert en er dus in een analyse met geen enkele zekerheid te zeggen is of dit de gebruiker is of de app.

De kans op een echte sessie zal aanmerkelijk kleiner (factor 10 tot 100) moeten zijn.

## Certificaten
Voor de backend zal gebruik moeten worden gemaakt van PKI-Overheid EV-certificaten^[^4]^ en de app zal controle van het certificaat doen op basis van de normale (Subject) controles, CA pinning, DNS CAA records en de DNS van de backend zal DNSsec gesigneerd dienen te zijn.

Gezien de recente G3 situatie verdient het hierbij aanbeveling om, waar mogelijk, gebruik te maken van de M2M certificaten van de PKI Overheid (welke beter geisioleerd zijn van het World CAB forum en google.com haar wensen).

Clients dienen zich niet te identificeren met een certificaat. De toegevoegde waarde van een certificaat is nihil gezien de inhoud al versleuteld is (zie Versleutelen verstuurde data). Terwijl dit al gauw tot een zeer hoog niveau van traceerbaarheid zou leiden – met volledig verlies van de privacy. Het registreren/ondertekenen van een client certificaat zou ook geautomatiseerd dienen te gebeuren zonder extra controles ten opzichte van de andere processen. Om deze reden is de eerder genoemde patat-drempel zo belangrijk. Het dient mogelijk te zijn om 'goedkoop^[^5]^' vast te stellen of een binnenkomend bericht echt genoeg is om resources te vragen. Zodat een DOS goedkoop kan worden afgevangen.

De overwegingen hierbij zijn:
- PKI overheid EV heeft een hele lijst met eisen waaraan voldaan dient te worden.^[^6]^
- CA pinning zorgt ervoor dat slechts 1 CA toegestaan is voor dit gebruikelijk
- DNS CAA zorgt er ook voor dat er slechts de gepubliceerde CA toegestaan is (en dit kan eventueel ook onderdeel uitmaken van een pin in de app).
- DNSsec is nodig om DNS geauthenticeerd is en valse data tegen te gaan

### Ciphers
Indien het device het ondersteund zal er gebruik gemaakt dienen te worden van TLS 1.3 omdat deze vele voordelen heeft ten opzichte TLS 1.2 in niet meer ondersteunde onveilige communicatiemogelijkheden. Ook bij een niet perfecte configuratie is de kans op een mogelijke niet goede encryptie zeer sterk beperkt.

Toegestane TLS strings voor communicatie app<>sluis en sluis<>backend:

*TLS\_AES\_128\_GCM\_SHA256
TLS\_AES\_256\_GCM\_SHA384
ECDHE-RSA-AES128-GCM-SHA256
ECDHE-RSA-AES128-SHA256
ECDHE-RSA-AES256-GCM-SHA384
ECDHE-RSA-AES256-SHA384*

## Versleutelen verstuurde data
Bij aanmelding zal; encrypted met de publieke sleutel van de backend^[^7]^; de publieke sleutel van de client ten behoeve van communicatie verstuurd worden naar de backend.

De app en de backend doen een ECDH-E exchange ten bate van een sessie-sleutel. Hiervoor wordt door de client en door de backend een emphemeral-sleutel gebruikt.

De afgeleide gedeelde sleutel (session-key) wordt gebruikt ten behoeve van encryptie van berichten naar elkaar.

De redenen voor het creëren van tijdelijke sleutels is zodat er een makkelijk re-keying proces kan plaatsvinden, de (vaste) sleutels niet getraceerd kunnen worden omdat deze niet gebruikt worden in het proces van de “normale” communicatie. Ook zal bij sleutelverlies van de primaire sleutel er geen decryptie mogelijk zijn van alle berichten op basis van de enkel initieel gebruikte primaire sleutel. En het (her)gebruik van sleutels is beperkt tot 1 installatie van de applicatie.

### Het proces
Client: Genereer een emphemeral sleutel (ECDH-E) en versleutelt het
volgende met de bekende public key van de backend:
- public key van de client

De client verstuurd deze versleutelde data tesamen met de pairing key
(indien meegegeven) naar de sluis.

Server: Genereer een emphemeral sleutel (RSA keypair) en versleutel het
volgende met (emphemeral) public key van de client:

- (emphemeral) public key van de server

Opdrachten die op de publieke backend / sluis neergezet door de backend worden geidentificeerd aan de hand van de SHA-256 van de shared-secret.

Een client die een opdracht wil ophalen communiceert de SHA-256 van de shared-secret met de sluis en krijgt aan de hand hiervan een antwoord. Indien er een opdracht aanwezig is de opdracht en indien dat niet het geval is een block vol met random data zodat met een attack niet af te leiden is of er voor een client een opdracht klaar staat. En zodat vanaf passieve observatie niet af te leiden is wat een client binnenkrijgt.

Een client die een antwoord wil verzenden zal dit encrypten met de shared-secret en opsturen met vermelding van de SHA-256 van de shared-secret.

### Re-keying
Indien een client opnieuw een sessie wil initieeren kan dit door:

Genereer een emphemeral sleutel (ECDH-E) en versleutelt het volgende met de bekende public key van de backend:

- public key van de client
- Ondertekend door de hiervoor gebruikte public key van de client.

Aangezien de vorige public key van de client bekend is zal deze daarna vervangen worden door de nieuwe public key. Er zal een nieuwe shared-secret worden berekend zoals hierboven aangegeven.

### Opslag tijdelijk sleutels  (empheral keys)
#### Device
Op het device dienen de sleutels (public en private keys) versleuteld te worden opgeslagen.

Dit mag in dezelfde database als de eerder beschreven.

##### Backend
Op de backend zullen de sleutels die genereerd worden op basis van random verkregen uit de HSM alleen tijdelijk in memory mogen worden opgeslagen. Dit mag in een database maar na 3 weken zullen deze sleutels vernietigd dienen te worden. Indien er hierna nog gecommuniceerd dien te worden met de client zal er een re-keying proces plaats dienen te vinden.

## Vernietigen sleutels
Na het verwijderen van de app is zal de data van de telefoon verwijderd moeten zijn.

Na afloop van de nuttige tijd zoals gesteld is door de GGD zal de data verwijderd moeten worden op de backend storage. Ook zullen de decryptiesleutels vernietigd moeten worden.

Op IOS is het niet mogelijk om bij deinstallatie de sleutel uit de keychain te verwijderen.

Er is geen mogelijke toegang meer toe tot na herinstallatie van de app. Bij het verwijderen van de app is wel de database met informatie, shared secret, public/private EC keyset en andere data verdwenen.

Dit is dus geen onoverkomelijk probleem. Wel zal hier in het ontwerp rekening mee gehouden moeten worden. (Bij herinstallatie de oude key verwijderen is een goede optie).

## Bijwerken van data door de gebruiker

Er zijn 2 methoden van bijwerken:

- Er wordt alleen data toegevoegd
- Er wordt data toegevoegd en verwijderd.

Alleen data toevoegen is niet wenselijk, dan kan een app-gebruiker nooit data verwijderen. Het is misschien niet verplicht om data te kunnen verwijderen, maar uit maatschappelijk oogpunt wel gewenst dat indien de gebruiker in de app data verwijdert dit aan de backend kant ook gereflecteerd wordt.

Bij het delen van nieuwe contacten zal door de applicatie de complete dataset bijgewerkt worden.

Hierdoor is het door gebruikers mogelijk om contacten die eerder gedeeld waren toch te verwijderen.

Hiermee is het voor gebruikers mogelijk om fouten te herstellen binnen de tijd dat de data bestaat ten behoeve van het BCO.

[^1]: https://www.ismp.org/resources/misidentification-alphanumeric-symbols

[^2]: https://nl.wikipedia.org/wiki/Verjaardagenparadox

[^3]:  Dus dat deze besmet is indien dat zo is; of juist niet besmet is indien zij geen index is.

[^4]: PKI-overheid OV bestaat niet meer, de opties zijn dus DV versus EV. DV is niet voldoende.

[^5]: Dus zonder al te veel database lookups – en liefst geheel zonder (ECDHE of HMAC check)

[^6]: https://www.logius.nl/diensten/pkioverheid/aansluiten-als-tsp/pogramma-van-eisen

[^7]: Dit is een andere sleutel dan de sleutel van de sluis
