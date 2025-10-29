# SERVEIS DE DIRECTORI (LDAP)
---
- **Autor:** Pol Serrano Aromí
- **Data:** 29/10/2025

---
## 1. Introducció:
En aquesta pràctica treballarem amb la instal·lació i configuració d’un servidor LDAP utilitzant Ubuntu Server 24.04 dins d’una màquina virtual a VirtualBox. Treballarem també la configuració de la xarxa, l’accés remot mitjançant SSH i la instal·lació de l’eina LDAP Account Manager (LAM) per gestionar usuaris i grups de manera gràfica. L’objectiu és aprendre a crear i administrar un directori LDAP, comprendre la seva estructura i veure com pot utilitzar-se en entorns professionals per a la gestió centralitzada d’usuaris i permisos.

---
## 2. Índex:

IMATGE 1

---
## 3. Configuració Prèvia:

Primer de tot crearem una màquina nova a VirtualBox, seguidament, seleccionem la ISO anteriorment descarregada, en el nostre cas (Ubuntu Server 24.04). Després, en el meu cas, li posarem 25GB i 4GB de RAM.

Un cop haguim instal·lat correctament el server a VirtualBox, procedim a la primera arrencada del server, també de adaptadors de xarxa hi posarem 2 adaptadors: **Xarxa Nat** i **Només amfitrió**, també podeu veure la imatge per més informació sobre el servidor.

IMATGE 2
---
## 4. Actualitzacions opcionals (recomanades):

Un cop haguem fet tot el procés d'instal·lació i estiguem dins del server introduirem la comanda: sudo apt upgrade -y & sudo apt update

IMATGE 3

El símbol ‘&&’ es representa, com si diguessim una coma, despres de executar el ‘sudo apt update’ després instalara l’altre comanda.

---
## 5. Connexió SSH:

Per fer-ho obrirem en el meu cas una terminal amb git instal·lat, i posarem la comanda: 

```bash
ssh usuari@192.168.56.101 
```

IMATGE 4

Això és en el meu cas, ja que el meu usuari, es diu usuari i aquella és la ip del meu adaptador. Un cop fet això estem connectats correctament remotament.

---
## 6. Canviar domini:

Per canviar el domini, entrarem al arxiu nano: 

```bash
sudo nano /etc/hosts
```

Allà haurem de canviar el domini, en el nostre cas, l'activitat ens demana server.innovatech21.test

IMATGE 5

Un cop finalitzat aquests pas, introduirem la comanda: ‘hostname -f’ per veure si els canvis s’han desat correctament.

IMATGE 6

---
## 7. Instal·lació OpenLDAP:

Ara passarem a la instal·lació, on amb la comanda: 

```bash
apt install slapd ldap-utils -y 
```

Gràcies aquesta comanda instal·larem el sevei LDAP, ens preguntara per introduir una **contrasenya** i el **nom del domini**.

IMATGE 7

I amb la comanda:

```bash
systemctl status ldap
```

comprovarem que el servei està funcionant correctament, com podeu veure està actiu i funcionant correctament.

IMATGE 8

---
## 8. Comprovació del directori:

Seguidament amb la comanda:

```bash
sudo slapcat
```

Amb això comprovarem que el directori s’ha creat amb el nom que volem.

IMATGE 9

En canvi, si el nom del directori no és el que volem, hauriem de reconfigurar el servei amb la comanda: 

```bash
dpkg-reconfigure slapd
```

IMATGE 10
IMATGE 11
IMATGE 12

En demana coses com: nom de l’organització, password del admin, borrar la base de dades i moure la informació del directori existent a una carpeta de backup.

---
## 9. Creació dels OU:

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

IMATGE 13

I finalment per borrar: 

```bash
ldapdelete -D “cn=admin,dc=innovatech,dc=test” -W “ou=users,dc=innovatech,dc=test
```

I veurem que s’ha eliminat correctament ja que només ens surt el predeterminat i no ens surt els dels usuaris que haviem creat anteriorment.

---
## 10. Instal·lació LDAP Account Manager:

---
## 11. Configuración prèvies LDAP Account Manager:

---
## 12. Creació de grups i usuaris

---
## 13. Conclusió
