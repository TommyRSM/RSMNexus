# Anvendelsesscenarier for RSM Nexus (første version)

## Formål
Dette dokument beskriver de tre første prioriterede anvendelsesscenarier for RSM Nexus i et format, der kan bruges direkte til backlog og videre specifikation.

Hvert anvendelsesscenarie indeholder:
- Forretningsmål
- Primære aktører
- Udløser
- Forudsætninger
- Hovedforløb
- Alternative forløb
- Afgrænsning for første version
- Acceptkriterier for første version
- Succeskriterier

---

## Anvendelsesscenarie 1: Planlægning og igangsætning af "rulning" af Caseware-fil

### Forretningsmål
RSM skal kunne igangsætte forberedelse af næste regnskabsår hurtigere og mere ensartet ved at kunne starte en "rulning" af en kundes Caseware-fil fra Nexus.

### Primære aktører
- Revisor
- Teamleder
- RSM Nexus (integration til Caseware)

### Udløser
Brugeren vælger en kunde i kundelisten og aktiverer handlingen "Start rulning".

### Forudsætninger
- Kunden findes i Nexus med gyldig reference til Caseware.
- Brugeren har rettigheder til at igangsætte rulning.
- Caseware-integration er tilgængelig.

### Hovedforløb (første version)
1. Brugeren åbner kundelisten i Nexus.
2. Brugeren vælger en kunde og trykker på knappen "Start rulning".
3. Nexus validerer, at kunden har nødvendige referencenøgler til Caseware.
4. Nexus sender en anmodning om rulning til Caseware.
5. Nexus viser status for igangsætning (fx "Igangsat" eller "Fejlet").
6. Handling og resultat logges til audit/formål.

### Alternative forløb
- **A1: Manglende Caseware-reference**  
  Nexus afviser handlingen og viser, hvad der mangler.
- **A2: Integration utilgængelig**  
  Nexus registrerer fejlen og viser en brugerforståelig fejlstatus.
- **A3: Manglende rettighed**  
  Nexus afviser handlingen med tydelig besked om manglende adgang.

### Afgrænsning for første version
- Kun manuel igangsætning via knap på kundeliste.
- Ingen regelmotor for automatisk planlægning endnu.

### Acceptkriterier for første version
- Brugeren kan starte rulning for én valgt kunde direkte fra kundelisten.
- Systemet viser straks, om anmodningen er modtaget eller afvist.
- Fejltilfælde vises med tydelig årsag (manglende reference, manglende rettighed eller integrationsfejl).
- Hver igangsætning kan spores i log med tidspunkt, bruger og resultat.

### Fremtidig udvidelse
- Automatisk planlægning baseret på kriterier som:
  - Forrige års status
  - Dato for regnskabsårets afslutning
  - Kundetype/segment
  - Ressourcekapacitet

### Succeskriterier
- En bruger kan igangsætte rulning på under 30 sekunder.
- Mindst 95 % af gyldige igangsætninger opnår en teknisk kvittering uden manuel genkørsel.

---

## Anvendelsesscenarie 2: Oprettelse af ny kunde med sekventielt godkendelsesforløb

### Forretningsmål
Nye kunder skal oprettes ensartet og compliance-mæssigt korrekt via et styret forløb, hvor AML/KYC-godkendelse sker før oprettelse i de øvrige kernesystemer.

### Primære aktører
- Kundevendt medarbejder
- Compliance-medarbejder (via Creditro)
- RSM Nexus (orkestrering)
- Creditro
- Uniconta
- Microsoft Teams

### Udløser
Brugeren vælger "Opret ny kunde" i Nexus.

### Forudsætninger
- Brugeren har rettighed til at oprette kunder.
- CVR og øvrige minimumsdata kan valideres.
- Integrationer til Creditro og Uniconta er konfigureret.

### Hovedforløb (første version)
1. Brugeren opretter kunde i Nexus med CVR og nødvendige stamdata.
2. Nexus opretter kunden i status "Afventer AML/KYC".
3. Nexus starter et Creditro-forløb for kunden.
4. Nexus afventer godkendelsesstatus fra Creditro.
5. Når kunden er godkendt i Creditro, opretter Nexus kunden i Uniconta.
6. Uniconta-oprettelsen udløser automatisk oprettelse af Team i Microsoft Teams.
7. Nexus opdaterer kunden til "Aktiv" og viser links til tilknyttede systemer.

