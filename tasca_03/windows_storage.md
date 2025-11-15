# Gestió Flexible de discos (Windows)

**Autors d'aquesta part:** Aran Perez i Pau Lopez  
**Data:** 15/11/2025  
**Assignatura:** Seguretat Informàtica  

---

## 1. Introducció

En aquesta pràctica hem treballat amb els Espais d’Emmagatzematge de Windows 11 per entendre com funcionen els sistemes de mirall i la gestió de discos virtuals. S’han creat, configurat i provat particions amb mirall doble i mirall triple, comprovant-ne el funcionament mitjançant l’addició i eliminació de discos dins la màquina virtual. L’objectiu principal és aprendre com Windows protegeix la informació duplicant-la o triplicant-la en diferents unitats per garantir la seguretat de les dades en cas de fallada d’un disc.

---

## 2. Índex:

**3.** Configuració inicial

**4.** Efecte mirall doble

**5.** Efecte mirall triple

**6.** Conclusió

---

## **3.** Configuració inicial:

![imatge](/tasca_03/img/win_01.png)
![imatge](/tasca_03/img/win_02.png)

---

## **4.** Efecte mirall doble: 

**Partició del disc:** Primer de tot entrerem a “administrar espacios de almacenamiento”:

![imatge](/tasca_03/img/win_03.png)

Un cop dins crearem un espai de disc d'emmagatzematge, (entrem a la opció marcada).

![imatge](/tasca_03/img/win_04.png)

I s´obrirà aquest panell, que al que haurem de fer serà posar les característiques que volem que tingui al nostre disc.

![imatge](/tasca_03/img/win_05.png)

Un cop haguem posat totes les característiques, acabarem de crear al disc del tot, fen clic a la part marcada. Ara ja podem veure el disc principal i veurel partit en dos particions en efecte mirall.

![imatge](/tasca_03/img/win_06.png)

**Posar informacío dins del disc i eliminar 1 disc:**

![imatge](/tasca_03/img/win_07.png)
![imatge](/tasca_03/img/win_08.png)

Ara tancarem la màquina virtual i eliminem un disc de la mateixa manera que abans haviem creat un.

![imatge](/tasca_03/img/win_09.png)

Ara podem veure que hi ha una partició que no funciona correctament, ja que hem eliminat un disc de la màquina virtual. Ara mirarem si s'ha guardat la informació en l´altre partició, per comprovar si l´efecte mirall s'ha creat correctament.

![imatge](/tasca_03/img/win_10.png)

En aquesta imatge es pot veure que se'ns ha guardat la informació correctament ✅:

![imatge](/tasca_03/img/win_11.png)

I ara podem afegir un altre cop al disc perquè no ens dongui cap error i estigui tot correcte.

![imatge](/tasca_03/img/win_12.png)

---

## **5.** Efecte mirall triple: 

Ara al primer que farem serà borrar el disc de paritat doble que hem fet per la part anterior. Un cop l´hem eliminitat hem d'afegir els discos necesaris fins a tenir 5:

![imatge](/tasca_03/img/win_13.png)

I haurem de agregar les unitats fins a tenir 5, per poder fer la partició de mirall triple.

![imatge](/tasca_03/img/win_14.png)

Ara haurem de crear un espai d´emmagatzematge amb els 5 discos com també em fet amb la part anterior, però amb reflejo triple.

![imatge](/tasca_03/img/win_15.png)

Amb amb aquesta imatge es pot comprovar que s´ha creat correctament.

![imatge](/tasca_03/img/win_16.png)

Ara posarem arxius dins, del disc i eliminem una de les unitats que hem afegit desde al VM, per veure que pasa.

![imatge](/tasca_03/img/win_17.png)
![imatge](/tasca_03/img/win_18.png)

En aquesta imatge es pot veure que ja em trencat una de les unitats partides.

I en aquí ja es veu que seguim tenint l'arxiu, la unica diferencia es que ha distribuït la informació de recuperació entre els 5 discos partits per eficiència.


![imatge](/tasca_03/img/win_19.png)

---

## **6.** Conclusió

A través d’aquesta pràctica hem pogut observar que els Espais d’Emmagatzematge de Windows 11 ofereixen un sistema robust per evitar la pèrdua de dades. Tant amb el mirall doble com amb el mirall triple, la informació es manté intacta fins i tot quan un o diversos discos fallen, demostrant l’eficàcia d’aquest tipus d’emmagatzematge redundant. També hem après a gestionar discos en una màquina virtual i a interpretar l’estat de les particions quan hi ha errors. En resum, ha estat una pràctica útil per comprendre el funcionament real de la tolerància a fallades en entorns Windows.


