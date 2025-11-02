# **Fonaments del Servei DNS**

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

---

## **3. Fase teòrica**

### **3.1 Estructura del DNS**

El DNS té una estructura jeràrquica en arbre, dividida en nivells:

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
- En xarxes petites, es poden resoldre noms localment mitjançant `/etc/hosts` o protocols com **mDNS (multicast DNS)**.  
- Permet trobar dispositius locals amb noms com `nom.local` sense servidor DNS extern.

---

## **Fase pràctica**

Per a la fase pràctica, cal crear una màquina virtual amb **Zorin OS**, amb dues interfícies de xarxa:
- **NAT**
- **Pont (Bridge)**  
Amb la IP correctament configurada segons les indicacions dels responsables.

---

### **4.1 Comanda 1 — Consulta bàsica de Registre A**

Comanda:
```bash
dig xtec.cat A
```

**Resultats:**

- **IP de resposta:** `83.247.151.214`  
- **TTL:** `1721` segons  
- **Servidor DNS utilitzat:** `127.0.0.53`

---

### **4.2 Comanda 2 — Consulta de servidors de Noms**

Comanda:
```bash
dig tecnocampus.cat NS
```

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

**Resultat:**
```
135.2.83.147.in-addr.arpa. 3600 IN PTR upc.cat.
135.2.83.147.in-addr.arpa. 3600 IN PTR upc.edu.
135.2.83.147.in-addr.arpa. 3600 IN PTR wdelvio.producclo.upc.edu.
```

**Interpretació:**
- **Tipus de registre:** PTR  
- **IP consultada:** `147.83.2.135`  
- **Noms associats:** `upc.cat`, `upc.edu`, `upc.es`, `upc.eu`  
- Pertany a la infraestructura de la **UPC** i pot ser compartida per diversos serveis.

---

### **4.5 Comprovació de resolució amb nslookup**

Comanda inicial:
```bash
nslookup
```

Entrant en mode interactiu (`>`), podem executar:
```bash
set type=A
tecnocampus.cat
```

La resposta és **no autoritativa**, ja que no prové directament del servidor autoritatiu sinó d’un servidor amb informació en *cache*.

Per fer una consulta **autoritativa**, canviem:
```bash
set type=NS
```
Després consultem un dels servidors autoritatius obtinguts (ex. `ns-130.awsdns-16.com`) amb una consulta del tipus `A`.

---

### **4.6 Diferències entre les diferents consultes**

| **Consulta** | **Servidor Utilitzat** | **Tipus de Resposta** | **Observació** |
|---------------|-------------------------|------------------------|----------------|
| **No autoritativa** | DNS públic | No autoritativa | Obté la info de la memòria cau o d’altres DNS |
| **Autoritativa** | ns-130.awsdns-16.com | Autoritativa | Resposta directa del DNS responsable del domini |

---

### **4.7 Resolucions Locals**

Per comprovar la resolució local:
```bash
nslookup localhost
```

Si obtenim una IP com `127.0.0.1` o `192.168.x.x`, la resolució local funciona.

Per afegir una entrada local:
```bash
sudo nano /etc/hosts
```

Afegir una línia amb una IP i nom local, per exemple:
```
192.168.1.50 servidorlocal
```

Comprovació:
```bash
nslookup servidorlocal
```

Si el nom i la IP corresponen, la resolució local s’ha configurat correctament.
