# Gestió Flexible de discos (LVM amb Zorin OS)

**Autors d'aquesta part:** Pau Constanseu i Pol Serrano  
**Data:** 28/10/2025  
**Assignatura:** Seguretat Informàtica  

---

## 1. Introducció

En aquesta pràctica aprendrem a gestionar volums lògics (LVM) dins d’un sistema Linux mitjançant una màquina virtual configurada amb diversos discos. L’objectiu és entendre com crear i administrar volums físics, grups de volums i volums lògics, així com realitzar tasques com ampliar o reduir espai, crear snapshots i configurar mirroring per garantir la seguretat de les dades.

A través de diferents comandes del sistema, es posarà en pràctica la gestió flexible de l’emmagatzematge, millorant la capacitat d’adaptació i manteniment dels recursos dins d’un entorn Linux.

---

## 2. Índex

**1.** Introducció  
**2.** Índex  
**3.** Configuracions Prèvies  
**4.** Detecció de discos  
**5.** Inicialització de discos  
**6.** Crear Grup de Volums  
**7.** Crear volums lògics  

![imatge](/tasca_03/img/lvm_01.png)

---

## 3. Configuracions Prèvies

Primer de tot haurem de crear una màquina virtual, hi posarem 2 CPUs i 8 GB (ja que és una interfície gràfica) i afegirem 3 discs durs més de 10 GB.  
Un cop posats els requeriments de la màquina, la iniciem per procedir amb la instal·lació del sistema operatiu.

| Disc | Ús | Mida Recomanada |
|------|----|----------------|
| /dev/sda | Disc principal | 20 GB |
| /dev/sdb | Primer disc per a LVM | 10 GB |
| /dev/sdc | Per mirroring | 10 GB |
| /dev/sdd | Per snapshots o expansió | 10 GB |

![imatge](/tasca_03/img/lvm_02.png)

---

## 4. Detecció de discos:

Un cop hàgiu instal·lat tot el sistema operatiu, obrirem la terminal i introduirem la comanda:

```bash
fdisk -l
```

per comprovar que el sistema ha detectat els discos com a particions.

![imatge](/tasca_03/img/lvm_03.png)


---

## 4. Detecció de discos:

Un cop hàgiu instal·lat tot el os, obrirem la terminal i introduirem la comanda: 

```bash
fdisk -l
```

Per comprovar que el sistema ha detectat els discos com a particions.

---

## 5. Inicialització de discos:

Ara crearem els volums físics amb la comanda: 

```bash
pvcreate
```

![imatge](/tasca_03/img/lvm_04.png)

A partir de les particions de la part anterior (sdb/sdc/sdd). Recordatori: Recomano que abans de començar a posar totes les comandes, recomano posar la comanda sudo su, per realitzar totes les comandes amb root així tots els processos seran més ràpids a la hora de realizarlos.

---

## 6. Crear Grups de Volums:

Seguidament crearem el grup de volums, mitjançant la comanda: 

```bash
vgcreate volgrup
```

Posteriorment hi podem agregar o eliminar volums. En el meu cas la comanda completa serà: 

```bash
vgcreate volgrup /dev/sdb /dev/sdc /dev/sdd
```

![imatge](/tasca_03/img/lvm_05.png)

I si en algun cas volem afegir algún nou volum en el grup, només haurem d'introduir la comanda: 

```bash
vgextend volgrup nom_disc’
```

Finalment per veure característiques sobre el grup de volum creat anteriorment ho farem amb la comanda: 

```bash
vgdisplay
```

Veurem info com el nom del grup, el estat, el format, les àrees que abarca i moltes coses més que les podeu veure en la imatge.

![imatge](/tasca_03/img/lvm_06.png)

---

## 7. Crear volums lògics

Es creen a partir dels grups de volums indicant la mida, el grup de volum i el nom que se li vol donar al volum lògic, és fa amb la comanda: **‘lvcreate’**

![imatge](/tasca_03/img/lvm_07.png)

I ara amb la comanda: **‘vgdisplay’** s’observa com l’espai està siguent utilitzat. Recordo que els volums lògics són com les particions, per tant, per utilitzar-se caldrà formatar-los amb un sistema d’arxius.

![imatge](/tasca_03/img/lvm_08.png)

**1-** I ara per muntar un volum lògic parcialment, caldrà utilitzar la comanda **‘mount’** per muntar el volum cap la carpeta creada en l’anterior pas

![imatge](/tasca_03/img/lvm_09.png)

**PD:** Aquesta acció caldria fer-la cada cop al iniciar la máquina.

