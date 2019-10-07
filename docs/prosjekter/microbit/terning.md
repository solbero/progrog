# Lag en terning med Micro Bit

<iframe width="768" height="432" src="https://www.youtube.com/embed/3XVeBTbpBo4" frameborder="0" modestbranding="1" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Introduksjon

Dette er en oppskrift som passer deg som er nybegynner i Micro Bit. Den tar omtrent en halvtime å gjennomføre. I denne oppskriften vil du programmere Micro Biten til å bli en terning som du kan bruke til å spille brettspillet *Snakes and Ladders*.


!!! abstract "Du vil lære"
    * å få Micro Biten til å gjøre noe når den ristes
    * å lage animasjoner på skjermen til Micro Biten
    * å bruke en variabel til å huske et tall

!!! abstract "Du trenger"
    * en Micro Bit
    * en USB-kabel til overføring
    * en batteripakke med to AAA-batterier
    * en utskrift av brettspillet <a href="../images/snakes-and-ladders.svg" target="_blank">Snakes and Ladders</a>

## Steg 1: Gjør noe når Micro Biten ristes

Micro Biten har en sensor som gjør at den kan merke når den ristes. Den skal vi bruke til å lage vår egen Micro Bit-terning. I dette steget skal du få Micro Biten til å reagere på at den ristes og da vise et terningkast.

* Begynn med å åpne nettsiden <a href="https://makecode.microbit.org/" target="_blank">MakeCode for micro:bit</a>.

* Trykk på knappen `Nytt Prosjekt` for å starte et nytt prosjekt.

* Gi prosjektet navnet *Lag en terning* ved å skrive i tekstfeltet nederst på siden.

* Slett alle klossene som ligger i lærretet. Du sletter en kloss ved å dra den til venstre over kategoriene. Slipp klossen når søplespannet vises for å slette den.

Micro Biten kan reagere på forskjellige typer *inndata*. Inndata er noe som skjer med Micro Biten og som du ønsker den skal reagere på. Noen eksempler på inndata er å trykke på en knapp på Micro Biten eller å vende den opp-ned. I dette programmet ønsker vi at Micro Biten skal reagere på at den ristes.

* Dra klossen `når ristes`{:.input} fra kategorien `Inndata`{:.input} og slipp den et sted på lærretet.

```blocks
input.onGesture(Gesture.Shake, function () {
})
```

Som du ser ovenfor er det en munn på `når ristes`{:.input}-klossen. Hvis du plasserer en kloss i munnen på `når ristes`{:.input} vil denne klossen utføres når Micro Biten ristes. Alle klosser som blir plassert i munnen til en kloss fra `Inndata`{:.input}-kategorien vil utføres om Micro Biten får denne typen inndata.

Du skal nå fortelle Micro Biten at den skal vise tallet `0` når den ristes.

* Trykk på kategorien `Basis`{:.basic} og finn `vis tall 0`{:.basic}-klossen. Ta tak i klossen og plasser den i munnen til `når ristes`{:.input}.

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.showNumber(0)
})
```

!!! success "Test programmet"
    Til venstre på siden er det et bilde av en Micro Bit. Denne kan du bruke til å teste programmet ditt mens du koder. Trykk på den hvite sirkelen ved siden av `SHAKE`. Da tror Micro Biten at du rister den, og den vil vise tallet null.

## Steg 2: Vis et tilfeldig tall fra 1 til 6

Du har nå programmert at Micro Biten skal vise tallet null når den ristes. Men når du kaster en ekte terning vil den lande på og vise et tilfeldig tall fra en til seks. For å få til dette må vi fortelle Micro Biten at den skal vise et tilfeldig tall fra en til seks når den ristes.

* Finn klossen `velg tilfeldig 0 til 10`{:.math} i kategorien `Matematikk`{:.math}. Ta tak i klossen og slipp den på verdifeltet `0` på `vis tall`{:.basic}-klossen.

* Trykk på verdifeltet `0` på `velg tilfeldig 0 til 10`{:.math} og skriv inn tallet `1`.

* Trykk deretter på verdifeltet `10` på `velg tilfeldig 1 til 10`{:.math} og skiv inn tallet `6`.

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.showNumber(Math.randomRange(1, 6))
})
```
!!! success "Test programmet"
    Trykk `SHAKE` på Micro Biten. Den skal nå vise ett tilfeldig tall fra en til seks hver gang du trykker på `SHAKE`.

!!! failure "Det virker ikke!"
    Hvis Micro Biten ikke viser et tilfeldig tall fra en til seks hver gang du trykker `SHAKE` så er noe galt i programmet ditt. For å finne feilen bør du lese oppskriften om igjen og se nøye på bildene. En vanlig feil er å glemme å skifte tallene i verdifeltet på `velg tilfeldig fra 0 til 10`{:.math} til `1` og `6`.

