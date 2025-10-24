# Introducció tasca T04 (Serveis de directori. LDAP)

- **Autor:** Pol Serrano Aromí
- **Data:** 24/10/2025

En aquesta tasca, es treballarà en la implementació d’un **servei d’autenticació centralitzada** per a l’empresa **Innovatech**, una start-up tecnològica en ple creixement que actualment pateix problemes de gestió d’usuaris i accessos a causa d’un sistema descentralitzat. Cada servei intern utilitza la seva pròpia base de dades d’usuaris i contrasenyes, fet que genera **ineficiències operatives**, **riscos de seguretat** i una **manca d’escalabilitat** a mesura que l’empresa creix.

Per tal de solucionar aquests inconvenients, s’ha decidit implementar **OpenLDAP (Lightweight Directory Access Protocol)** com a solució d’autenticació centralitzada. Aquesta elecció es deu al fet que OpenLDAP és una eina **robusta, segura i de codi obert**, totalment compatible amb l’entorn **GNU/Linux** utilitzat per Innovatech.

L’objectiu principal de la tasca és **instal·lar i configurar un servidor OpenLDAP** que permeti gestionar usuaris i grups de forma centralitzada. També s’inclourà la **configuració d’un equip client** perquè pugui autenticar-se mitjançant aquest directori. 

El treball inclourà les següents fases:
1. **Instal·lació del servei OpenLDAP** en un servidor Linux.
2. **Configuració del domini base i la jerarquia** d’unitats organitzatives.
3. **Creació i gestió d’usuaris i grups** dins del directori.
4. **Integració d’un client Linux** per a l’autenticació centralitzada.

Aquesta implementació proporcionarà a Innovatech una gestió d’usuaris més eficient, segura i escalable, facilitant el manteniment i la integració de nous serveis dins la seva infraestructura tecnològica.

--

- Pots trobar la solució en l'arxiu [solucio.md](/tasca_04/solucio.md)

- [Torna a la pàgina principal](../)
