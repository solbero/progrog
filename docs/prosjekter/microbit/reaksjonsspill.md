# Lag et reaksjonsspill med Micro Bit

<iframe width="768" height="432" src="https://www.youtube.com/embed/obrNe2_qAKU" frameborder="0" modestbranding="1" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Introduksjon

Dette er en oppskrift som passer for deg som har programmert litt på Micro Bit fra før. Oppskriften tar omtrent en time å gjennomføre. Du skal i denne oppskriften lage et reaksjonsspill for to spillere.

!!! abstract "Du vil lære"
    * å vise piler på skjermen til Micro Biten når en knapp trykkes
    * å lage en nøyaktig nedtelling
    * å programmere spilleregler
    * å bruke en variabel til å huske om noe har skjedd

!!! info "Du trenger"
    * en Micro Bit
    * en USB-kabel til overføring
    * en batteripakke med to AAA-batterier

## Steg 1: Vis en pil på skjermen til Micro Biten når en knapp trykkes

I dette steget skal vi fortelle Micro Biten at den skal vise en pil på skjermen når en knapp trykkes. Pilen skal peke mot knappen som ble trykt.

* Begynn med å åpne nettsiden <a href="https://makecode.microbit.org/" target="_blank">MakeCode for micro:bit</a>.

* Trykk på knappen `Nytt Prosjekt` for å starte et nytt prosjekt.

* Gi prosjektet navnet *Reaksjonsspill for to spillere* ved å skrive i tekstfeltet nederst på siden.

* Slett alle klossene som ligger i lærretet. Du sletter en kloss ved å dra den til venstre over kategoriene. Slipp klossen når søplespannet vises for å slette den.

Da er vi klar til å begynne å kode! Først skal vi lage pilen som peker mot A-knappen når den trykkes.

* Dra klossen `når knapp A trykkes`{:.input} fra kategorien `Inndata`{:.input} og slipp den et sted på lærretet.

* Finn klossen `vis bilde`{:.basic} i kategorien `Basis`{:.basic}. Ta tak i klossen og plasser den i munnen til `når A trykkes`{:.input}.

