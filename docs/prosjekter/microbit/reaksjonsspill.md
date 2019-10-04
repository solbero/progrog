# Reaksjonsspill for to spillere med Micro Bit

## Introduksjon

Dette er en oppskrift som passer for deg som har programmert litt på Micro Bit fra før. Oppskriften tar en time å gjennomføre. Du skal i denne oppskriften  skal du lage et reaksjonsspill. Du vil i reaksjonsspillet spille en-mot-en og den som tykker først på sin knapp når en firkant vises på skjermen vinner!

!!! abstract "Du vil lære"
    * å vise bilder på skjermen til Micro Biten
    * å få Micro Biten til å gjøre noe når en knapp trykkes
    * å bruke en variabel til å lage en nedtelling
    * å kode regler for et spill

!!! info "Du trenger"
    * en Micro Bit
    * en USB-kabel til overføring
    * en batteripakke med to AAA-batterier

## Steg 1: Vis en firkant på skjermen når du trykker på to knapper

Begynn med å gå til [MakeCode for micro:bit](https://makecode.microbit.org/).[^1] Start et nytt prosjekt ved å trykke på knappen `Nytt Prosjekt`. Da vil nettsiden der du programmerer Micro Biten åpnes. Gi prosjektet navnet *Reaksjonsspill* ved å skrive i tekstfeltet nederst på nettsiden.

Nå skal vi kode! Det første vi vil er å  vise en firkant på skjermen til Micro Biten når du trykker A og B-knappene samtidig. Begynn med å dra en `gjenta for alltid`-kloss fra kategorien `Basis` og slipp den på lærretet til høyre på nettsiden.

```blocks
basic.forever(function () {
})
```

Finn en `hvis sann`-kloss fra kategorien `Løkker`. Slipp `hvis sann`-klossen inni munnen til `gjenta for alltid`-klossen.

```blocks
basic.forever(function () {
    if (true) {
    }
})
```

Etterpå tar du en `knapp A trykkes`-kloss fra kategorien `Inndata` og plasserer den på verdifeltet til `hvis sann`-klossen.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.A)) {
    }
})
```

Vi vil at Micro Biten skal gjøre noe når knappene A og B trykkes samtidig. For å få til dette må vi skifte `A` i `knapp A trykkes`-klossen til `A+B`. Trykk på bokstaven `A` på `knapp A trykkes`-klossen. Du vil da få opp en rullegardinmeny. Trykk på `A+B` i rullegardinmenyen for å velge den.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
    }
})
```

Når knappene `A` og `B` trykkes samtidig skal Micro Biten vise en liten firkant på skjermen. først finner du `vis ikon`-klossen i kategorien `Basis` og plasser den i «munnen» til `hvis`-klossen.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.showIcon(IconNames.Heart)
    }
})
```

Trykk på bildet av hjertet på `vis ikon`-klossen. Du vil da få opp en rullegardinmeny som inneholder mange forskjellige ikoner. Trykk på bildet av en liten firkant helt nederst i rullegardinmenyen.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.showIcon(IconNames.SmallSquare)
    }
})
```

Micro Biten skal vise den lille firkanten på skjermen på et tilfeldig tidspunkt når A og B knappene trykkes samtidig. For å få til dette må du først finne klossen `pause` i kategorien `Basis`. Plasser den over `vis ikon`-klossen.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.pause(100)
        basic.showIcon(IconNames.SmallSquare)
    }
})
```

Finn så `velg tilfeldig`-klossen i kategorien `Matematikk` og plasser den i verdifeltet til `pause`-klossen. Skift så verdien `10` i `velg tilfeldig`-klossen til `3000`.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.pause(Math.randomRange(0, 3000))
        basic.showIcon(IconNames.SmallSquare)
    }
})
```

!!! info "Hva er et millisekund (ms)?"
    Du la kanskje merke til at det står `(ms)` på `pause`-klossen? Datamaskiner arbeider veldig raskt og derfor, når vi skal fortelle den om hvor lenge den skal ta en pause, må vi bruke millisekund. Et millisekund er et tusenedelssekund. Det betyr at 3000 millisekunder er det samme som 3 sekunder.

