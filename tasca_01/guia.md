# Guia d’Ús Tècnica – Bitwarden

**- Autor:** Pol Serrano Aromí
**- Data:** 24/10/2025

## 1. Instal·lació i Configuració Inicial

### 1.1 Descàrrega i Instal·lació
1. Accedeix a la web oficial: [https://bitwarden.com/download/](https://bitwarden.com/download/)
2. Descarrega la versió adequada segons el teu sistema operatiu:
   - **Windows:** Bitwarden Desktop  
   - **macOS / Linux:** Versió corresponent  
   - **Mòbil:** App Store (iOS) o Google Play (Android)
  
![imatge1](/tasca_01/img/imatge_01.png)

### 1.2 Creació del Compte Mestre
1. Obre Bitwarden i selecciona **“Create Account”**.  
2. Introdueix:
   - Correu electrònic corporatiu  
   - Contrasenya mestra **(haura de tenim min 12 caràcters amb mayus, minúscules, números i símbols)**  
3. Accepta els termes i prem **“Submit”**.  
4. Inicia sessió amb el teu compte.

![imatge2](/tasca_01/img/imatge_02.png)

6. Una recomanació que us donc, és habilitar el factor de autentificació (2FA)

---

## 2. Generació de Contrasenyes Segures

### 2.1 Ús del Generador de Contrasenyes
1. Al panell principal, fes clic a Ctrl+g, per generar contrasenyes segures.  
2. Escull entre:
   - **Contrasenya aleatòria**
   - **Passphrase (frase de paraules aleatòries)**
3. Configura els **paràmetres recomanats**:
   - Longitud: 18 és ho recomanable, entre 18 i 20
   - Incloure: majúscules, minúscules, números i símbols
4. Desa o copia la contrasenya directament en una entrada del voltant.

![imatge3](/tasca_01/img/imatge_03.png)
---

## 3. Exemples d’Ús i Emplenament Automàtic

### 3.1 Desar una Credencial d’un Compte de Correu
1. Fes clic a **“+ Add Item”**.  
2. Completa els camps:
   - **Nom:** Gmail / Outlook / Correu corporatiu  
   - **Nom d’usuari:** `usuari@empresa.com`  
   - **Contrasenya:** enganxa la generada  
   - **URL:** `https://mail.google.com` o el servei corresponent  
3. Prem **Save**.

### 3.2 Desar una Credencial d’una Aplicació o Servei Web
1. Repiteix el procés anterior per serveis com **Jira**, **Trello**, **CRM**, etc.  
2. Pots afegir notes addicionals (departament, permisos, etc.).

### 3.3 Ús de l’Extensió del Navegador
1. Instal·la l’extensió des de [https://bitwarden.com/download/](https://bitwarden.com/download/).  
2. Inicia sessió amb el teu compte.  
3. Quan visitis una pàgina d’inici de sessió, Bitwarden detectarà les credencials automàticament.  
4. Prem la icona de Bitwarden i selecciona **“Autofill”**.

💡 *Drecera útil:*  
- **Windows:** `Ctrl + Shift + L`  
- **Mac:** `Cmd + Shift + L`

---

## 🔹 4. Gestió de Còpies de Seguretat (Backup)

### 4.1 Crear una Còpia de Seguretat
1. Ves a: *Settings → Tools → Export Vault*.  
2. Tria el format **.json** o **.csv**.  
3. Desa l’arxiu en una ubicació segura (no compartida).  
4. Si tens una organització o servidor propi, activa les còpies automàtiques des del panell d’administració.

### 4.2 Bones Pràctiques de Seguretat
- **Mai** guardis l’arxiu d’exportació en text pla a l’ordinador.  
- Desa’l en un suport segur com:
  - 🔐 **Clau USB xifrada**
  - ☁️ **Emmagatzematge al núvol amb xifratge (Tresorit, Proton Drive, OneDrive xifrat)**  
- Actualitza la còpia de seguretat **cada mes** o després de canvis importants.

---

## 🔹 5. Resum de Bones Pràctiques

| Acció | Recomanació |
|-------|--------------|
| Contrasenya mestra | Més de 12 caràcters, complexa, única |
| 2FA | Sempre activat |
| Compartició de credencials | Només mitjançant “Organizations” de Bitwarden |
| Backups | Mensuals i sempre xifrats |
| Actualització | Mantén aplicacions i extensions al dia |

---

## 🔹 6. Annex: Captures Recomanades
Afegeix captures de pantalla per fer la guia més visual:
1. Pantalla de registre i inici de sessió  
2. Generador de contrasenyes  
3. Formulari d’“Add Item”  
4. Extensió del navegador amb l’autofill  
5. Pantalla d’“Export Vault”  

---

📘 **Autoria:** Equip Tècnic  
📅 **Versió:** 1.0  
🔐 **Eina:** Bitwarden Password Manager