### Alternative forløb
- **B1: Kredit-/compliance-afvisning i Creditro**  
  Kunden markeres som "Afvist"; oprettelse i Uniconta/Teams stoppes.
- **B2: Timeout eller teknisk fejl mod Creditro**  
  Kunden forbliver i "Afventer AML/KYC" med fejlstatus og mulighed for genforsøg.
- **B3: Fejl ved oprettelse i Uniconta**  
  Sagen markeres til manuel opfølgning; Teams-oprettelse afventes.

### Afgrænsning for første version
- Fokus på standardforløb med én juridisk enhed.
- Ingen avanceret forløbskonfiguration pr. kundetype.
- Ingen parallel oprettelse i andre satellitsystemer end de nævnte.

### Acceptkriterier for første version
- Oprettelse i Uniconta må først ske, når Creditro har returneret godkendt status.
- Hvis Creditro afviser kunden, må Uniconta og Teams ikke blive oprettet.
- Brugeren kan altid se, hvilken status kunden er i (afventer, afvist, aktiv, fejl).
- Fejl i integrationer markeres tydeligt og kan følges op manuelt.

### Succeskriterier
- 100 % af kunder oprettes i korrekt sekvens: Nexus -> Creditro-godkendelse -> Uniconta -> Teams.
- Der er fuld sporbarhed i statusskift for hver kundeoprettelse.

---

## Anvendelsesscenarie 3: Moderne kundeoverblik med dybe links og nøgleoplysninger

### Forretningsmål
Brugere skal have ét visuelt klart og moderne kundeoverblik, hvor de både kan se nøgledata og hurtigt åbne relevante kundekontekster i tilknyttede systemer.

### Primære aktører
- Revisor
- Kundevendt medarbejder
- Compliance-medarbejder

### Udløser
Brugeren åbner en kunde i Nexus.

### Forudsætninger
- Kunden er oprettet med referencenøgler til relevante systemer.
- Brugeren er autentificeret og autoriseret.

### Hovedforløb (første version)
1. Brugeren åbner kundens overbliksside.
2. Nexus viser nøgleoplysninger (fx CVR, kundenummer, status, seneste opdatering).
3. Nexus viser links til kundens kontekst i:
   - Microsoft Teams
   - Creditro
   - Uniconta
   - RGDatabank
   - Caseware
4. Brugeren kan åbne et link og fortsætte arbejdet i målsystemet.

### Alternative forløb
- **C1: Manglende reference til et system**  
  Link vises som utilgængeligt med forklaring.
- **C2: Utilstrækkelig rettighed til et system**  
  Brugeren informeres om manglende adgang.
- **C3: Midlertidigt systemnedbrud**  
  Nexus viser driftsstatus og anbefalet næste handling.

### Afgrænsning for første version
- Fokus på informationskort og links (ikke avancerede dashboards/analytics).
- Begrænset personalisering af visning per rolle.

### Acceptkriterier for første version
- Overblikket viser mindst CVR, internt kundenummer, overordnet status og seneste opdatering.
- Links til Teams, Creditro, Uniconta, RGDatabank og Caseware vises samlet i kundeoverblikket.
- Manglende integration eller manglende adgang vises som tydelig status frem for døde links.
- Brugerens adgangsniveau afgør, hvilke informationer og links der vises.

### Succeskriterier
- Brugeren kan finde centrale kundeoplysninger og åbne relevante systemer fra én side uden ekstra søgning.
- Overblikket reducerer tid til opgavestart sammenlignet med nuværende arbejdsgang.

---

## Tværgående krav for alle tre anvendelsesscenarier
- Rollebaseret adgangsstyring skal håndhæves i alle forløb.
- Alle kritiske handlinger skal logges for sporbarhed.
- Fejlbeskeder skal være forståelige og handlingsanvisende.
- Integrationer skal være robuste over for midlertidige fejl (genforsøg og tydelig status).

## Forslag til prioriteret implementeringsrækkefølge
1. Anvendelsesscenarie 3 (kundeoverblik med links), så brugerne hurtigt får et fælles indgangspunkt.
2. Anvendelsesscenarie 2 (kundeoprettelse), så masterdata- og compliance-forløbet standardiseres.
3. Anvendelsesscenarie 1 (rulning af Caseware-fil), som derefter kan udvides med automatisk planlægning.