!!! question "Utfordring"
    Vanlige terninger har øyne fra en til seks. Men noen terninger har øyne fra en til tjue. Disse kalles for D20-terninger. Hva må du forandre i koden du har laget for å få Micro Biten til å fungere som en D20-terning?

## Steg 3: Lage en terninganimasjon

Terningen din fungerer nå, men den er litt kjedelig. Den viser kun ett tall for hver gang du rister Micro Biten. Det ville vært mye kulere om terningen viste mange tilfeldige tall fra en til seks før den til slutt landet på et tall. For å få til dette må du lage en animasjon.

* Finn klossen `gjenta 4 ganger`{:.loops} fra kategorien `Løkker`{:.loops}. Dra den over til `vis tall`{:.basic} i programmet ditt. Når `vis tall`{:.basic} er i munnen til `gjenta 4 ganger`{:.loops} slipper du klossen for å plassere den.

```blocks
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 4; i++) {
        basic.showNumber(Math.randomRange(1, 6))
    }
})
```

Klossene som plasserer i munnen til `gjenta 4 ganger`{:.loops} vil utføres fire ganger etter hverandre. Antall ganger klossene i munnen utføres av `gjenta`{:.loops} bestemmes av tallet som står i verdifeltet til `gjenta`{:.loops}-klossen.

Vi vil at Micro Biten skal utføre `vis tall`{:.basic} fem ganger etter hverandre. For å få til dette må vi skifte tallet i verdifeltet til fem.

* Trykk på tallet `4` i verdifeltet på `gjenta 4 ganger`{:.loops} og skriv inn tallet `5`.

```blocks
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 5; i++) {
        basic.showNumber(Math.randomRange(1, 6))
    }
})
```

Hvis du nå tester programmet ditt vil se du at tallene skifter litt for fort. For å få hvert tall til å vises lengre på skjermen må vi legge til en pause mellom hver gang et tall vises.

* Finn klossen `pause (ms) 100`{:.basic} fra kategorien `Basis`{:.basic} og plasser den under `vis tall`{:.basic}. Pass på at `pause`{:.basic}-klossen plasseres i munnen til `gjenta 5 ganger`{:.loops}.

```blocks
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 5; i++) {
        basic.showNumber(Math.randomRange(1, 6))
        basic.pause(100)
    }
})
```

!!! success "Test programmet"
    Trykk på `SHAKE` for å teste programmet ditt. Micro Biten skal nå vise fem tilfeldige tall på skjermen hver gang du trykker `SHAKE`.

!!! question "Utfordring"
    Hva må du forandre i koden din for å få Micro Biten til å kun vise tre tilfeldige tall hver gang du trykker på `SHAKE`?

## Steg 4: Lag en blinkeanimasjon

Terningen fungerer nå, men det kan være vanskelig å se hva tall terningen lander på til slutt. Det kan vi gjøre tydeligere ved å lage en ny animasjon som får tallet terningen lander på til å blinke.

* Finn klossen `gjenta 4 ganger`{:.loops} i kategorien `Løkker`{:.loops}. Plasser den under `gjenta 5 ganger`{:.loops}. Skift tallet i verdifeltet til `3`.

```blocks
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 5; i++) {
        basic.showNumber(Math.randomRange(1, 6))
        basic.pause(100)
    }
    for (let i = 0; i < 3; i++) {

    }
})
```

For å få tallet terningen lander på til å blinke trenger du noen flere klosser.

* Finn klossen `tøm skjerm`{:.basic}. Du finner den ved å først trykke på kategorien `Basis`{:.basic} og deretter på `⋯ more`{:.basic} som dukker opp under.
* Ta tak i `tøm skjerm`{:.basic}-klossen og plasser den i munnen til `gjenta 3 ganger`{:.loops}.

```blocks
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 5; i++) {
        basic.showNumber(Math.randomRange(1, 6))
        basic.pause(100)
    }
    for (let i = 0; i < 3; i++) {
        basic.clearScreen()
    }
})
```

Klossen `tøm skjerm`{:.basic} skrur av alle lysene  på skjermen til Micro Biten. Det er en kloss som er fin å bruke hvis du vil vise noe på skjermen og så ta det vekk etterpå.

Nå skal vi finne tre klosser på en gang, men heldigvis kommer alle fra samme kategori.

* Finn klossen `pause (ms) 100`{:.basic} fra `Basis`{:.basic} og plasser den under `tøm skjerm`{:.basic}.
* Ta en `vis tall 0`{:.basic} og plasser den under `pause (ms) 100`{:.basic}
* Ta enda en `pause (ms) 100`{:.basic} og plasser den under `vis tall 0`{:.basic}.

```blocks
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 5; i++) {
        basic.showNumber(Math.randomRange(1, 6))
        basic.pause(100)
    }
    for (let i = 0; i < 3; i++) {
        basic.clearScreen()
        basic.pause(100)
        basic.showNumber(0)
        basic.pause(100)
    }
})
```

