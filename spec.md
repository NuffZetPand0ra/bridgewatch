# Bridgeur spec

## Hvad skal hvert enkelt bridgeur kunne?

* Starte/Pause.
* Nulstille til start.
* Nulstille til starten af nuværende historiepunkt.
* Starte på et foruddefineret tidspunkt.
* Planlægge en turneringshistorie (se eksempel). Tænker at det er nemt at generere.
* Vise en turneringshistorie med noget pretty print, og computede klokkeslet, samt hvor langt vi er nået i historien.


### Eksempel på historie

En historie er et array med historiepunkt objects. Hvert object indeholder data om længde, visning og andet:

* `isRound` definerer om det er en runde eller en pause/andet. Hvis det er en runde skal `round_count` forøges, og et `round` skal forøges når runden er nået.
* `name` er displayet over timeren når dette historiepunkt er nået.
* `duration` er varigheden på historiepunktet i sekunder.
* `greeting` tænker jeg kan være enten kan være noget SSML, eller et keyword til en MP3 e.l.  
Afspilles når historiepunktet er nået under kørsel.
* `endNotif` Giv et beep når der er X sekunder tilbage af historiepunktet.

Hver gang et historiepunkt med `isRound==true` er nået under kørsel, tænker jeg at en `round` variabel forøges. Samtidig kan den vel også lige tælle hvor mange historiepunkter der er med `isRound==true`, og opdatere en `round_count` variabel derefter.

Json data:

    [
        {
            "isRound":  true,
            "name":     "Runde %round% af %round_count%.",
            "duration": 1620,
            "greeting": "Runde %round% starter.",
            "endNotif": 360
        },
        {
            "isRound":  false,
            "name":     "Skifter til runde %next_round%.",
            "duration": 90,
            "greeting": "Skifter til runde %next_round%."
        },
        {
            "isRound":  true,
            "name":     "Runde %round% af %round_count%.",
            "duration": 1620,
            "greeting": "Runde %round% starter.",
            "endNotif": 360
        },
        {
            "isRound":  false,
            "name":     "Pause",
            "duration": 360,
            "greeting": "Nyd fem minutters pause"
        },
        {
            "isRound":  true,
            "name":     "Runde %round% af %round_count%.",
            "duration": 1620,
            "greeting": "Runde %round% starter.",
            "endNotif": 360
        }
    ]

Man kunne sagtens lave et interface til historiepunkter, der har defaults på alt andet en `duration`.