Til slutt så må vi fortelle Micro Biten at skjermen skal tømmes hver gang vi trykker A og B knappene samtidig. Å tømme skjermen betyr å fjerne alt som vises på den. Hvis vi ikke forteller Micro Biten at skjermen skal tømmes så vil den lille firkanten vises hele tiden.

Finn `tøm skjerm`-klossen. For å finne denne klossen må du først trykke på kategorien `Basis`. Når du har trykket på den vil det komme en ny kategori under `Basis` som heter `⋯ more`. Trykk på den nye kategorien for å finne `tøm skjerm`-klossen. Plasser `tøm skjerm`-klossen over `velg tilfeldig`-klossen.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.clearScreen()
        basic.pause(Math.randomRange(0, 3000))
        basic.showIcon(IconNames.SmallSquare)
    }
})
```

!!! success "Test programmet"
    Til venstre er det bilde av en Micro Bit. Denne kan du bruke til å teste programmet ditt mens du koder. Trykk på den hvite sirkelen ved siden av `A+B`. Da tror Micro Biten at du trykker på A og B knappene samtidig og en liten firkant vil vises på skjermen. Firkanten vil dukke opp på forskjellige tidspunkt mellom 0 og 3 sekunder.

!!! failure "Det virker ikke!"
    Viser ikke den lille firkanten når du trykker på `A+B` knappen på Micro Biten? For å finne feilen bør du lese oppskriften om igjen og se nøye på bildene om du har glemt noe. En vanlig feil er å glemme å skifte `A` til `A+B` på `når trykkes`-klossen.

!!! question "Utfordring"
    Micro Biten viser nå den lille firkanten på et tilfeldig tidspunkt mellom 0 og 3 sekunder. Hvis du vil at Micro Biten skal vise den lille firkanten på et tilfeldig tidspunkt mellom 0 og 5 sekunder, hva tall skal da stå i stedet for 3000 i `velg tilfeldig`-klossen?

## Steg 2: Legge til to spillere

Micro Biten viser nå en firkant på et tilfeldig tidspunkt når du trukker på A og B knappen samtidig. Nå skal vi kode reglene til reaksjonspillet. Vi vil at den som trykker først på sin knapp når firkanten vises på skjermen vinner spillet.

Hent to `når knapp A trykkes`-klosser fra kategorien `Inndata`. Plasser disse klossene på lærretet. Skift `A` på den ene `når knapp A trykkes`-klossen til `B`.

```blocks
input.onButtonPressed(Button.A, function () {
})
input.onButtonPressed(Button.B, function () {
})
```

Plasser en `vis bilde`-kloss i munnen på hver av de rosa `når trykkes`-klossene.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
})
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
})
```

Tegn piler på `vis bilde`-klossene ved å trykke på de små firkantene.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . # . .
        . # . . .
        # # # # #
        . # . . .
        . . # . .
        `)
})
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . # . .
        . . . # .
        # # # # #
        . . . # .
        . . # . .
        `)
})
```

!!! success "Test programmet"
    Test programmet ved å trykke på A+B på Micro Biten til venstre på skjermen. Hva skjer om du tryker på A-knappen før firkanten kommer frem på skjermen på Micro Biten? Prøv så å trykke på A-knappen og etterpå trykk på B-knappen.

## Steg 3: Bruke en variabel for å huske en nedtelling

Når du testet programmet på slutten av forrige steg så la du kanskje merke til noe merkelig? Slik vi har kodet reaksjonspillet nå så har det ikke noe å si om firkanten har blitt vist på skjermen eller ikke. Pilen vil vise at du vant uansett. Dette må vi fikse.

For å løse dette må vi lage en nedtelling som teller ned til når firkanten vises på skjermen. For å huske hvor mye som er igjen av tiden til firkanten vises på skjermen må vi bruke en variabel.

Trykk på kategorien `Variabler` og så på den grå knappen `Lag en variabel`. Variabelen gir du navnet `nedtelling`. Dra så en `sett nedtelling til`-kloss ut i lærretet og plasser den over `pause`-klossen.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.clearScreen()
        nedtelling = 0
        basic.pause(Math.randomRange(0, 3000))
        basic.showIcon(IconNames.SmallSquare)
    }
})
```

!!! info "Hva er en variabel?"
    Variabler brukes i programmer for å huske noe til senere. En variabel kan være et tall eller en setning. Det er være mange grunner til at programmer må huske noe. En grunn for at et program skal huske et tall som skal brukes i et regnestykke senere i programmet.