* Tegn en pil på `vis bilde`{:.basic}-klossen ved å trykke på de små firkantene. Pass på at pilen peker til venstre!

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
```

Da skal vi lage pilen som peker mot B-knappen når den trykkes.

* Dra klossen `når knapp A trykkes`{:.input} fra kategorien `Inndata`{:.input} og slipp den et sted på lærretet. Trykk på `A`{:.input} på `når knapp A trykkes`{:.input} og velg `B`{:.input} fra rullegardinmenyen.

* Finn klossen `vis bilde`{:.basic} og plasser den i munnen til `når B trykkes`{:.input}.

* Tegn en pil som peker mot høyre på `vis bilde`{:.basic}-klossen ved å trykke på de små firkantene.

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
    Til venstre er det bilde av en Micro Bit. Denne kan du bruke til å teste programmet ditt mens du koder. Trykk på `A`-knappen, da skal det vises en pil på skjermen som peker mot venstre. Etterpå prøver du å trykke på `B`-knappen. Da skal det vises en pil mot høyre.

!!! failure "Det virker ikke!"
    Peker ikke pilene mot knappene når du trykker på dem? Da er noe galt i koden din. For å finne feilen bør du lese oppskriften om igjen og se nøye på bildene.

## Steg 2: Lag en tilfeldig nedtelling

Vi vil at en prikk skal vises på skjermen til Micro Biten når reaksjonspillet begynner. På et tilfeldig tidspunkt mellom null til fem sekunder skal denne prikken bli til en firkant. For å få til dette må vi lage en tilfeldig nedtelling.

For å lage en tilfeldig nedtelling må reaksjonsspillet huske tre tidspunkter:

1. Når nedtellingen starter
2. Hvor lenge nedtellingen varer
3. Når nedtellingen slutter

Disse tre tidspunktene skal reaksjonsspillet huske med å bruke tre variabler. Vi begynner med å lage variablene vi trenger.

Legg merke til at klossene fra forrige steg vil fortsatt være i lærretet ditt på MakeCode. De skal ikke slettes selv om kun klossene for dette steget vises under.

* Ta klossen `ved start`{:.basic} fra kategorien `Basis`{:.basic} og plasser den på lærretet.
* Trykk på kategorien `Variabler`{:.variables} og deretter på knappen `Lag en variabel`. I tekstfeltet som vises på skjermen skriver du *starttid*.
* Plasser klossen `sett starttid til 0`{:.variables} i munnen til `ved start`{:.basic}.

```blocks
let starttid = 0
```

* Lag to variabler til i `Variabel`{:.variables}-kategorien ved å trykke på `Lag en variabel`. Den ene variabelen skal hete *ventetid* og den andre skal hete *sluttid*.
* Plasser `sett ventetid til 0`{:.variables} og `sett sluttid til 0`{:.variables} i munnen til `når starter`{:.variables}.

Klossene `sett … til 0`{:.variables} og `endre … med 0`{:.variables} i kategorien `Variabler`{:.variables} viser alltid navnet til den siste variabelen du laget. For å skifte navnet på en variabel-kloss må du dra klossen ut i lærretet og deretter trykke på firkanten som er rundt navnet på klossen. I rullegradinmenyen som da vises vil du kunne velge riktig variabel.

```blocks
let starttid = 0
let ventetid = 0
let sluttid = 0
```

* Finn klossen `kjøretid (ms)`{:.input} og plasser den på verdifeltet til `sett starttid til 0`{:.variables}. For å finne denne klossen må du først trykke på kategorien `Inndata`{:.input}. Når du har trykket på kategorien vil det dukke opp en kategori under `Inndata`{:.input} som heter `⋯ more`{:.input}. Trykk på den nye kategorien for å finne `kjøretid (ms)`{:.input}.

```blocks
let starttid = input.runningTime()
let ventetid = 0
let sluttid = 0
```

* Finn klossen `velg tilfeldig 0 til 10`{:.math} fra kategorien `Matematikk`{:.math}. Plasser den i verdifeltet til `sett ventetid til 0`{:.variables}.
* Skift tallet 10 til 5000 på `velg tilfeldig 0 til 10`{:.math}-klossen. Klossen `velg tilfeldig 0 til 5000`{:.math} vil nå velge en tilfeldig ventetid mellom 0 og 5000 millisekunder. Et millisekund er et tusenedelssekund. Det betyr at 5000 millisekunder er det samme som 5 sekunder.

```blocks
})
let starttid = input.runningTime()
let ventetid = Math.randomRange(0, 5000)
let sluttid = 0
```

Nå skal vi regne ut sluttiden for nedtellingen. Den regner vi ut ved å summere `starttid`{:.variables} og `ventetid`{:.variables} variablene.

* Ta klossen `0 + 0`{:.math} fra `Matematikk`{:.math}-kategorien og plasser den på verdifetet til `sett sluttid til 0`{:.math}.
* Plasser variabelene `starttid`{:.variables} og `ventetid`{:.variables} på verdifeltene til klossen `0 = 0`{:.math}.

```blocks
let starttid = input.runningTime()
let ventetid = Math.randomRange(0, 5000)
let sluttid = starttid + ventetid
```

Til slutt skal vi lage en prikken som skifter til en firkant på skjermen når ventetiden er løpt ut.

* Begynn med å plassere to `vis bilde`{:.basic}-klosser i munnen til `når starter klossen`{:.basic}. Pass på at begge klossene plasseres under variablene.
* Tegn en prikk på den øverste `vis bilde`{:.basic}-klossen og en firkant på den nederste `vis bilde`{:.basic}-klossen.
* Plasser deretter klossen `pause (ms) 0`{:.basic} fra `Basis`{:.basic}-kategorien mellom de to `vis bilde`{:.basic}-klossene.
* Plasser variabelen `ventetid`{:.variables} på verdifeltet til `pause (ms) 0`{:.basic}-klossen.

```blocks
let starttid = input.runningTime()
let ventetid = Math.randomRange(0, 5000)
let sluttid = starttid + ventetid
basic.showLeds(`
    . . . . .
    . . . . .
    . . # . .
    . . . . .
    . . . . .
    `)
