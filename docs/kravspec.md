# Kravspec – Deadlines i uppgiftsappen

## 1. Problemet, med kundens egna ord
> "Vi är ett team på åtta personer som använder er uppgiftsapp varje dag. Problemet är att vi missar deadlines hela tiden, och ingen märker det förrän kunden ringer och är arg." /Sara, teamledare

Buggrapport: "Klockan nio på morgonen står det att 'Skicka offert' är en dag sen, fast den ska vara klar idag. Folk har slutat lita på listan."

## 2. Mål och hur vi vet att vi nått dem
| Nuläge | Mål | Tidsram | Hur vi mäter |
|---|---|---|---|
| Ca 6 av 10 uppgifter blir klara i tid | 85 % klara i tid | Inom 4 veckor | Systemet sparar när en uppgift blev klar och jämför med förfallodatumet |



## 3. Frågor vi ställde, och svaren
| # | Fråga | Saras svar |
|---|---|---|
| F1 | Hur många använder appen? | 8 personer i teamet |
| F2 | Hur många uppgifter blir klara i tid idag? | Ungefär 6 av 10 |
| F3 | När räknas en uppgift som försenad? | Inte förrän dagen är slut, 23:59 svensk tid |
| F4 | Kan en uppgift som är klar vara försenad? | Nej, aldrig |
| F5 | Hur snabbt måste listan laddas? | Under 200 ms, även när alla 8 öppnar den samtidigt |
| F6 | Vad händer idag när en deadline missas? | ❓ |
| F7 | Vad ska hända med uppgifter utan datum? | ❓ |
| F8 | Vem ska få veta när något blir försenat? | ❓ |
| F9 | Om en månad, vad har ändrats om vi lyckats? | 85 % klara i tid inom 4 veckor |



## 4. User stories med acceptanskriterier

### US-1: Se försenade uppgifter
Som teammedlem vill jag se vilka uppgifter som är försenade, så att jag kan agera innan kunden ringer.

- **AK-1.1** Givet en uppgift med förfallodatum igår, som inte är klar, när jag öppnar listan, så visas den som försenad.
- **AK-1.2** Givet en uppgift med förfallodatum idag, när klockan är 23:59 svensk tid, så är den inte försenad.
- **AK-1.3** Givet en uppgift som är klar, så är den aldrig försenad, oavsett datum.
- **AK-1.4** Givet att inga uppgifter är försenade, när jag öppnar listan, så visas en tom lista.



## 5. Use case: Se och åtgärda försenade uppgifter
**Aktör:** Teammedlem
**Mål:** Hinna göra försenade uppgifter innan kunden ringer

### Huvudflöde
1. Teammedlemmen öppnar appen.
2. Systemet visar de försenade uppgifterna överst.
3. Teammedlemmen gör uppgiften.
4. Teammedlemmen markerar uppgiften som klar.
5. Uppgiften försvinner från listan över försenade (AK-1.3).

### Alternativa flöden
- **A1. Inget är försenat:** systemet visar en tom lista (AK-1.4).
- **A2. Uppgiften ska vara klar idag:** den visas inte som försenad förrän dagen är slut (AK-1.2). *Det här är Kims bugg.*
- **A3. Uppgiften blir klar för sent:** den räknas som klar, men inte som "klar i tid" i mätvärdet.
- **A4. Uppgiften saknar datum:** ❓ (väntar på Saras svar, F7)

### Undantagsflöden
- **E1. API:t svarar inte:** ❓ vad ska användaren se?
- **E2. Uppgiften är borttagen av någon annan:** ❓ vad ska hända?
