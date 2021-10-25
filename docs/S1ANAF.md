---
layout: default
title: S1 ANAF Instalare RO
nav_order: 15

---



![S1ANAF](\assets\images\s1anaf_1.jpg)

#### Sumar

S1 ANAF este o aplicație externă dezvoltată pentru calculul si depunerea declaratiilor fiscale din România. Acesta aplicatie rulează extern față de Soft1 ERP, dar necesită o conexiune activă la o bază de date Soft1 ERP. Contabilii pot utiliza aplicația pentru a trimite următoarele declarații pentru companiile lor: D300, D390 și D394 (care apare în Ver 2.0 a aplicatiei).

Va rugam sa urmatii pașii prevăzuți în acest document pentru a instala S1 ANAF atât pentru instalarile cloud, cât și pentru cele on premise.

Atentie!!!!Puteți utiliza aplicația S1ANAF pentru versiunile Soft1 ERP 5.00.521.11427 sau mai recente.

#### **Pas 1 - Import fișiere necesare în baza de date Soft1**

Pentru a utiliza aplicația S1Anaf, trebuie să importați fișierul S1_RO_STATEMENTS.cst (S.D.K. / Customization Tools / Custom Administration / Import) pentru fiecare dintre conexiunile dumneavoastra. După import, în baza de date, veți găsi tabela CCCS1ROSTM care va conține informațiile legate de declarațiile de TVA. Deoarece aplicația utilizează tabela specificată, este important să efectuați acest pas înainte de a lansa aplicația pentru prima dată.

NOTĂ: dacă aveți mai multe baze de date S1 în aceeași instalare, trebuie să importați fișierul S1_RO_STATEMENTS.cst în fiecare bază de date separat

#### **Pas 2 – Download folder aplicație S1 Anaf**

Aplicația este livrată sub forma unui folder care conține fișierele necesare pentru a rula. Folderul trebuie copiat pe statia dumneavostra de lucru, nu contează locația.

Puteți descărca cea mai recentă versiune a S1ANAF folosind următorul link:

[]: http://s1international.blob.core.windows.net/romania/S1ANAF/S1ANAFCurrentVersion/S1ANAF.zip	"Download aici"

#### **Pas 3 – Creare fișier s1anaf.xco** 

Înainte de a lansa S1ANAF pentru prima dată, este necesar să creați (dacă nu există) un fișier s1anaf.xco care ar trebui să fie situat în folderul S1Anaf (acesta poate fi creat și modificat folosind notepad.exe sau orice alt editor de text). Adăugați calea către folderul în care se află aplicația Softone (dacă sunt utilizate atât local cât și Cloud și veti specifica ambele căi daca aveti ambele tipuri de instalari). Structura fișierului este următoarea:

- **[S1ANAFCONFIG]** secțiune obligatorie;
- **path-softone-onpremise:** cale Softone On-premise, rubrica se va specifica DOAR dacă folosiți conexiunea On-Premise;
- **path-softone-azure:** cale Softone Cloud, rubrica se va specifica DOAR dacă folosiți conexiunea Cloud;
- **path-xcos:** calea către folderul unde se găsesc fișierele xco, de regulă folderul de instalare Soft1 sau in C/Program Data/ Softone / Data;
- **admin**: true/false: specifică modul în care rulează aplicația. Dacă se specifică
   **admin = true**, în timpul execuției aplicației, se vor afișa diverse opțiuni suplimentare (configurare SQL queries, afișare rezultate SQL query);

```
**** CHANGE THE PATHS ACCORDINGLY****

[S1ANAFCONFIG]
path-softone-onpremise = C:\SoftOne\Soft1
path-softone-azure = C:\SoftOne\Soft1 Azure
path-xcos = C:\SoftOne\Soft1
admin = true
```

Exemplu:

![Imagine2](C:\Users\stefan.furtuna\Documents\GitHub\WIKI\assets\images\S1anaf_2.jpg)

#### **Pas 4 – Lansare S1ANAF**

După ce fișierul s1anaf.xco a fost creat, aplicația S1Anaf.exe poate fi lansată.

La prima lansare, utilizatorul trebuie să aleagă modul de conectare: On-premise / Cloud:

![Imagine3](C:\Users\stefan.furtuna\Documents\GitHub\WIKI\assets\images\S1anaf_3.jpg)

##### 4.1 Logare On-premise