!!! success "Test programmet"
    Trykk på `SHAKE` for å teste programmet ditt. Se nøye etter om det skjer noe merkelig!

## Steg 4: Husk et terningkast med en variabel

Hvis du testet programmet ditt på slutten av forrige steg så vil du ha sett en feil i programmet. Det var kun tallet 0 som blinket, og ikke terningkastet. Det skal vi fikse nå!

Heldigvis finnes det en måte å få Micro Biten til å huske det siste tallet i terninganimasjonen. Vi må bruke en variabel.

Variabler brukes i nesten alle programmer. En variabel kan være et tall eller en setning. Det kan være mange grunner til at programmer må huske noe til senere. En grunn til at et program for eksempel må huske et tall er fordi tallet skal brukes senere i et regnestykke.

* Trykk på kategorien `Variabler`{:.variables}
* Trykk så på knappen `Lag en ny variabel`. Du vil få et spørsmål om hva du vil kalle variabelen; kall den for *terningkast* og trykk på `Ok`.

Etter at du har laget variabelen `terningkast`{:.variables} vil det komme noen nye klosser i kategorien `Variabel`{:.variables}.

* Finn klossen `sett terningkast til 0`{:.variables} og plasser den over den øverste `vis tall`{:.basic}-klossen.

```blocks
let terningkast = 0
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 5; i++) {
        terningkast = 0
        basic.showNumber(Math.randomRange(1, 6))
        basic.pause(100)
    }
    for (let i = 0; i < 3; i++) {
        basic.clearScreen()
        basic.pause(100)
        basic.showNumber(0)
        basic.pause(100)
    }
})
```

* Dra klossen `velg tilfeldig 1 til 6`{:.math} vekk fra verdifeltet til `vis tall`{:.basic} og slipp den ned på verdifeltet til `sett terningkast til 0`{:.variables}.

```blocks
let terningkast = 0
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 5; i++) {
        terningkast = Math.randomRange(1, 6)
        basic.showNumber(0)
        basic.pause(100)
    }
    for (let i = 0; i < 3; i++) {
        basic.clearScreen()
        basic.pause(100)
        basic.showNumber(0)
        basic.pause(100)
    }
})
```

* Hent to `terningkast`{:.variables} fra kategorien `Variabler`{:.variables} og plasser dem på verdifeltene til begge `vis tall 0`{:.basic}-klossene.

```blocks
let terningkast = 0
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 5; i++) {
        terningkast = Math.randomRange(1, 6)
        basic.showNumber(terningkast)
        basic.pause(100)
    }
    for (let i = 0; i < 3; i++) {
        basic.clearScreen()
        basic.pause(100)
        basic.showNumber(terningkast)
        basic.pause(100)
    }
})
```

Du har nå brukt en variabel til å huske det siste terningkastet. Det som skjer i programmet er at hver gang terninganimasjonen viser et tilfeldig tall så husker variabelen `terningkast`{:.variables} dette tallet. Når terninganimasjonen er ferdig og programmet går videre til blinkeanimasjonen så er det det siste tallet som ble vist i terninganimasjonen som huskes av variablen `terningkast`{:.variables}. Det er dette tallet som så blinker i blinkeanimasjonen!

!!! success "Test programmet"
    Trykk på `SHAKE` for å teste programmet ditt. Skjermen på Micro Biten skal først vise fem tilfeldige tall. Det siste av de fem tilfeldige tallene skal så blinke tre ganger på skjermen.

!!! failure "Det virker ikke!"
    Hvis Micro Biten ikke viser fem tilfeldige tall og så blinker det siste tilfeldige tallet når du trykker på `SHAKE` så er noe galt i programmet ditt. For å finne feilen bør du se på det siste bildet av koden ovenfor og sammeligne det med din kode.

## Avslutning

Gratulerer, du har nå gjort Micro Biten om til en terning! Hvis du testet programmet ditt på slutten av forrige steg og ikke fant noen feil så skal du nå overføre programmet til Micro Biten.

* Koble Micro Biten til datamaskinen din med en USB-kabel.
* Trykk på tannhjulet øverst til høyre på siden og velg `Koble sammen`.
* Nå vises en dialogboks på siden. Trykk på knappen `Koble sammen`.
* Velg *BBC micro:bit CMSIS-DAP* eller *DAPLink CMSIS-DAP* fra listen som vises og trykk på knappen `Sammenkoble`.
* Trykk til slutt på knappen `Last ned` nederst til venstre på siden for å overføre programmet til Micro Biten.

Da er det på tide å teste terningen din med å spille brettspillet *Snakes and Ladders*. Koble batteripakken til Micro Biten slik at du kan ta den med deg. Gå sammen med en venn og se hvem som klarer å vinne!