Dra den lilla `velg tilfeldig tall`-klossen fra verdifeltet til `pause`-klossen og slipp den på verdifeltet til `sett nedtelling til`-klossen.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.clearScreen()
        nedtelling = Math.randomRange(0, 3000)
        basic.pause(100)
        basic.showIcon(IconNames.SmallSquare)
    }
})
```

Ta en `hvis sann`-kloss fra kategorien `Logikk` og plasser den under `vis ikon`-klossen, men pass på at `hvis`-klossen er inni munnen til den blå `gjenta for alltid`-klossen.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.clearScreen()
        nedtelling = Math.randomRange(0, 3000)
        basic.pause(100)
        basic.showIcon(IconNames.SmallSquare)
        if (true) {

        }
    }
})
```

Finn så en `0 = 0`-kloss fra kategorien `Logikk` og plasser den over `sann` i `hvis sann`-klossen.

```blocks
let nedtelling = 0
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.clearScreen()
        nedtelling = Math.randomRange(0, 3000)
        basic.pause(100)
        basic.showIcon(IconNames.SmallSquare)
        if (0 == 0) {

        }
    }
})
```

Trykk på `=` på `0 = 0`-klossen for å få frem rullegardinmenyen og skift tegnet til `>`.

```blocks
let nedtelling = 0
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.clearScreen()
        nedtelling = Math.randomRange(0, 3000)
        basic.pause(100)
        basic.showIcon(IconNames.SmallSquare)
        if (0 > 0) {

        }
    }
})
```

Ta en `nedtelling`-kloss fra `Variabler` og plasser den på `0` som er til venstre på `0 = 0`-klossen.

```blocks
let nedtelling = 0
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.clearScreen()
        nedtelling = Math.randomRange(0, 3000)
        basic.pause(100)
        basic.showIcon(IconNames.SmallSquare)
        if (nedtelling > 0) {

        }
    }
})
```

Flytt `pause`-klossen og plasser den i «munnen» til `hvis nedtelling > 0`-klossen. Skift verdien i verdifeltet på `pause`-klossen til `1`. Etterpå flytter du `vis ikon`-klossen under `hvis nedtelling > 0`-klossen.

!!! tip "Hvordan flytte kun en kloss"
    Du kan flytte en kloss som henger fast andre klosser. For å gjøre det må du holde nede `ctrl`-tasten på tastaturet når du flytter klossen.

```blocks
let nedtelling = 0
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.clearScreen()
        nedtelling = Math.randomRange(0, 3000)
        if (nedtelling > 0) {
            basic.pause(100)
        }
        basic.showIcon(IconNames.SmallSquare)
    }
})
```

Til slutt henter du en `endre nedtelling med`-kloss fra variabler og plasserer den under `pause`-klossen. Pass på at både `pause`-klossen og `endre nedtelling med`-klossen er inni «munnen» til `hvis nedtelling > 0`-klossen.

```blocks
let nedtelling = 0
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.clearScreen()
        nedtelling = Math.randomRange(0, 3000)
        if (nedtelling > 0) {
            basic.pause(100)
            nedtelling += 1
        }
        basic.showIcon(IconNames.SmallSquare)
    }
})
```

Endre verdien i verdifeltet til `pause`-klossen til 1 og verditeltet til `endre nedtelling med`-klossen til -1.

```blocks
let nedtelling = 0
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        basic.clearScreen()
        nedtelling = Math.randomRange(0, 3000)
        if (nedtelling > 0) {
            basic.pause(1)
            nedtelling += -1
        }
        basic.showIcon(IconNames.SmallSquare)
    }
})
```

