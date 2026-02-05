# RSM Nexus – High Level Design (HLD)

## 1. Purpose
Dette dokument beskriver det overordnede design for **RSM Nexus**.  
Formålet er at give et fælles overblik over systemets rolle, arkitektur, integrationer og centrale funktioner på et højt niveau.

Dokumentet er ikke en detaljeret teknisk specifikation, men fungerer som et fælles referencepunkt for forretning, IT og videre design- og udviklingsarbejde.

---

## 2. Scope

### 2.1 In Scope
RSM Nexus skal fungere som:
- Centralt navigations- og indgangspunkt for kundearbejde
- Bindeled mellem udvalgte interne og eksterne systemer
- Platform for fælles funktioner og automatiseringer relateret til kunder

### 2.2 Out of Scope (for nu)
- Detaljeret UI/UX-design
- Implementeringsdetaljer på kode- og API-niveau
- Udskiftning af eksisterende kernesystemer

---

## 3. System Overview
RSM Nexus er en applikation, der samler adgang til og information fra flere systemer, hvor der arbejdes med kunder.

Systemet fungerer som:
- Ét samlet overblik over kunden
- Ét fælles startpunkt for arbejdsgange
- Et aktivt knudepunkt for integrationer og automatiseringer

---

## 4. System Integration Catalogue
Dette afsnit beskriver de konkrete systemer, som RSM Nexus forventes at integrere med, samt deres primære funktion og hvordan RSM Nexus anvender dem.

Formålet er at give et overblik over systemlandskabet og RSM Nexus’ rolle i forhold til hvert system.

### 4.1 Uniconta (kundestamdata)
**Rolle:**  
System of record for kundestamdata.

**Anvendelse i RSM Nexus:**  
- Synkronisering af CVR, kundenummer og øvrige masterdata
- Etablering af fælles kundereference på tværs af systemer

---

### 4.2 Microsoft Teams (kundemapper)
**Rolle:**  
Dokument- og filopbevaring for kunder.

**Anvendelse i RSM Nexus:**  
- Lagring og adgang til kundefiler
- Teams og kundestruktur oprettes automatisk baseret på Uniconta-kunder

---

### 4.3 Caseware (regnskabsproduktion)
**Rolle:**  
Primært fagsystem for revisorer til udarbejdelse af regnskaber.

**Anvendelse i RSM Nexus:**  
- Deep links til kundesager
- Visning af udvalgte kundefakta

---

### 4.4 Creditro (hvidvaskkontrol)
**Rolle:**  
Lovpligtig AML/KYC-kontrol af alle kunder.

**Anvendelse i RSM Nexus:**  
- Status- og compliance-overblik pr. kunde
- Dokumentation af kontrol

---

### 4.5 RGDatabank (skatte- og kundedata)
**Rolle:**  
Eksternt API med data- og skatteoplysninger om kunder.

**Anvendelse i RSM Nexus:**  
- Indhentning og visning af relevante skatte- og virksomhedsdata i kundeoverblikket

---

## 5. Core Capabilities

### 5.1 Navigation & Entry Point
- Fælles startside for kundearbejde
- Genveje og dybe links til underliggende systemer
- Konsistent navigation på tværs af systemlandskabet

### 5.2 Kundeoverblik
- Samlet visning af kunderelevant information
- Hurtig adgang til relaterede systemer og data
- Kontekstbaseret visning afhængigt af kundetype og rolle

### 5.3 Automatiseringer
- Understøttelse af automatiserede arbejdsgange
- System-til-system handlinger
- Trigger-baserede processer (fx hændelser, statusændringer)

---

## 6. High-Level Architecture
RSM Nexus fungerer som et centralt lag mellem brugere og underliggende systemer.

RSM Nexus indeholder en fælles kundekerne med udvalgte stam- og referenceoplysninger, herunder:
- CVR-nummer
- Internt kundenummer
- Grundlæggende kundedata
- Nøgler til relaterede systemer

Disse data anvendes til:
- Kundeoverblik
- Sammenkobling af information på tværs af systemer
- Videregivelse af konsistent kundekontekst til integrerede systemer

Detaljerede og fagspecifikke data forbliver primært i de respektive satellitsystemer, som fortsat fungerer som system of record for deres domæne.


---

## 7. Security & Compliance (High Level)
- Integration med eksisterende identitets- og adgangsstyring
- Rollebaseret adgang til funktioner og data
- Overholdelse af gældende sikkerheds- og compliancekrav (fx ISO 27001)

---

## 8. Assumptions
- Eksisterende systemer forbliver system of record
- Integrationer baseres primært på API’er
- Løsningen skal kunne udvides gradvist

---

## 9. Risks & Considerations
- Kompleksitet i integrationer
- Afhængighed af eksterne systemers stabilitet og API-kvalitet
- Brugeradoption og ændring af arbejdsgange

---

## 10. Future Considerations
- Udvidelse med yderligere automatiseringer
- Avanceret kundeindsigt og rapportering
- AI-baserede assistenter og beslutningsstøtte
