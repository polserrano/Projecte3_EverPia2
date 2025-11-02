# **Fonaments del Servei DNS**
**- Autor:** Pol Serrano Aromí

**- Data:** 23/10/2025

## **1. Introducció a la tasca**

Com a membres de l’equip tècnic d’EverPia, hem rebut l’encàrrec de realitzar una auditoria del servei DNS per al nostre client **DigiCore**, una empresa de màrqueting digital que pateix problemes ocasionals de connectivitat.  
L’objectiu és identificar possibles errors en la resolució de noms i oferir eines de diagnosi eficients.

---

## **2. Índex**

1. Introducció a la tasca
2. Índex
3. Fase teòrica
   - 3.1 Estructura del DNS  
   - 3.2 Procés de resolució  
   - 3.3 Tipus de zones  
   - 3.4 Tipus de registres clau  
   - 3.5 Conceptes essencials  
4. Fase pràctica
   - 4.1 Consulta bàsica de registre A  
   - 4.2 Consulta de servidors de noms  
   - 4.3 Consulta detallada SOA  
   - 4.4 Consulta de resolució inversa  
   - 4.5 Comprovació amb nslookup  
   - 4.6 Diferències entre consultes  
   - 4.7 Resolucions locals
5. Conclusió Final:  

---

## **3. Fase teòrica**

### **3.1 Estructura del DNS**

El DNS té una estructura jeràrquica en arbre, dividida en nivells:

![imatge1](/tasca_06/img/img_01.png)

- **Root (arrel):** representada per un punt (.) final (sovint ocult).  
- **TLD (Top Level Domain):** dominis com `.com`, `.org`, `.net`, `.cat`, `.es`, etc.  
- **Segon nivell:** el nom registrat (ex: `tecnocampus.cat`, `xtec.cat`).  
- **Subdominis:** parts internes (ex: `mail.tecnocampus.cat`, `www.xtec.cat`).

---

### **3.2 Procés de resolució**

Quan un client vol accedir a `www.tecnocampus.cat`, el procés pot ser **iteratiu** o **recursiu**:

#### **Consulta iterativa**
1. El client demana al DNS local: “Quina IP té www.tecnocampus.cat?”  
2. El DNS local pregunta als *Root Servers* quins servidors gestionen `.cat`.  
3. Els servidors `.cat` responen quins són els autoritatius per a `tecnocampus.cat`.  
4. El DNS local pregunta a aquests servidors i finalment obté la IP.  

Cada pas és una “iteració”: el client o DNS continua preguntant fins tenir la resposta.

#### **Consulta recursiva**
El servidor DNS recursiu fa tot el procés anterior per tu i et retorna només la resposta final.

---

### **3.3 Tipus de zones**

Una **zona** és la part de la base de dades DNS que gestiona un servidor autoritatiu.

| Tipus de Zona | Funció | Exemple |
|----------------|---------|----------|
| **Zona directa** | Resol noms → IPs | `www.tecnocampus.cat → 84.88.56.11` |
| **Zona inversa** | Resol IPs → noms | `84.88.56.11 → www.tecnocampus.cat` |
| **Zona primària** | Còpia “mestre” editable | - |
| **Zona secundària** | Còpia de només lectura sincronitzada | - |

---

### **3.4 Tipus de registres clau**

| **Tipus** | **Funció** | **Exemple** |
|------------|-------------|-------------|
| **A** | Associa un nom amb una IPv4 | `www → 84.88.56.11` |
| **AAAA** | Associa amb una adreça IPv6 | `www → 2001:db8::1` |
| **CNAME** | Alias d’un altre nom | `blog → www.tecnocampus.cat` |
| **MX** | Servidor de correu | `tecnocampus.cat → mail.tecnocampus.cat` |
| **NS** | Servidors de noms del domini | `ns1.tecnocampus.cat` |
| **SRV** | Servei específic | `_ldap._tcp.example.com` |

---

### **3.5 Conceptes essencials**

#### **Resposta autoritativa**
- Prové directament del servidor que gestiona la zona.  
- Si ve d’un servidor recursiu o *cache*, és **no autoritativa**.  
- En `dig`, s’identifica amb **aa** o **AUTHORITY SECTION**.

#### **Time To Live (TTL)**
- Indica quant temps pot guardar-se la resposta en memòria cau.  
- Exemple: `TTL=3600` → es pot reutilitzar durant 1 hora.  
- **TTL massa baix:** més trànsit DNS.  
- **TTL massa alt:** canvis triguen més a propagar-se.

