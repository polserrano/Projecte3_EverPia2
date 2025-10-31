# Introducció: Espais d’Emmagatzematge

Després d’haver superat la fase formativa, ja esteu preparats per afrontar un nou repte professional com a tècnics de **EverPia Consultors**. En aquesta ocasió, el nostre client és **"Garriga i Associats"**, un prestigiós **bufet d’advocats** que gestiona una gran quantitat d’informació legal **altament sensible**.  

La direcció del bufet ha expressat la **necessitat urgent de renovar els seus sistemes de servidors** per garantir la **integritat**, la **disponibilitat** (alta redundància) i la **facilitat de gestió** del seu emmagatzematge de dades.  

Com a consultors, el vostre encàrrec consisteix a **dissenyar i documentar dues solucions d’emmagatzematge**, una per **entorns Linux** i una altra per **entorns Windows**, que compleixin els principis de **redundància, escalabilitat i alta disponibilitat**.  
Aquesta tasca actuarà com una **prova de concepte** prèvia a la presentació final de la proposta al client.

---

## Objectius del projecte

1. **Dissenyar una solució d’emmagatzematge per a sistemes Linux utilitzant LVM (Logical Volume Manager)**  
   - Utilitzar la distribució **Zorin OS** o una alternativa compatible.  
   - Crear un **grup de volums (VG)** i un **volum lògic (LV)** amb dos discs de 10 GB.  
   - Configurar el muntatge automàtic del volum a través de **/etc/fstab**.  
   - Implementar un **mirall (lvm_mirror)** per garantir l’alta disponibilitat.  
   - Crear **instantànies (snapshots)** per protegir dades i demostrar com restaurar-les.  
   - Mostrar el procés d’**escalabilitat** ampliant el volum existent amb l’espai lliure del grup de volums.

2. **Dissenyar una solució d’emmagatzematge per a sistemes Windows amb Espais d’Emmagatzematge (Storage Spaces)**  
   - Utilitzar **Windows 11** i crear un **Storage Pool** amb tres discs de 10 GB.  
   - Experimentar amb diferents configuracions de **resiliència**:  
     - Mirroring (alta disponibilitat)  
     - Parity (eficiència d’espai)  
     - Triple mirall (redundància màxima)  
   - Mostrar la gestió dels discos i l’estat del pool des de la **consola de gestió de Windows**, destacant la seva facilitat d’administració.

---

## Metodologia de Treball

El treball es realitzarà **en grup**, seguint aquestes fases:

- **Divisió d’equips:**  
  Un equip s’encarregarà de la part **Linux (LVM)** i l’altre de la part **Windows (Storage Spaces)**.

- **Treball individual previ:**  
  Cada membre prepararà el **guió de la seva part**, investigant comandes, opcions de configuració i documentació tècnica.

- **Demostració pràctica:**  
  Cada parella executarà i documentarà la seva implementació en **màquines virtuals**.

- **Integració i revisió final:**  
  El grup complet revisarà la documentació generada i assegurarà la coherència entre ambdues parts.

- **Lliurament:**  
  Cada membre pujarà la documentació al seu **repositori personal**, dins la carpeta `tasca03`.

---

## Estructura de la carpeta `tasca03`

- `README.md` → Descripció general de la tasca i enllaços als dos informes.  
- `linux_lvm.md` → Document amb la solució implementada per a **Linux (LVM)**.  
- `windows_storage.md` → Document amb la solució implementada per a **Windows (Storage Spaces)**.  
- `img/` → Carpeta amb les **captures de pantalla i imatges** de les demostracions.

---

## Resultat esperat

El projecte ha de demostrar la capacitat de l’equip per:
- Dissenyar solucions tècniques adaptades a necessitats reals.
- Documentar els procediments de manera professional i clara.
- Treballar de forma col·laborativa i coordinada.
- Preparar una **presentació final** per al client amb les **conclusions i recomanacions** del projecte.

---

## Recursos del projecte

- 📂 [Carpeta d’imatges](./img)  
- 🐧 [Solució Linux ](./linux-lvm.md)  
- 🪟 [Solució Windows](./windows_storage.md)

