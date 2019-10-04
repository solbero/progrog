# Lag en terning med Micro Bit

<iframe width="768" height="432" src="https://www.youtube.com/embed/3XVeBTbpBo4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Introduksjon

Dette er en oppgave som passer godt for nybegynnere og den tar en time å gjennomføre. Du skal i denne oppgaven programmere Micro Biten til å bli en terning. Micro Biten har en sensor som gjør at den kan merkes om den ristes. Den skal vi bruke til å lage vår egen Micro Bit-terning!


!!! abstract "Du vil lære"
    * å få Micro Biten til å gjøre noe når den ristes
    * å lage en animasjon på skjermen til Micro Biten
    * å bruke en variabel til å huske et tall

!!! info "Du trenger"
    * en Micro Bit
    * en USB-kabel til overføring
    * en batteripakke med to AAA-batterier
    * en utskrift av brettspillet [Snakes and Ladders](images/snakes-and-ladders.svg) per to elever

## Steg 1: Slå en terning

Begynn med å gå til [MakeCode for micro:bit](https://makecode.microbit.org/). Start et nytt prosjekt ved å trykke på knappen `Nytt Prosjekt`. Da vil nettsiden der du programmerer Micro Biten åpnes. Gi prosjektet navnet *Terning* ved å skrive i tekstfeltet nederst på nettsiden.

Slett alle klossene som ligger i lærretet. Du sletter en kloss ved å dra den til venstre. Når det dukker opp et søplespann slipper du klossen for å slette den.

Nå skal vi kode! Vi vil at Micro Biten skal gjøre noe når du rister den. Begynn med å dra klossen `når ristes`{:.input} fra kategorien `Inndata`{:.input} og slipp den på lærretet til høyre på nettsiden.


```blocks
input.onGesture(Gesture.Shake, function () {
})
```

Når Micro Biten ristes skal den vise et tall på skjermen. For å få til dette må du dra klossen `vis tall`{:.basic} fra kategorien `Basis`{:.basic} og plassere den i munnen til `når ristes`{:.input}.

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.showNumber(0)
})
```

Micro Biten skal vise et tilfeldig tall på skjermen når den ristes. For å kode dette må du plassere klossen `velg tilfeldig`{:.math} fra kategorien `Matematikk`{:.math} på verdifeltet til `vis tall`{:.basic}.

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.showNumber(Math.randomRange(0, 10))
})
```