#### **Start of Authority (SOA)**
Defineix la configuració de la zona. Conté:
- Servidor principal (*mname*)  
- Correu de l’administrador (*rname*)  
- Número de sèrie (*serial*)  
- Valors de sincronització (*refresh*, *retry*, *expire*, *minimum TTL*)

#### **Reenviadors (Forwarders)**
Els servidors als quals un DNS envia les consultes que no pot resoldre.

- **Incondicionals:** totes les consultes es reenvien a un servidor concret.  
- **Condicionals:** només per a determinats dominis.

#### **Resolució local i mDNS**
- En xarxes petites sense DNS central, es pot resoldre noms localment.
- Mitjançant fitxers com /etc/hosts o protocols com mDNS (multicast DNS).
- mDNS permet que equips locals (com impressores o IoT) es trobin entre si amb noms com nom.local sense cap servidor DNS extern.


---

## **Fase pràctica**

Per fer la fase pràctica, com ens diu la tasca, haurem de crear un màquina virtual amb un entorn de zorin, hi haurem de posar dues interfícies de xarxa: NAT i pont amb la IP correctament configurada segons indicacions dels vostres responsables.

![imatge2](/tasca_06/img/img_02.png)
---

### **4.1 Comanda 1 — Consulta bàsica de Registre A**

La comanda que introduirem serà: **‘dig xtec.cat A’**

Comanda:
```bash
dig xtec.cat A
```
![imatge3](/tasca_06/img/img_03.png)

**Resultats:**

**1. IP de resposta (registre A):**

- A la secció ANSWER SECTION, veiem:
- xtec.cat.  1721  IN  A  83.247.151.214
- IP de resposta: **83.247.151.214**

**2. Valor TTL (Time To Live):**

- El número abans de IN és el TTL:
- xtec.cat.  1721  IN  A  83.247.151.214
- TTL: 1721 segons

**3. Servidor que ha respost a la consulta:**

- A la part inferior, apareix:
- ;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
- Servidor DNS utilitzat: **127.0.0.53**

---

### **4.2 Comanda 2 — Consulta de servidors de Noms**

Comanda:
```bash
dig tecnocampus.cat NS
```
![imatge4](/tasca_06/img/img_04.png)

**Servidors de noms autoritatius:**
- `ns-1689.awsdns-19.co.uk`
- `ns-535.awsdns-02.net`
- `ns-1071.awsdns-05.org`
- `ns-130.awsdns-16.com`

**TTL:** `172800` segons  
**Servidor DNS utilitzat:** `127.0.0.53`

---

### **4.3 Comanda 3 — Consulta detallada SOA**

Comanda:
```bash
dig escolapia.cat SOA
```
![imatge5](/tasca_06/img/img_05.png)

**Informació obtinguda:**
- **Servidor primari:** `dns1.nominalia.com`  
- **Correu administrador:** `root@dns1.nominalia.com`  
- **Número de sèrie:** `1761028956`  
- **Refresh:** `86400`  
- **Retry:** `7200`  
- **Expire:** `2592000`  
- **Minimum TTL:** `300`

---

### **4.4 Comanda 4 — Consulta resolució inversa**

Comanda:
```bash
dig -x 147.83.2.135
```
![imatge6](/tasca_06/img/img_06.png)

**Resultat:**

La comanda retorna diverses línies dins la secció ANSWER SECTION, com ara:

- `135.2.83.147.in-addr.arpa. 3600 IN PTR upc.cat.`
- `135.2.83.147.in-addr.arpa. 3600 IN PTR upc.edu.`
- `135.2.83.147.in-addr.arpa. 3600 IN PTR wdelvio.producclo.upc.edu.`

**Interpretació:**

PTR: és el tipus de registre DNS utilitzat per les consultes inverses. Associa una adreça IP amb un o més noms de domini.


En aquest cas, l’adreça IP **147.83.2.135** té múltiples registres PTR, tots relacionats amb dominis de la Universitat Politècnica de Catalunya (UPC).


Resumidament la informació obtinguda és:

**- Tipus de registre:** PTR (Pointer Record)
**- IP consultada:** 147.83.2.135
**- Noms de domini associats:** upc.cat, upc.edu, upc.es, upc.eu
**- Indica que aquesta IP pertany a la infraestructura de la UPC i pot ser compartida per diferents serveis o subdominis.**


