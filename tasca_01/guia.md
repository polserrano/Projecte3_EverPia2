# Guia d’Ús Tècnica – Bitwarden

**- Autor:** Pol Serrano Aromí
**- Data:** 24/10/2025

## 🠲 1. Instal·lació i Configuració Inicial

### 1.1 Descàrrega i Instal·lació:
1. Accedeix a la web oficial: https://bitwarden.com/es-la/download/
2. Descarregem la versió adequada segons els nostre sistema operatiu:
   - **Windows:** Bitwarden Desktop  
   - **macOS / Linux:** Versió corresponent  
   - **Mòbil:** App Store (iOS) o Google Play (Android)
  
![imatge1](/tasca_01/img/imatge_01.png)

### 1.2 Creació del Compte Mestre:
1. Obrim bitwarden i li donem a **“Create Account”**.  
2. Introduim:
   - Correu electrònic
   - Contrasenya mestra **(haura de tenim min 12 caràcters amb mayus, minúscules, números i símbols)**   
3. Revisem la safata d'entrada del correu que hem posat associat
4. Per últim pas, iniciem sessió

![imatge2](/tasca_01/img/imatge_02.png)

5. Una recomanació que us donc, és habilitar el factor de autentificació (2FA)

---

## 🠲 2. Generació de Contrasenyes Segures

### 2.1 Ús del Generador de Contrasenyes
1. Al panell principal, fes clic a Ctrl+g, per generar contrasenyes segures i us sortirà un menu.  
2. Podrem escollir entre:
   - Contrasenya aleatòria
   - Passphrase (frase de paraules aleatòries)
   - Nom d'usuari
3. Configura els paràmetres recomanats:
   - Longitud: 18 és ho recomanable, però pots utilitzar entre 18 i 20
   - Incloure: majúscules, minúscules, números i símbols
4. Desa o copia la contrasenya que es genera.

![imatge3](/tasca_01/img/imatge_03.png)
---

## 🠲 3. Exemples d’Ús i Emplenament Automàtic

### 3.1 Desar una Credencial d’un Compte de Correu
1. Fes clic al **+** que et surt abaix del software de bitware.  
2. Completem els camps:
   - **Nom:** Gmail (en el meu cas) 
   - **Nom d’usuari:** aqui posem el correu
   - **Contrasenya:** enganxa la generada  
   - **URL:** `https://mail.google.com` o el servei corresponent  
3. Finalment desem.
4. Aqui teniu un exemple fet per mi en google.

![imatge4](/tasca_01/img/imatge_04.png)

### 3.2 Desar una Credencial d’una Aplicació o Servei Web
1. Farem el mateix que el pas anterior, pero en aquests cas jo ho fare en la web de trello.

![imatge5](/tasca_01/img/imatge_05.png)

### 3.3 Ús de l’Extensió del Navegador
1. Instal·la l’extensió des de https://bitwarden.com/download/
2. Inicia sessió amb el teu compte.  
3. Quan visitis una pàgina d’inici de sessió, Bitwarden detectarà les credencials automàticament.  
4. Prem la icona de Bitwarden i selecciona **“Autofill”**.

---

## 🠲 4. Gestió de Còpies de Seguretat (Backup)

### 4.1 Crear una Còpia de Seguretat
1. Ves a: adaalt esquerra, fitxer --> Exporta caixa forta
2. Tria el format **.json** o **.csv**.  
3. Desa l’arxiu en una ubicació segura (no compartida).  

### 4.2 Bones Pràctiques de Seguretat
- **Mai** guardis l’arxiu d’exportació en text pla a l’ordinador.  
- Desa’l en un suport segur com:
  - **Clau USB xifrada**
  - **Emmagatzematge al núvol amb xifratge (Tresorit, Proton Drive, OneDrive xifrat)**  
- Actualitza la còpia de seguretat **cada mes** o després de canvis importants.

---

## 🠲 5. Resum de Bones Pràctiques

| Acció | Recomanació |
|-------|--------------|
| Contrasenya mestra | Més de 12 caràcters, complexa, única |
| 2FA | Sempre activat |
| Compartició de credencials | Només mitjançant “Organizations” de Bitwarden |
| Backups | Mensuals i sempre xifrats |
| Actualització | Mantén aplicacions i extensions al dia |