basic.pause(ventetid)
basic.showLeds(`
    . . . . .
    . # # # .
    . # . # .
    . # # # .
    . . . . .
    `)
```

!!! success "Test programmet"
    Micro Biten til venstre på MakeCode skal nå vise en prikk som blir til en firkant på et tilfeldig tidspunkt. Trykk på `🔃` under Micro Biten for å kjøre koden igjen. Tiden det tar før prikken blir en forkant skal være ulik hver gang du trykker på `🔃`.

!!! failure "Det virker ikke!"
    Hvis ikke prikken blir til en firkant på Micro Biten så er noe galt i koden din. For å finne feilen bør du se nøye på bildene i oppskriften og sammenligne dem med din kode. En vanlig feil er å plassere gale klosser på verdifeltene til `sett … til`{:.variables}-klossene

!!! question "Utfordring"
    Prikken vil bli til en firkant på skjermen til Micro Biten etter at det har gått fra 0 til 5 sekunder. Hva må du skifte i koden din hvis du vil at firkanten skal vises når det har gått fra 2 til 8 sekunder?

## Steg 3: Lage reglene for når en spiller vinner eller taper

Nå må vi lage noen regler for reaksjonsspillet. Reglene forteller spillet hvem som vinner eller taper. For å få til dette må bruke to regler:

1. Hvis en spiller trykker på sin knapp etter at firkanten vises på skjermen så vinner spilleren som trykket knappen.
2. Hvis en spiller trykker på sin knapp før firkanten vises på skjermen så vinner så taper spilleren som trykket knappen.

Først skal vi programmere den første regelen. Dette er regelen som forteller reaksjonspillet at en spiller har trykket på sin knapp etter at firkanten er dukket opp på skjermen.

* Finn klossen `hvis sann`{:.logic} fra kategorien `Logikk`{:.logic}. Dra klossen over `hvis knapp A trykkes`{:.input}-klossen og slipp den når `vis bilde`{:.basic}-klossen er i munnen på `hvis sann`{:.logic}-klossen.

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
    }
})

```

* Trekk klossen `0 < 0`{:.logic} fra kategorien `Logikk`{:.logic} og plasser den på verdifetet til `hvis sann`{:.logic}-klossen.