!!! question "Hvordan fungerer nedtellingen?"
    Vi bruker variabelen `nedtelling` til å huske et tilfeldig valgt tall mellom 0 og 3000. La oss si at tallet 10 var det tilfeldige tallet som ble valgt.

    I neste steg av koden går programmet inn i en `gjenta`-kloss. I begynnelsen av denne klossen skjekker `gjenta`-klossen om variabelen `nedtelling` er større enn 0. Variabelen `nedtelling` er 10, derfor fortsetter programmet inn i «munnen» til `gjenta`-klossen. Her tar programmet en pause på 1 millisekund. Etter pausen tar programmet og forandrer `nedtelling`med -1. Variabelen `nedtelling` er nå tallet 9.

    I det siste steget går programmet tilbake til toppen av `gjenta`-klossen og skjekker om `nedtelling` er større enn 0. Variabelen `nedtelling` er nå 9, så den gjentar koden inni «munnen» på `gjenta`-klossen på ny.

    Dette fortsetter helt til variabelen `nedtelling` er 0. Da vil programmet gå videre i koden og vise firkanten på skjermen som er plassert under `gjenta`-klossen.

    Fordi variabelen `nedtelling` begynte som tallet 10, så blir koden inni `gjenta`-klossen gjentatt ti ganger før `nedtelling` er blitt 0. I løpet disse ti gjentagelsene har også programmet tatt ti pauser på 1 millisekund hver. Det betyr at vi har laget en nedtelling som totalt varer i 10 millisekund.

## Steg 4: Lage reglene for når en spiller vinner eller taper

I denne delen skal vi kode reglene for reaksjonspillet ved å bruke klosser fra `Logikk` kategorien. Vi ønsker at når en spiller er den første til å trykke på sin knapp når firkanten vises på skjermen vinner spillet.

Vi ønsker også å kode en regel som gjør at hvis en spiller trykker på sin knapp før firkanten er blitt vist, så taper den spilleren som trykket.

Begynn med å finne en `hvis ellers`-kloss fra kategorien `Logikk`. Plasser klossen inni «munnen» til `når knapp A trykkes`-klossen. Pass på at `vis skjerm`-klossen plasseres inni «munnen» under `hvis`-klossen.

```blocks
input.onButtonPressed(Button.A, function () {
    if (true) {
        basic.showLeds(`
            . . # . .
            . # . . .
            # # # # #
            . # . . .
            . . # . .
            `)
    } else {

    }
})
```

Finn å en `0 = 0`-kloss fra `Logikk` og plasser den på verdifeltet til `hvis ellers`-klossen.

```blocks
input.onButtonPressed(Button.A, function () {
    if (0 == 0) {
        basic.showLeds(`
            . . # . .
            . # . . .
            # # # # #
            . # . . .
            . . # . .
            `)
    } else {

    }
})
```

Plasser så `nedtelling`-klossen fra variabler på verdifeltet til venstre for er lik i `0 = 0`-klossen.

```blocks
input.onButtonPressed(Button.A, function () {
    if (nedtelling == 0) {
        basic.showLeds(`
            . . # . .
            . # . . .
            # # # # #
            . # . . .
            . . # . .
            `)
    } else {
        basic.showLeds(`
            . . # . .
            . . . # .
            # # # # #
            . . . # .
            . . # . .
            `)
    }
})
```

Gjenta så Steg 5 fra begynnelsen for `når knapp B trykkes`-klossen.

```blocks
input.onButtonPressed(Button.B, function () {
    if (nedtelling == 0) {
        basic.showLeds(`
            . . # . .
            . . . # .
            # # # # #
            . . . # .
            . . # . .
            `)
    } else {
        basic.showLeds(`
            . . # . .
            . # . . .
            # # # # #
            . # . . .
            . . # . .
            `)
    }
})
```

!!! warning "Pass på!"
    Husk at pilene er omvendt i `når knapp B trykkes`-klossen sammenlignet med `når knapp A trykkes`-klossen.

!!! success "Test programmet"

## Skjekke om spillet kjører

!!! success "Test programmet"
    Overfør det ferdige programmet til Micro Biten ved å bruke en USB-kabel eller Blåtann. Spør en lærer om hjelp hvis du er usikker. Rist på terningen din og sjekk at programmet fungerer riktig.

Gratulerer, du har nå laget et reaksjonspill. Start spillet med å trykke på A og B-knappene på Micro Biten samtidig. Hvem er raskest av deg og en venn?

!!! question "Utfordring"
    Spillet vårt kan få flere funksjoner. Se om du kan legge til en nedtelling før spillet begynner på egenhånd. Eller se om du klarer å programmere ved å bruke boolske variabler slik at hvis en spiller trykker for tidlig så taper han eller henne.

[^1]:
    Det finnes mange forskjellige programmeringssider og -apper for Micro Bit. Bruk den siden eller appen som du har lært i undervisningen.