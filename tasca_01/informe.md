# Fase 1: Anàlisi i Justificació
- **Autor:** Pol Serrano Aromí
- **Data:** 21/10/2025

---
### 🠲 1. Introducció i Justificació:
#### Per què les contrasenyes febles o reutilitzades són un risc?
Les contrasenyes febles o reutilitzades són un gran error, ja que si ens posem en el cas, de que un ciberdelinqüent la descobreix, i de sobte té accés a tota la teva correspondència, als teus comptes de xarxes socials i fins i tot a informació més crítica, com dades bancàries. Aquest tipus d’atacs no són teòrics ni distants, passen cada dia, i el resultat pot ser devastador: des del robatori d’identitat fins a la pèrdua de dades sensibles.

A més, la reutilització de contrasenyes agreuja encara més el problema. Els ciberdelinqüents sovint utilitzen tècniques de credential **stuffing**, que consisteixen a prendre combinacions d'usuari i contrasenya filtrades d'altres fuites de dades i provar-les en diferents serveis i comptes.

Aquestes vulnerabilitats no només poden permetre l'accés no autoritzat a dades sensibles, sinó que també poden provocar interrupcions en el funcionament de l'empresa, pèrdues econòmiques i greus danys a la reputació. Per això, és fonamental implementar polítiques de **gestió de contrasenyes**, com l’ús de **contrasenyes fortes**, **l’autenticació multifactor** i més.

### La importància d’una bona gestió de les contrasenyes
La funció crucial d’un gestor de contrasenyes per mitigar riscos és garantir la seguretat i la gestió eficient de les credencials d’accés. Concretament, això implica:

- **Generació de contrasenyes fortes i úniques:** Els gestors creen contrasenyes complexes, difícils de desxifrar, que es poden utilitzar exclusivament per a cada compte, evitant l’ús repetitiu.

- **Emmagatzematge xifrat:** Les contrasenyes es guarden de manera xifrada dins del gestor, protegint-les contra accés no autoritzat i minimitzant el risc de robatori.

- **Facilitar l’autenticació:** Amb l’autocompletat i la sincronització entre dispositius, permeten als usuaris accedir fàcilment als seus comptes sense haver de recordar o anotar contrasenyes.

En conclusió, un gestor de contrasenyes és molt útil per a empreses o persones per per acabar de assegurar totes les seves contrasenyes de qualsevol pàgina o aplicació.

---
### 🠲 2. Comparativa Tècnica:

---
### 🠲 3. Avantatges i inconvenients:

A continuació us mostrare las avantatges i inconvenients de cada model, online i offline, desde un punt de vista seguretat, usabilitat i continuïtat del negoci:

**3.3 Bitwarden (Solució en línia / Núvol)**

**3.3.1 - Avantatges**

- **Codi obert i seguretat:** Utilitza xifratge AES-256 amb arquitectura knowledge, garantint que només l'usuari pot accedir a les seves dades. 

- **Sincronització entre dispositius:** Permet l'accés a les contrasenyes des de qualsevol dispositiu amb connexió a Internet. 

- **Pla gratuït generós:** Inclou emmagatzematge il·limitat de contrasenyes i sincronització entre dispositius. 

- **Funcions per a usuaris premium:** Inclou autenticació de dos factors, accés d'emergència i emmagatzematge segur de fitxers. 

- **Opció d'auto-hospedatge:** Permet als usuaris o organitzacions allotjar el servei en els seus propis servidors per un control total. 

**3.3.2 - Inconvenients**

- **Interfície:** Alguns usuaris troben que les funcions d'ompliment i auto-desar requereixen varios clics i no són tan fluides com en altres. 

- **Limitació en el pla gratuït:** Algunes funcions com la sincronització entre dispositius, poden estar restringides en el pla gratuït. 

- **Manca de funcions avançades:** Algunes funcions com alertes de phishing o ompliment automàtic d'adreces poden no estar disponibles.

- **Problemes amb l'exportació de contrasenyes:** Usuaris han reportat problemes amb la funció d'exportació, incloent-hi la pèrdua de dades. 

**3.4 KeePassXC (Solució local / Escriptori)**

**3.4.1 - Avantatges**

- **Emmagatzematge local i control total:** Les dades es guarden en un fitxer .kdbx xifrat localment, sense necessitat de connexió a Internet. 

- **Codi obert i seguretat millorada:** Utilitza xifratge AES-256 amb derivació de clau Argon2, garantint una protecció robusta. 

- **Funcionalitats avançades:** Inclou generació de contrasenyes d'un sol ús (TOTP), integració amb SSH-agent i autocompletar amb teclat. 

- **Portabilitat del fitxer de base de dades:** El fitxer .kdbx es pot emmagatzemar en dispositius USB o serveis de núvol per facilitar l'accés. 

**3.4.2 - Inconvenients**

- **Sincronització manual:** Requereix configuració manual per sincronitzar entre dispositius, amb el risc de conflictes si es modifica. 

- **Manca d'aplicacions mòbils:** No disposa d'aplicacions mòbils oficials, els usuaris han de confiar en aplicacions de tercers per a mòbils. 

- **Curva d'aprenentatge més pronunciada:** Algunes funcions avançades poden ser difícils de configurar per a usuaris sense experiència. 

- **Sense mecanismes de recuperació:** En cas de pèrdua de la contrasenya mestra, no hi ha mecanismes de recuperació. 

---
### 🠲 4. Recomanació Final:

---
### 🠲 5. Webgrafia

- **1/** https://www.incibe.es/ciudadania/blog/gestores-de-contrasenas-como-funcionan
- **2/** https://www.keepersecurity.com/blog/es/2025/07/18/8-features-to-look-for-in-a-password-manager/
- **3/** https://es.wikipedia.org/wiki/Bitwarden
- **4/** https://es.wikipedia.org/wiki/KeePassX
- **5/** https://www.passwordmanager.com/bitwarden-vs-keepass/
- **6/** https://www.wizcase.com/blog/bitwarden-vs-keepass/
- **7/** https://www.ticges.com/els-errors-que-cometem-amb-les-contrasenyes-estas-segur-que-la-teva-es-segura/

---
## Gràcies per la vostra atencio!

- [Torna a la pàgina principal](../)