---

### **4.5 Comprovació de resolució amb nslookup**

Ara farem diferentes consultes DNS amb la comanda: ‘nslookup’, entendre la diferència entre respostes autoritatives i no autoritatives, i comprovar la resolució local. El primer pas serà obrir la terminal i escriure la comanda: ‘nslookup’

![imatge7](/tasca_06/img/img_07.png)

Un cop introduïda ens sortirà un icone com aquests: ‘>’, això vol dir que hi podem executar les comandes dins del mode interactiu.

En aquests cas, com demana la pràctica, hem fet una consulta no autoritativa, ja que hem escrit ‘set type=A’ per fer consultes del registre tipus A, és a dir, adreces IPv4, després hem fet la consulta al domini: ‘tecnocampus.cat’, i la sortida ha sigut la següent: 

```bash
set type=A
tecnocampus.cat
```

![imatge8](/tasca_06/img/img_08.png)

La resposta és no autoritativa perquè el servidor DNS que t’ha respost no és el servidor de noms original (autoritat) per al domini tecnocampus.cat.

El servidor simplement ha consultat o emmagatzemat en memòria cache la informació des d’un altre servidor autoritatiu. I ara el següent pas serà fer-ho, però amb consulta autoritativa, bàsicament haurem de canviar el tipus de: ‘A –> NS’. Això et mostrarà quins són els servidors de noms del domini.

```bash
set type=NS
```
![imatge9](/tasca_06/img/img_09.png)

Seguidament, ara que ja sabem quins són els servidor autoritatius, seguirem al seguent pas de la pràctica, farem una consulta amb els primers servidor autoratius, que en la meva consulta m’han sortit: ‘ns-130.awsdns-16.com’ i la consulta la farem del tipus ‘A’.

![imatge10](/tasca_06/img/img_10.png)

Llavors com us he dit, això farà que el ‘nslookup’ pregunti directament al servidor autoritatiu. Seguidament aquestes són les diferències trobes entre les consultes:

---

### **4.6 Diferències entre les diferents consultes**

| **Consulta** | **Servidor Utilitzat** | **Tipus de Resposta** | **Observació** |
|---------------|-------------------------|------------------------|----------------|
| **No autoritativa** | DNS públic | No autoritativa | Obté la info de la memòria cau o d’altres DNS |
| **Autoritativa** | ns-130.awsdns-16.com | Autoritativa | Resposta directa del DNS responsable del domini |

---

### **4.7 Resolucions Locals**

Finalment en l’últim pas, s’haura de comprovar si hi ha resolució local existen, per fer-ho, el primer pas serà escriure: ‘nslookup localhost’

```bash
nslookup localhost
```
![imatge11](/tasca_06/img/img_11.png)

Si ibtenim una resposta d’un IP del tipus: ‘172.0.0.1’ o ‘192.168.x.x’, significa que la resolució local funciona, com és en el meu cas, com es mostra a la imatge. Seguidament un cop comprovat la resolució local, crearem una entrada local, pero fer-ho haurem de entrar com a root i editar el fitxer: ‘/etc/hosts’. Seguidament afegirem una línia, la tercera en l’imatge, on pot ser la IP d’un altre equip de la nostra xarxa o qualsevol IP de prova que tinguem.

```bash
sudo nano /etc/hosts
```

![imatge12](/tasca_06/img/img_12.png)

Finalment podem fer la comprovació amb la comanda ‘nslookup servidorlocal’ i veurem que el nom i la ip s’ha canviat correctament.

Comprovació:
```bash
nslookup servidorlocal
```
![imatge13](/tasca_06/img/img_13.png)

---
## 5. Conclusió Final:

El servei DNS és un component fonamental en el funcionament d’Internet, ja que permet traduir noms de domini fàcilment recordables en adreces IP utilitzables per les màquines.

També s’ha posat de manifest la rellevància dels valors TTL i dels reenviadors per optimitzar la resolució de noms i reduir el trànsit innecessari dins la xarxa. A més, la configuració local i l’ús de protocols com mDNS permeten assegurar la resolució en entorns petits o sense connexió directa a Internet.

En definitiva, dominar les eines i conceptes associats al DNS és essencial per a qualsevol professional de xarxes o administració de sistemes, ja que garanteix una infraestructura més fiable, segura i eficient.

---
# Gràcies per la vostra atenció!