En terning har øyne fra 1 til 6. Men `velg tilfedig`{:.math} har som standard et at den velger et tilfeldig tall fra 0 til 10. For at Micro Biten skal vise riktige tall for en terning må du skifte verdiene til 1 og 6.

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.showNumber(Math.randomRange(1, 6))
})
```
!!! success "Test programmet"
    Til venstre på MakeCode er det et bilde av en Micro Bit. Denne kan du bruke til å teste programmet ditt mens du koder. Trykk på den hvite sirkelen ved siden av `SHAKE`. Da tror Micro Biten at du rister den, og den vil vise ett tilfeldig tall mellom 1 til 6.

!!! failure "Det virker ikke!"
    Hvis Micro Biten ikke viser et tall mellom 1 til 6 hver gang du trykker `SHAKE` så er noe galt i koden din. For å finne feilen bør du lese oppskriften om igjen og se nøye på bildene. En vanlig feil er å glemme å skifte tallene i `velg tilfeldig`{:.math} til 1 og 6.

!!! question "Utfordring"
    Vanlige terninger har øyne fra 1 til 6. Men noen terninger har øyne fra 1 til 20. Disse kalles for D20-terninger. Hva må du forandre i koden du har skrevet for å få Micro Biten til å fungere som en D20-terning?

## Steg 2: Lage en enkel terninganimasjon

Terningen vår fungerer nå, men den er litt kjedelig. Det ville vært mye morsommere om terningen viste forskjellige tall før den til slutt landet på et tall slik som en ekte terning. For å få til dette må du lage en animasjon.

Hent klossen `gjenta`{:.loops} fra kategorien `Løkker`{:.loops} og plasser den rundt `vis tall`{:.basic} i koden din.

```blocks
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 4; i++) {
        basic.showNumber(Math.randomRange(1, 6))
    }
})
```

Skift tallet i verdifeltet til `gjenta`{:.loops} fra 4 til 5.

```blocks
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 5; i++) {
        basic.showNumber(Math.randomRange(1, 6))
    }
})
```

!!! info "Hva gjør klossen `gjenta`{:.loops}?"
    Denne klossen gjentar koden som plasseres i munnen til klossen. Antall ganger `gjenta`{:.loops} gjentar koden bestemmes av tallet som står i verdifeltet. Det finnes forkjellige typer gjenta-klosser. Du kan se alle typene som finnes i MakeCode ved å trykke på kategorien `Løkker`{:.loops}.

Hvis du tester programmet ditt nå vil se du at tallene på skjermen til Micro Biten skifter veldig fort. Det er rett og slett vanskelig å se dem. For å få hvert tall til å vises lengre på skjermen må vi legge til en pause.

Dra klossen `pause`{:.basic} fra kategorien `Basis`{:.basic} og plasser den under `vis tall`{:.basic}. Pass på at `pause`{:.basic} er inni munnen til `gjenta`{:.loops}.

```blocks
input.onGesture(Gesture.Shake, function () {
    for (let i = 0; i < 5; i++) {
        basic.showNumber(Math.randomRange(1, 6))
        basic.pause(100)
    }
})
```

!!! success "Test programmet"
    Bruk Micro Biten på nettsiden til å teste programmet ditt. Trykk på den hvite sirkelen ved siden av `SHAKE`. Microbiten skal da vise fem tilfeldige tall på skjermen for hver gang du trykker `SHAKE`.

!!! question "Utfordring"
    Hva må du forandre i koden din for å få Micro Biten til å kun vise tre tilfeldige tall hver gang du trykker på `SHAKE`?

## Steg 3: Få terningkastet til å blinke

Terningen fungerer nå, men det kan være vanskelig å se hva tall terningen lander på til slutt. Det kan vi gjøre tydeligere ved å lage en ny animasjon som får tallet terningen lander på til å blinke.

Begynn med å ta en ny `gjenta`{:.loops} fra kategorien `Løkker`{:.loops}. Plasser den under klossen `gjenta`{:.loops} som allerede er i programmet. Skift tallet 4 til 3 i verdifeltet til den nye klossen.

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

For å få tallet til å blike på Micro Biten trenger du noen flere klosser. Finn først klossen `tøm skjerm`{:.basic}. For å finne denne klossen må du først trykke på kategorien `Basis`{:.basic}. Når du har trykket på kategorien vil det komme en ny kategori under `Basis`{:.basic} som heter `⋯ more`{:.basic}. Trykk på den nye kategorien for å finne `tøm skjerm`{:.basic}.

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

!!! info "Hva gjør klossen `tøm skjerm`{:.basic}?"
    Denne klossen skrur av alle lysene på skjermen til Micro Biten. Det er en kloss som er fin å bruke hvis du vil vise noe på skjermen og så ta det vekk etterpå.

Nå skal vi finne tre klosser på en gang, men heldigvis kommer alle fra samme kategori. Først finner du klossen `pause`{:.basic} fra kategorien `Basis`{:.basic}. Ta så en `vis tall`{:.basic} fra samme kategori. Til slutt trenger du enda en `pause`{:.basic}.

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
    Bruk simulatoren på MakeCode til å teste programmet ditt. Trykk på `SHAKE` på Micro Biten og se hva som skjer!

!!! failure "Det virker ikke!"
    Hvis du testet programmet ditt i simulatoren så vil du ha sett en feil i koden. Det var kun tallet 0 som blinket, og ikke terningkastet. Det skal vi fikse nå.

## Steg 4: Huske et terningkast med en variabel

Heldigvis finnes det en måte å få Micro Biten til å huske det siste tallet i animasjonen til terningen. Vi må bruke en variabel.

For å lage en variabel trykker du på kategorien `Variabler`{:.variables}. Trykk så på knappen `Lag en ny variabel`. Du vil få spørsmål om hva du vil kalle variabelen din, kall den for *terningkast* og trykk på `Ok`.

!!! info "Hva er en variabel?"
    Variabler brukes i programmer for å huske noe til senere. En variabel kan være et tall eller en setning. Det er være mange grunner til at programmer må huske noe. En grunn for at et program skal huske et tall som skal brukes i et regnestykke senere i programmet.

Etter at du har laget variabelen `terningkast`{:.variables} vil det komme noen nye klosser i kategorien `Variabel`{:.variables}. Finn klossen som heter `sett terningkast til`{:.variables} og plasser den over `vis tall`{:.basic}. Pass på at `sett terningkast til`{:.variables} er i munnen til `gjenta`{:.loops}.

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

Dra klossen `velg tilfeldig`{:.math} vekk fra verdifeltet til `vis tall`{:.basic} og slipp den ned på verdifeltet til `sett terningkast til`{:.variables}.

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

Hent to `terningkast`{:.variables} fra kategorien `Variabler`{:.variables} og plasser dem på vedrifeltet til `vis tall`{:.basic} i programmet.

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

!!! success "Test programmet"
    Overfør det ferdige programmet til Micro Biten ved å bruke en USB-kabel eller Blåtann. Spør en voksen eller venn om hjelp hvis du er usikker. Rist på terningen din og sjekk at programmet fungerer riktig.

Gratulerer, du har nå laget en terning med Micro Biten! Da er det på tide å teste terningen din med å spille brettspillet Snakes and Ladders. Gå sammen to-og-to og se hvem som klarer å vinne!

## Kode

<div style="position:relative;height:0;padding-bottom:70%;overflow:hidden;"><iframe style="position:absolute;top:0;left:0;width:100%;height:100%;" src="https://makecode.microbit.org/#pub:_XyC09yC7kK2f" frameborder="0" sandbox="allow-popups allow-forms allow-scripts allow-same-origin"></iframe></div>