```blocks
input.onButtonPressed(Button.A, function () {
    if (0 < 0) {
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

* Finn variabelen `sluttid`{:.variables} fra `Variabel`{:.variables}-kategorien og plasser klossen på det venstre verdifeltet på `0 < 0`{:.logic}-klossen.
* Finn klossen `kjøretid (ms)`{:.input} fra `Inndata`{:.input}-kategorien plasserer klossen på det høyre verdifeltet på `sluttid < 0`{:.logic}-klossen.

```blocks
input.onButtonPressed(Button.A, function () {
    let sluttid = 0
    if (sluttid < input.runningTime()) {
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

Nå har vi programmert den første regelen til reaksjonsspillet. Heldigvis er det enklere å fortelle spillet om den andre regelen.

* Trykk på `+`-knappen nederst på `hvis sluttid < kjøretid (ms)`{:.logic}-klossen. Klossen vil da bli til en `hvis sluttid < kjøretid (ms) ellers`{:.logic}-kloss.

```blocks
input.onButtonPressed(Button.A, function () {
    let sluttid = 0
    if (sluttid < input.runningTime()) {
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

* Finn en `vis bilde`{:.basic}-kloss og plasser i munnen på `ellers` på `hvis sluttid < kjøretid (ms) ellers`{:.logic}-klossen.
* Tegn en pil på `vis bilde`{:.basic}-kloss som peker motsatt vei `vis bilde`{:.basic}-klossen over den.

```blocks
input.onButtonPressed(Button.A, function () {
    let sluttid = 0
    if (sluttid < input.runningTime()) {
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

Da har vi fortalt spillet om den andre regelen.

Til slutt i dette steget skal vi fortelle spillet at det skal starte på nytt etter at en knapp er trykket. For å starte programmet på nytt skal vi bruke klossen `tilbakestill`.

* Ta klossen `pause (ms) 100`{:.basic} og plasser den under `hvis sluttid < kjøretid (ms) ellers`{:.logic}-klossen. Skift tallet i verdifeltet til 2000.
* Finn klossen `tilbakestill`{:.control} i kategorien `Styring`{:.control}. Kategorien `Kontroll`{:.control} finner du ved å først trykke på `Avansert` i kategoriskuffen. Da vil skuffen vise mange flere kategorier.
* Ta tak i `tilbakestill`{:.control}-klossen og plasser den under `pause (ms) 2000`{:.basic}-klossen.

```blocks
input.onButtonPressed(Button.A, function () {
    if (sluttid < input.runningTime()) {
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
    basic.pause(2000)
    control.reset()
})
```

Gjenta hele steget du akkurat har gjort for `hvis knapp B trykkes`{:.input}-klossen. Når du er ferdig skal`hvis knapp B trykkes` se ut som bildet under. Legg merke til at pilene peker motsatt vei sammenlignet med `hvis knapp B trykkes`{:.input}.

```blocks
input.onButtonPressed(Button.B, function () {
    if (sluttid < input.runningTime()) {
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
    basic.pause(2000)
    control.reset()
})
```

!!! success "Test programmet"
    Prøv å trykke på en av knappene på Micro Biten etter at firkanten dukker opp på skjermen. Da skal pilen som vises på skjermen peke mot knappen som ble tyrkt. Etter at pilen er blitt vist i to sekunder skal reaksjonsspillet starte på nytt. Prøv også å trykke på en av knappene før prikken blir til en firkant. Pilen skal nå peke mot den andre knappen.

!!! failure "Det virker ikke!"
    Peker ikke pilene riktig når du trykker på knappene? Eller starter ikke reaksjonsspillet på nytt når du trykker en knapp? Da er noe galt i koden din. For å finne feilen bør du lese dette steget om igjen og se nøye på bildene.

## Steg 4: Sjekke om en spiller har trykket sin knapp

Nå er reaksjonsspillet nesten ferdig, men det er et par ting som gjenstår. Vi må legge til en *tilstand* i spillet. En tilstand forteller spillet om noe har skjedd eller ikke. Tilstanden vi skal sjekke er om en av spillerne har trykket på sin knapp.

* Finn en `hvis sann`{:.logic}-kloss fra `Logikk`{:.logic}-kategorien. Plasser klossen i munnen til `hvis knapp A trykt`{:.input}-klossen og i tillegg rundt `hvis sluttid < kjøretid (ms) ellers`{:.logic}-klossen.
* Dra en `ikke`{:.logic}-kloss fra `Logikk`{:.logic}-kategorien og plasser de på verdifeltet til `hvis sann`{:.logic}-klossen.
* Lag en ny variabel som heter `knapp_er_trykt`{:.variables}.
* Drar `knapp_er_trykt`{:.variables}-klossen fra `Variabel`{:.variables}-kategorien og plasserer den på verdifeltet til `ikke`{:.logic}-klossen.

```blocks
input.onButtonPressed(Button.A, function () {
    let er_knapp_trykt = 0
    if (!(er_knapp_trykt)) {
        if (sluttid < input.runningTime()) {
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
        basic.pause(2000)
        control.reset()
    }
})
```

* Finn `sett knapp_er_trykt til`{:.variables}-klossen fra `Variabel`{:.variables}-kategorien. Plasser klossen ovenfor `hvis sluttid < kjøretid (ms) ellers`{:.logic}-klossen.
* Ta klossen `sann`{:.logic} fra kategorien `Logikk`{:.logic} og plasser den på verdifeltet til `sett knapp_er_trykt til`{:.variables}-klossen.

```blocks
input.onButtonPressed(Button.A, function () {
    if (!(er_knapp_trykt)) {
        er_knapp_trykt = true
        if (sluttid < input.runningTime()) {
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
        basic.pause(2000)
        control.reset()
    }
})
```

De siste klossen du skal plassere er en `hvis sann`{:.logic}-kloss Denne klosse skal sjekke om en knapp er blitt trykt. Den gjør at firkanten kun dukker opp på skjermen hvis ingen knaper er blitt trykt på av spillerne.

* Finn klossen `hvis sann`{:.logic} fra kategorien `Logikk`{:.logic}. Plasser klossen rundt `vis bilde`{:.basic}-klossen er plassert i kunnen til `ved start`{:.basic}-klossen.
* På verdifeltet til `hvis sann`{:.logic}-klossen plasserer du først en `ikke`{:.logic}-kloss og så variabelen `knapp_er_trykt`{:.variables}.

```blocks
let sluttid = 0
let starttid = input.runningTime()
let ventetid = Math.randomRange(0, 5000)
sluttid = starttid + ventetid
basic.showLeds(`
    . . . . .
    . . . . .
    . . # . .
    . . . . .
    . . . . .
    `)
basic.pause(ventetid)
if (!(knapp_er_trykt)) {
    basic.showLeds(`
        . . . . .
        . # # # .
        . # . # .
        . # # # .
        . . . . .
        `)
}
```

Da er du ferdig! Hele koden til reaksjonsspillet skal se ut som på bildet under.

```blocks
input.onButtonPressed(Button.A, function () {
    if (!(knapp_er_trykt)) {
        knapp_er_trykt = true
        if (sluttid < input.runningTime()) {
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
        basic.pause(2000)
        control.reset()
    }
})
input.onButtonPressed(Button.B, function () {
    if (!(knapp_er_trykt)) {
        knapp_er_trykt = true
        if (sluttid < input.runningTime()) {
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
        basic.pause(2000)
        control.reset()
    }
})
let knapp_er_trykt = false
let sluttid = 0
let starttid = input.runningTime()
let ventetid = Math.randomRange(0, 5000)
sluttid = starttid + ventetid
basic.showLeds(`
    . . . . .
    . . . . .
    . . # . .
    . . . . .
    . . . . .
    `)
basic.pause(ventetid)
if (!(knapp_er_trykt)) {
    basic.showLeds(`
        . . . . .
        . # # # .
        . # . # .
        . # # # .
        . . . . .
        `)
}
```

!!! success "Test programmet"
    Prøv å trykke på en knapp på Micro Biten før firkanten vises på skjermen. Pilen skal da peke mot den knappen som ikke ble trykt. Når spillet har startet på nytt prøver du å trykke på en knapp etter at firkanten dukker opp på skjermen. Pilen skal da peke mot den knappen du trykte. Prøv så å trykke på en knapp og rett etterpå den andre knappen. Pilene skal ikke skifte retning når du gjør dette.

!!! failure "Det virker ikke!"
    Vises firkanten på skjermen etter etter at du har trykt på en knapp? Eller skifter pilen retning når du trykker på begge knappene raskt etter hverandre? Da er noe galt i koden din. For å finne feilen bør du lese dette steget om igjen og se nøye på bildene.

## Avslutning

Gratulerer, du har nå laget et reaksjonspill! Hvis du testet programmet ditt på slutten av forrige steg og ikke fant noen feil så skal du nå overføre programmet til Micro Biten.

* Koble Micro Biten til datamaskinen din med en USB-kabel.
* Trykk på tannhjulet øverst til høyre på siden og velg `Koble sammen`.
* Nå vises en dialogboks på siden. Trykk på knappen `Koble sammen`.
* Velg *BBC micro:bit CMSIS-DAP* eller *DAPLink CMSIS-DAP* fra listen som vises og trykk på knappen `Sammenkoble`.
* Trykk til slutt på knappen `Last ned` nederst til venstre på siden for å overføre programmet til Micro Biten.

Da er det på tide å spille spillet! Hvem er raskest av deg og en venn?

[^1]:
    Det finnes mange forskjellige programmeringssider og -apper for Micro Bit. Bruk den siden eller appen som du har lært i undervisningen.