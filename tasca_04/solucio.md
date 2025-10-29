# T04: Serveis de directori (LDAP)
---
- **Autor:** Pol Serrano Aromí
- **Data:** 29/10/2025

---
## 📖 1. Introducció:
En aquesta pràctica treballarem amb la instal·lació i configuració d’un servidor LDAP utilitzant Ubuntu Server 24.04 dins d’una màquina virtual a VirtualBox. Treballarem també la configuració de la xarxa, l’accés remot mitjançant SSH i la instal·lació de l’eina LDAP Account Manager (LAM) per gestionar usuaris i grups de manera gràfica. L’objectiu és aprendre a crear i administrar un directori LDAP, comprendre la seva estructura i veure com pot utilitzar-se en entorns professionals per a la gestió centralitzada d’usuaris i permisos.

---
## 📁 2. Índex:

1. [Introducció](#1-introducció)  
2. [Índex](#2-índex)  
3. [Configuració Prèvia](#3-configuració-prèvia)  
4. [Actualitzacions opcionals (recomanades)](#4-actualitzacions-opcionals-recomanades)  
5. [Connexió SSH](#5-connexió-ssh)  
6. [Canviar domini](#6-canviar-domini)  
7. [Instal·lació OpenLDAP](#7-instal·lació-openldap)  
8. [Comprovació del directori](#8-comprovació-del-directori)  
9. [Creació dels OU (Unitats Organitzatives)](#9-creació-dels-ou)  
10. [Instal·lació LDAP Account Manager (LAM)](#10-instal·lació-ldap-account-manager)  
11. [Configuracions prèvies de LDAP Account Manager](#11-configuracions-prèvies-ldap-account-manager)  
12. [Creació de grups i usuaris](#12-creació-de-grups-i-usuaris)  
13. [Conclusió](#13-conclusió)

![imatge](/tasca_04/img/IMATGE_01.png)

---
## ⚙️ 3. Configuració Prèvia:

Primer de tot crearem una màquina nova a VirtualBox, seguidament, seleccionem la ISO anteriorment descarregada, en el nostre cas (Ubuntu Server 24.04). Després, en el meu cas, li posarem 25GB i 4GB de RAM.

Un cop haguim instal·lat correctament el server a VirtualBox, procedim a la primera arrencada del server, també de adaptadors de xarxa hi posarem 2 adaptadors: **Xarxa Nat** i **Només amfitrió**, també podeu veure la imatge per més informació sobre el servidor.

![imatge](/tasca_04/img/IMATGE_02.png)
---
## 💻 4. Actualitzacions opcionals (recomanades):

Un cop haguem fet tot el procés d'instal·lació i estiguem dins del server introduirem la comanda: sudo apt upgrade -y & sudo apt update

![imatge](/tasca_04/img/IMATGE_03.png)

El símbol ‘&&’ es representa, com si diguessim una coma, despres de executar el ‘sudo apt update’ després instalara l’altre comanda.

---
## 🌐 5. Connexió SSH:

Per fer-ho obrirem en el meu cas una terminal amb git instal·lat, i posarem la comanda: 

```bash
ssh usuari@192.168.56.101 
```

![imatge](/tasca_04/img/IMATGE_04.png)

Això és en el meu cas, ja que el meu usuari, es diu usuari i aquella és la ip del meu adaptador. Un cop fet això estem connectats correctament remotament.

---
## 🛜 6. Canviar domini:

Per canviar el domini, entrarem al arxiu nano: 

```bash
sudo nano /etc/hosts
```

Allà haurem de canviar el domini, en el nostre cas, l'activitat ens demana server.innovatech21.test

![imatge](/tasca_04/img/IMATGE_05.png)

Un cop finalitzat aquests pas, introduirem la comanda: ‘hostname -f’ per veure si els canvis s’han desat correctament.

![imatge](/tasca_04/img/IMATGE_06.png)

---
## ⚡ 7. Instal·lació OpenLDAP:

Ara passarem a la instal·lació, on amb la comanda: 

```bash
apt install slapd ldap-utils -y 
```

Gràcies aquesta comanda instal·larem el sevei LDAP, ens preguntara per introduir una **contrasenya** i el **nom del domini**.

![imatge](/tasca_04/img/IMATGE_07.png)

I amb la comanda:

```bash
systemctl status ldap
```

comprovarem que el servei està funcionant correctament, com podeu veure està actiu i funcionant correctament.

![imatge](/tasca_04/img/IMATGE_08.png)

---
## 💥 8. Comprovació del directori:

Seguidament amb la comanda:

```bash
sudo slapcat
```

Amb això comprovarem que el directori s’ha creat amb el nom que volem.

![imatge](/tasca_04/img/IMATGE_09.png)

En canvi, si el nom del directori no és el que volem, hauriem de reconfigurar el servei amb la comanda: 

```bash
dpkg-reconfigure slapd
```

![imatge](/tasca_04/img/IMATGE_10.png)
![imatge](/tasca_04/img/IMATGE_11.png)
![imatge](/tasca_04/img/IMATGE_12.png)

En demana coses com: **nom de l’organització**, **password del admin**, **borrar la base de dades** i **moure la informació del directori existent a una carpeta de backup**.

---
## 👤 9. Creació dels OU:

Per fer-ho, ho farem mitjançant la comanda: 

```bash
sudo nano OU_users.ldif 
```

I introduirem els següents paràmetres en aquell nano:

```bash
dn: ou=users,dc=innovatech21,dc=test
ou: Usuaris
ObjectClass: top
ObjectClass: organizationalUnit

dn: ou=groups,dc=innovatech21,dc=test
ou: Usuaris
ObjectClass: top
ObjectClass: organizationalUnit
```

I després el moure'm amb la comanda:

```bash
ldapadd -D "cn=admin,dc=innovatech,dc=test" -W -f OU_users.ldif
```

Finalment comprovarem amb ‘sudo slapcat’ que els ou s’han creat correctament:

![imatge](/tasca_04/img/IMATGE_13.png)

I finalment per borrar: 

```bash
ldapdelete -D “cn=admin,dc=innovatech,dc=test” -W “ou=users,dc=innovatech,dc=test
```

I veurem que s’ha eliminat correctament ja que només ens surt el predeterminat i no ens surt els dels usuaris que haviem creat anteriorment.

![imatge](/tasca_04/img/IMATGE_14.png)

---
## 🔗 10. Instal·lació LDAP Account Manager:

Seguidament farem la instal·lació del LDAP account manager i ho farem mitjançant la comanda: 

```bash
sudo apt install ldap-account-manager -y
```

![imatge](/tasca_04/img/IMATGE_15.png)

Un cop instal·lat, anirem al nostra buscador, i buscarem **‘http://IP/lam’** en el meu cas serà **‘http://192.168.56.101/lam’** y un cop haguim introduit aquests enllaç estarem dins del menu de login del nostre LDAP versió gràfica.

![imatge](/tasca_04/img/IMATGE_16.png)

Un cop estiguem en el menú com el que es mostra a la imatge localitzarem un botó a la part superior dreta que posa **‘LAM configuration’**, seguidament li farem click a la segona opcio, **‘Edit server profiles’**.

![imatge](/tasca_04/img/IMATGE_17.png)

Un cop haguim fet click a la segona opció ens direccionara a un nou menú on podrem introduir la contrasenya per el nostre LDAP account manager, recordeu que la contrasenya que ve ja predeterminada és: **‘lam’**

![imatge](/tasca_04/img/IMATGE_18.png)

Un cop haguim seguit tots els passos estarem finalment en la interfície per pogue configurar el nostre LDAP.

---
## 🛠️ 11. Configuración prèvies LDAP Account Manager:

Un cop estiguem dins i a la primera pàgina **(General Settings)* haurem de configurar diferents paràmetres com els que surten subratllats a la imatge; la llista valida d'usuaris, el idioma, la zona horaria i finalment el sufix com surt a la imatge.

![imatge](/tasca_04/img/IMATGE_19.png)

Després entrarem en la segona pestaña **(Account types)*, allà haurem de canviar el LDAP sufix dels usuaris i el LDAP sufix dels grups, com surt a la imatge. Un cop fet això guardarem.

![imatge](/tasca_04/img/IMATGE_20.png)

Un cop guardat els canvis, veurem què se'ns tancarà sessió i iniciarem amb la contrasenya introduïda en passos anteriors del LDAP.

---
## 🔎 12. Creació de grups i usuaris

Seguidament com diu la pràctica haurem de crear 2 usuaris amb el nom de: **‘tech01’ i ‘manager01’** i seguidament crear també 2 grups amb el nom de: **‘tech’** i **‘manager’**. Seguidament a les següents imatges podem veure que per crear els usuaris, haurem d'anar **‘users > crear nuevo usuario’** i per crear grups: **‘groups > crear un nuevo grupo’**.

Seguidament un cop hagiu fet un click a ‘crear un nuevo grupo’ hi crearem els dos grups com indica la tasca: ‘tech i manager’

![imatge](/tasca_04/img/IMATGE_21.png)

Aquí podem veure que fem la creació del primer usuari, amb el nom de tech01 com indica la pràctica i seguidament amb l’altre usuari: manager01

![imatge](/tasca_04/img/IMATGE_22.png)
![imatge](/tasca_04/img/IMATGE_23.png)

Podem comprovar que els usuaris s’han creat correctament, si anem a la **‘llista d'usuaris’**, que apareix justament en un botó quan acabes de crear un usuari i com podeu veure els tant els usuaris, com el nom dels usuaris estan creats correctament

![imatge](/tasca_04/img/IMATGE_24.png)

Finalment, l'últim pas serà agregar els usuaris als grups creats anteriorment

![imatge](/tasca_04/img/IMATGE_25.png)
![imatge](/tasca_04/img/IMATGE_26.png)

---
## ♣️ 13. Conclusió

En conclusió, amb aquesta tasca hem après a instal·lar i configurar un servidor Ubuntu Server 24.04 amb OpenLDAP i LDAP Account Manager dins d’una màquina virtual a VirtualBox. Hem configurat la xarxa, accedit per SSH, creat el domini i les unitats organitzatives, i finalment gestionat usuaris i grups des de la interfície gràfica del LAM. Aquest procés ens permet entendre millor la gestió centralitzada d’usuaris i grups en un entorn professional.

---
# Gràcies per la vostra atenció!