**2-** I si volem que el volum logic estigui muntat de forma permanent, cal editar l’arxiu:

```bash
nano /etc/fstab
```

![imatge](/tasca_03/img/lvm_10.png)

Copiarem la última línea del codi on podeu veure que he agregat una línia de codi. I si volem modificar la mida d’un lv usarem: **lvextend** (per estendre el volum) i **lvreduce** (per reduir la mida). I recordo que abans de modificar un lv sempre s’ha de desmuntar perquè no estigui en ús: 

```bash
umount /mnt/lv01
```

Si en algun cas volem ampliar el volum lògic, la mida s’indica amb el paràmetre -L:

![imatge](/tasca_03/img/lvm_11.png)

I per ampliar el sistema de fitxers per poder aprofitar la mida extra que anteriorment hem afegit, ho farem amb: 

```bash
resize2fs
```

I si en canvi de ampliar, volem reduir, ho fariem amb les següents comandes: 

```bash
umount /mnt/VolumLogic01
```

```bash
e2fsck -f /dev/volgrup/VolumLogic01
```

```bash
resize2fs /dev/volgrup/VolumLogic01 100M
```

```bash
lvreduce -L 100M /dev/volgrup/VolumLogic01
```

I si volem fer algun tipus de comprovació per veure que els canvis s’han desat correctament, podrem fer servir comandes com: **‘pvs’** / **‘vgs’** / **‘lvs’**

**PVS:** Mostra els volums físics creats indicant si estan assignats algun grup de volums.

![imatge](/tasca_03/img/lvm_12.png)

**VGS:** Serveix per veure els grups de volums existents i indicant els nombre de volums físics que el formen, els LV definits, l’espai total i l’espai sense assignar.

![imatge](/tasca_03/img/lvm_13.png)

**VGS:** Mostra els LV definits amb les seves propietats.

![imatge](/tasca_03/img/lvm_14.png)

Si en algun cas volem eliminar un volum lògic, només caldria fer dos passos:

- Desmuntar el volum lògic

- Executar comanda lvremove

Per desmuntar el volum lògic, com us he dit abans, seria amb la comanda: 

```bash
umount /mnt/VolumLogic01
```

Finalment per eliminar un cop desmontat el volum lògic: **‘lvremove /dev/volgrup/VolumLogic01’**

![imatge](/tasca_03/img/lvm_15.png)

Seguidament passarem amb les ‘snapshots’, són una còpia exacte d’un LV que conté totes les dades en el moment que es crea la instantània. És molt útil perquè permet fer les còpies de la informació sense parar els serveis:

- Es realitza la snapshot

- Es fa còpia de seguretat sense haver de parar el server.

Per posar-ho en pràctica, crearem una instantània, amb una mida i nom, a part també li indicarem que es una snapshot i que es el que farà. Comanda: 

```bash
lvcreate -L 100M -s -n copiaVolumLogic01 /dev/volgrup/VolumLogic01
```

![imatge](/tasca_03/img/lvm_16.png)

I per veure els dos lv creats i com la còpia apunta al volum original com us he indicat abans, ho realitzarem amb  la comanda: **‘lvs volgrup’**

![imatge](/tasca_03/img/lvm_17.png)

Un cop haguim vist que la còpia esta creada i ubicada correctament, muntarem la còpia per veure el contingut.

seguident, creem un grup de volums amb dos dels volums físics, amb la comanda introduïda amb passos anteriors:

```bash
vgcreate vg_mirror /dev/sdc /dev/sdd
```

En el meu cas he tingut que treure’l del grup actual, netejar la informació de el lvm del disc, reinicializarlo com a pv nou i finalment crear el nou grup amb el nom de: **vg_mirror** com diu la tasca.

![imatge](/tasca_03/img/lvm_18.png)

Seguidament crearem el sistema del mirror simple amb la comanda anteriorment feta en altres passos: 

```bash
lvcreate -L 90M -m1 -n mirrorlv vg_mirror
```

Aqui estem dien que crearem un nou vl, de 90MiB, amb el nom de: **mirrorlv**.

![imatge](/tasca_03/img/lvm_19.png)

Finalment podrem observar com el volum lògic està format pels miralls introduïts en el pas anterior i dels logs, que serveixen per mantenir la sincronització:

![imatge](/tasca_03/img/lvm_20.png)

Podem identificar gràcies a la comanda: **‘lva -a -o +devices’** el nombre de miralls que es vulguin mantenir amb el paràmetre **-m** a **lvcreate**.

---

### Gràcies per la vostra atenció!

- Podeu tornar a la [pàgina princial](/tasca_03/README.md)