Pentru instalarea On-Premise urmați pașii de mai jos:

![image-20211025115438680](C:\Users\stefan.furtuna\Documents\GitHub\WIKI\assets\images\S1anaf_4.jpg)

Atunci când utilizatorul selectează logarea On-premise, aplicația citește calea către fișierele xco specificată în s1anaf.xco. 

![Imagine3](C:\Users\stefan.furtuna\Documents\GitHub\WIKI\assets\images\S1Anaf_5.jpg)

Conexiunile definite sunt afișate în rubrica Connection. După ce utilizatorul selectează o conexiune, utilizatorul trebuie să introducă numele de utilizator și parola (așa cum sunt definite în aplicația Softone) și apoi clic pe butonul Login. Este foarte important ca fișierul xco asociat conexiunii să conțină secțiunea cu datele pentru logare, deci codul de companie și cel al filialei trebuie să fie specificate, de exemplu:

```
[LOGIN]
USERNAME=Admin
PASSWORD=
COMPANY=1000
BRANCH=1000
```



##### **4.2 Logare Cloud**

Pentru logarea Cloud se introduc numele de utilizator, parola, codul companiei și al filialei.

Se editează fișierul PARAMS.CFG din folderul SoftOne astfel încât să înceapă cu secțiunea PARAMS, iar secțiunea trebuie să conțină rubrica SAAS, astfel: 

```
[PARAMS]
SAAS:saas.azure.oncloud.gr
```

Pas 1. Se adaugă secțiunea:

```
[LOGIN]
USERNAME=YourUser
PASSWORD=
COMPANY= Yourcompany
BRANCH=YourBranch
```

Exemplu:

![Imagine8](C:\Users\stefan.furtuna\Documents\GitHub\WIKI\assets\images\S1anaf_6.jpg)

Pas 2. Dacă aveți mai multe conexiuni Azure veți observa următoarea structură:

![image-20211025131540931](C:\Users\stefan.furtuna\Documents\GitHub\WIKI\assets\images\S1ANAF_7.jpg)

Copiați conținutul unei conexiuni și înlocuiți identificatorul conexiunii cu [SAASSYTEM], așa cum se vede în exemplul de mai jos:

![image-20211025132050235](C:\Users\stefan.furtuna\Documents\GitHub\WIKI\assets\images\S1anaf_8.jpg)

```
NOTĂ
Pentru ambele moduri de logare, după prima logare reușită, parametri de logare vor fi salvați în fișierul s1anaf.xco file, cu excepția parolei.
```

Exemplu fisier s1anaf.xco:

*![image-20211025132050235](C:\Users\stefan.furtuna\Documents\GitHub\WIKI\assets\images\S1anaf_9.jpg)*

​                                                                              **Setări**

După ce au fost parcurse toate etapele anterioare și aplicația poate fi lansată, pentru a putea efectua primele teste, trebuie selectate căile către fișierele necesare (java.exe, DUKIntegrator.bat, D300.xsd, D390.xsd, D394.xsd, folder destinatie pentru fișierele xml generate). Pentru a putea selecta/introduce căile se utilizează dialogul setări. 

![image-20211025132050235](C:\Users\stefan.furtuna\Documents\GitHub\WIKI\assets\images\S1anaf_10.jpg)

După ce căile au fost selectate aplicația trebuie repornită.

Această operație trebuie reluată după fiecare update al aplicației, dacă se copiază o nouă versiune a aplicației, căile trebuie reintroduse/reselectate.

Pentru descărcare DUKIntegrator puteți folosi următorul link: 

[]: https://static.anaf.ro/static/DUKIntegrator/DUKIntegrator.htm	"Download aici"

\-     după descărcare, este important să consultați documentația de instalare și configurare a DUKIntegrator.

   























| Document  Information |                             |                     |            |
| --------------------- | --------------------------- | ------------------- | ---------- |
| Title:                | S1 Anaf Installation Manual |                     |            |
|                       |                             |                     |            |
| Release Date:         | 10/07/2021                  | Last Revision Date: | 10/07/2021 |
| Doc. Code:            | S1 Anaf Installation Manual | Revision  Number:   | 1.0        |
| Classification:       | Public                      |                     |            |
| Distrbution List      | Everyone                    |                     |            |

| Version History | Comments         |
| --------------- | ---------------- |
| 1.0             | Initial  Version |