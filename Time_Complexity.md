# Ajakeerukus

Ajakeerukus (ingl. _time complexity_) kirjeldab, kuidas algoritmi täitmisaeg kasvab sõltuvalt sisendi suurusest. See on üks põhilisi meetodeid algoritmide efektiivsuse hindamiseks ja võrdlemiseks.

## Sisukord
- [Ajakeerukuse Põhialused](#ajakeerukuse-põhialused)
- [Asümptootiline Notatsioon](#asümptootiline-notatsioon)
- [Ajakeerukuse Määramine](#ajakeerukuse-määramine)
- [Levinud Ajakeerukused](#levinud-ajakeerukused)
- [Erijuhtude Analüüs](#erijuhtude-analüüs)
- [Algoritmide Optimeerimine](#algoritmide-optimeerimine)
- [Ruumi- ja Ajakasutuse Kompromissid](#ruumi--ja-ajakasutuse-kompromissid)
- [Praktilised Näited](#praktilised-näited)

## Ajakeerukuse Põhialused

Ajakeerukus on viis mõõta, kui kiiresti algoritm töötab, sõltuvalt sisendi suurusest. Eesmärk on mõista, kuidas algoritmi jõudlus skaleerub suurte sisendmahtude korral, sõltumata konkreetse arvuti kiirusest või teistest keskkonnafaktoritest.

Erinevalt reaalse täitmisaja mõõtmisest (mis sõltub riistvarast, keelest ja implementatsiooni üksikasjadest), pakub ajakeerukus abstraktsemat, kuid universaalsemat mõõtu.

### Miks Ajakeerukus On Oluline?

- **Skaleerimine**: Väikeste sisendite puhul võivad erinevused olla märkamatud, kuid suurte andmemahtude puhul võib ebaefektiivne algoritm muutuda praktiliselt kasutuskõlbmatuks.
- **Ressursside Planeerimine**: Teades algoritmi ajakeerukust, saad kavandada, kui palju aega ja arvutusjõudu on probleemi lahendamiseks vaja.
- **Algoritmide Valimine**: Erinevate lahenduste võrdlemisel aitab ajakeerukus valida kõige sobilikuma algoritmi konkreetse probleemi jaoks.
- **Kitsaskohtade Tuvastamine**: Keerukate süsteemide puhul aitab see tuvastada pudelikaelu ja optimeerimise võimalusi.

## Asümptootiline Notatsioon

Ajakeerukuse kirjeldamiseks kasutatakse kolme põhilist asümptootilist notatsiooni:

### O-notatsioon (Big O)

O-notatsioon (ingl. _Big O notation_) määratleb algoritmi täitmisaja ülemise piiri (halvima juhu stsenaarium). See on kõige enam kasutatav notatsioon ajakeerukuse kirjeldamiseks.

Näiteks, kui algoritmi ajakeerukus on O(n²), tähendab see, et halvimal juhul kasvab täitmisaeg proportsionaalselt sisendi suuruse ruuduga.

```java
// O(n) - lineaarne ajakeerukus
void näideLineaarne(int n) {
    for (int i = 0; i < n; i++) {
        System.out.println(i);
    }
}

// O(n²) - ruutkeerukus
void näideRuut(int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            System.out.println(i + ", " + j);
        }
    }
}
```

### Θ-notatsioon (Theta)

Θ-notatsioon (ingl. _Big Theta notation_) määratleb nii algoritmi täitmisaja ülemise kui ka alumise piiri. See annab täpse ajakeerukuse, kui halvim ja parim juht on asümptootiliselt samad.

Näiteks, kui algoritmi ajakeerukus on Θ(n²), tähendab see, et algoritmi täitmisaeg on proportsionaalne sisendi suuruse ruuduga nii parimal kui ka halvimal juhul.

```java
// Θ(n²) - ruutkeerukus, kus täitmisaja ülemine ja alumine piir on samad
void näideTheta(int n) {
    // Kasvab täpselt proportsionaalselt n²-ga sõltumata sisendist
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            System.out.println(i + ", " + j);
        }
    }
}
```

### Ω-notatsioon (Omega)

Ω-notatsioon (ingl. _Big Omega notation_) määratleb algoritmi täitmisaja alumise piiri (parima juhu stsenaarium).

Näiteks, kui algoritmi ajakeerukus on Ω(n), tähendab see, et algoritm vajab vähemalt sisendi suurusega proportsionaalset aega.

```java
// Ω(n) - lineaarne alumine piir
void näideOmega(int[] massiiv, int otsitav) {
    // Parimal juhul leiame otsitava kohe esimese elemendina (Ω(1))
    // Kuid üldiselt on alumine piir Ω(n)
    for (int element : massiiv) {
        if (element == otsitav) {
            System.out.println("Leitud!");
            return;
        }
    }
    System.out.println("Ei leitud");
}
```

Selles kursuses keskendume peamiselt O-notatsioonile, kuna see annab hea ülevaate algoritmi jõudlusest halvimal juhul.

## Ajakeerukuse Määramine

### Elementaarsete Operatsioonide Loendamine

Elementaarne operatsioon (ingl. _elementary operation_) on põhiline arvutussamm, mille täitmisaeg on piiratud konstandiga. Näiteks:
- Muutuja omistamine
- Aritmeetilised operatsioonid
- Võrdlusoperatsioonid
- Massiivi elemendile ligipääs
- Funktsioonikutse (välja arvatud funktsiooni enda täitmisaeg)

Ajakeerukuse määramiseks:
1. Loendame elementaarsete operatsioonide arvu kui funktsioon sisendi suurusest
2. Väljendame seda loendust võimalikult lihtsas vormis
3. Rakendame sobivat asümptootilist notatsiooni

### Tsüklite Analüüs

Tsüklite ja pesastatud tsüklite korral analüüsime alustades kõige seesmisemast tsüklist välja liikudes:

```java
// O(n) ajakeerukus
for (int i = 0; i < n; i++) {
    // konstantse aja operatsioon
    System.out.println(i);
}
```

```java
// O(n²) ajakeerukus
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        // konstantse aja operatsioon
        System.out.println(i + ", " + j);
    }
}
```

```java
// O(n²) ajakeerukus - märka, et sisemine tsükkel sõltub välimise tsükli muutujast
for (int i = 0; i < n; i++) {
    for (int j = 0; j < i; j++) {
        // konstantse aja operatsioon
        System.out.println(i + ", " + j);
    }
}
// Täpsem analüüs: 0 + 1 + 2 + ... + (n-1) = n(n-1)/2 = O(n²)
```

### Rekursiivsete Funktsioonide Analüüs

Rekursiivsete funktsioonide puhul:
1. Tuvastame baasjuhu(d)
2. Määrame rekursiivsete väljakutsete arvu
3. Arvutame töö, mida tehakse igas väljakutses
4. Kombineerime, kasutades sobivat rekurrentsiseos

Näide: Fibonacci jada arvutamine
```java
int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n-1) + fibonacci(n-2);
}
```

Rekurrentsiseos: T(n) = T(n-1) + T(n-2) + O(1)
Lahendus: T(n) = O(2ⁿ)

## Levinud Ajakeerukused

Järjestuses kõige efektiivsemast kõige vähem efektiivseni:

### 1. O(1) - Konstantne aeg
- Massiivile ligipääs, lihtsad arvutused
- Täitmisaeg ei sõltu sisendi suurusest
- Näited: Massiivi elemendi lugemine indeksi järgi, lihtne aritmeetika

```java
int esimeneelement(int[] massiiv) {
    return massiiv[0]; // Konstantse ajaga operatsioon
}
```

### 2. O(log n) - Logaritmiline aeg
- Binaarotsing, kahendpuu operatsioonid
- Sisendi suuruse väheneb igal sammul teguri võrra
- Näited: Binaarotsing, tasakaalustatud puude operatsioonid

```java
// Binaarotsing
int binaarotsing(int[] massiiv, int otsitav) {
    int algus = 0;
    int lõpp = massiiv.length - 1;
    
    while (algus <= lõpp) {
        int keskmine = algus + (lõpp - algus) / 2;
        
        if (massiiv[keskmine] == otsitav) {
            return keskmine;
        }
        
        if (massiiv[keskmine] < otsitav) {
            algus = keskmine + 1;
        } else {
            lõpp = keskmine - 1;
        }
    }
    
    return -1; // Ei leitud
}
```

### 3. O(n) - Lineaarne aeg
- Lihtsad tsüklid, lineaarotsing
- Täitmisaeg kasvab proportsionaalselt sisendi suurusega
- Näited: Massiivi läbimine, lineaarotsing

```java
// Lineaarotsing
int lineaarotsing(int[] massiiv, int otsitav) {
    for (int i = 0; i < massiiv.length; i++) {
        if (massiiv[i] == otsitav) {
            return i;
        }
    }
    return -1; // Ei leitud
}
```

### 4. O(n log n) - Linearitmiline aeg
- Efektiivsed sorteerimisalgoritmid
- Lineaarse ja logaritmilise käitumise kombinatsioon
- Näited: Merge sort, heap sort, quick sort (keskmiselt)

```java
// Merge Sort
void mergeSort(int[] massiiv, int algus, int lõpp) {
    if (algus < lõpp) {
        int keskmine = (algus + lõpp) / 2;
        
        mergeSort(massiiv, algus, keskmine);
        mergeSort(massiiv, keskmine + 1, lõpp);
        
        merge(massiiv, algus, keskmine, lõpp);
    }
}
```

### 5. O(n²) - Ruutaeg
- Pesastatud tsüklid, lihtsad sorteerimisalgoritmid
- Täitmisaeg kasvab proportsionaalselt sisendi suuruse ruuduga
- Näited: Bubble sort, insertion sort, selection sort

```java
// Bubble Sort
void bubbleSort(int[] massiiv) {
    int n = massiiv.length;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (massiiv[j] > massiiv[j + 1]) {
                // Vaheta elemendid
                int temp = massiiv[j];
                massiiv[j] = massiiv[j + 1];
                massiiv[j + 1] = temp;
            }
        }
    }
}
```

### 6. O(2ⁿ) - Eksponentsiaalne aeg
- Rekursiivsed algoritmid ilma memoiseerimiseta
- Täitmisaeg kahekordistub iga täiendava elemendiga
- Näited: Fibonacci arvutamine ilma memoiseerimiseta, kõigi alamhulkade genereerimine

```java
// Fibonacci ilma memoiseerimiseta
int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n-1) + fibonacci(n-2);
}
```

### 7. O(n!) - Faktoriaalne aeg
- Kõigi permutatsioonide genereerimine
- Äärmiselt ebaefektiivne suurte sisendite korral
- Näited: Rändkaupmehe probleem jõumeetodil, permutatsioonide genereerimine

```java
// Kõigi permutatsioonide genereerimine
void permutatsioonid(char[] sõne, int algus, int lõpp) {
    if (algus == lõpp) {
        System.out.println(new String(sõne));
    } else {
        for (int i = algus; i <= lõpp; i++) {
            // Vaheta
            char temp = sõne[algus];
            sõne[algus] = sõne[i];
            sõne[i] = temp;
            
            // Rekursioon
            permutatsioonid(sõne, algus + 1, lõpp);
            
            // Taasta (backtrack)
            temp = sõne[algus];
            sõne[algus] = sõne[i];
            sõne[i] = temp;
        }
    }
}
```

## Erijuhtude Analüüs

### Parima, Keskmise ja Halvima Juhu Analüüs

- **Parim juht** - Minimaalne operatsioonide arv (praktikas harva kasulik)
- **Keskmine juht** - Oodatav operatsioonide arv tavalistes tingimustes
- **Halvim juht** - Maksimaalne operatsioonide arv (kõige enam analüüsitud)

Näide: Lineaarotsing
- Parim juht: O(1) - Element leitakse esimeselt positsioonilt
- Keskmine juht: O(n/2) = O(n) - Element leitakse keskmiselt positsioonilt
- Halvim juht: O(n) - Element ei leita või leitakse viimaselt positsioonilt

### Amortiseeritud Analüüs

Amortiseeritud analüüs (ingl. _amortized analysis_) vaatleb operatsioonide keskmist jõudlust operatsioonide jadas, isegi kui mõned üksikud operatsioonid võivad olla kulukad.

Näide: Dünaamilise massiivi laiendamine
- Enamik lisamisi on O(1)
- Perioodilised laiendamisoperatsioonid on O(n)
- Amortiseeritud kulu lisamise kohta: O(1)

```java
// Lihtsustatud dünaamilise massiivi (ArrayList) implementatsioon
class DünaamilineMassiiv {
    private int[] elemendid;
    private int suurus;
    private int maht;
    
    public DünaamilineMassiiv() {
        maht = 10;
        elemendid = new int[maht];
        suurus = 0;
    }
    
    public void lisa(int element) {
        if (suurus == maht) {
            // Laienda massiivi (kulukas O(n) operatsioon)
            maht *= 2;
            int[] uusMassiiv = new int[maht];
            for (int i = 0; i < suurus; i++) {
                uusMassiiv[i] = elemendid[i];
            }
            elemendid = uusMassiiv;
        }
        
        // Lihtne O(1) lisamise operatsioon
        elemendid[suurus++] = element;
    }
}
```

## Algoritmide Optimeerimine

- **Tuvasta pudelikael algoritmis**
  - Leia kõige keerukam osa
  - Keskendu koodiosadele, mis käivituvad kõige sagedamini või suuremate sisenditega

- **Väldi tarbetut tööd või korduvaid arvutusi**
  - Kasuta memoiseerimiset (tulemuste meeldejätmine)
  - Eemalda mittevajalikud operatsioonid

- **Kasuta efektiivsemaid andmestruktuure**
  - Massiivist HashMapile (O(n) -> O(1) otsing)
  - Tavaliste puude asemel tasakaalustatud puud

- **Rakenda sobivaid algoritmi disaini tehnikaid**
  - Jaga ja valitse
  - Dünaamiline programmeerimine
  - Ahned algoritmid
  - Meelespidamine

## Ruumi- ja Ajakasutuse Kompromissid

Mõnikord saad vahetada mälu kiiruse vastu:
- Memoiseerimine korduvate arvutuste vältimiseks
- Ettearvutamine kulukate operatsioonide vältimiseks
- Täiendavate andmestruktuuride kasutamine operatsioonide kiirendamiseks

```java
// Fibonacci ilma memoiseerimiseta - O(2ⁿ) aeg
int fiboIlmaMemota(int n) {
    if (n <= 1) return n;
    return fiboIlmaMemota(n-1) + fiboIlmaMemota(n-2);
}

// Fibonacci memoiseerimisega - O(n) aeg, O(n) ruum
int fiboMemoga(int n, Integer[] memo) {
    if (memo[n] != null) return memo[n];
    if (n <= 1) return n;
    
    memo[n] = fiboMemoga(n-1, memo) + fiboMemoga(n-2, memo);
    return memo[n];
}
```

## Praktilised Näited

### Otsingud

```java
// Lineaarotsing - O(n)
int lineaarotsing(int[] massiiv, int otsitav) {
    for (int i = 0; i < massiiv.length; i++) {
        if (massiiv[i] == otsitav) {
            return i;
        }
    }
    return -1;
}

// Binaarotsing - O(log n)
int binaarotsing(int[] massiiv, int otsitav) {
    int algus = 0;
    int lõpp = massiiv.length - 1;
    
    while (algus <= lõpp) {
        int keskmine = algus + (lõpp - algus) / 2;
        
        if (massiiv[keskmine] == otsitav) {
            return keskmine;
        }
        
        if (massiiv[keskmine] < otsitav) {
            algus = keskmine + 1;
        } else {
            lõpp = keskmine - 1;
        }
    }
    
    return -1;
}
```

### Sorteerimisalgoritmid

```java
// Bubble Sort - O(n²)
void bubbleSort(int[] massiiv) {
    int n = massiiv.length;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (massiiv[j] > massiiv[j + 1]) {
                int temp = massiiv[j];
                massiiv[j] = massiiv[j + 1];
                massiiv[j + 1] = temp;
            }
        }
    }
}

// Merge Sort - O(n log n)
void mergeSort(int[] massiiv, int algus, int lõpp) {
    if (algus < lõpp) {
        int keskmine = (algus + lõpp) / 2;
        
        mergeSort(massiiv, algus, keskmine);
        mergeSort(massiiv, keskmine + 1, lõpp);
        
        merge(massiiv, algus, keskmine, lõpp);
    }
}

void merge(int[] massiiv, int algus, int keskmine, int lõpp) {
    // Loome ajutised massiivid
    int n1 = keskmine - algus + 1;
    int n2 = lõpp - keskmine;
    
    int[] vasak = new int[n1];
    int[] parem = new int[n2];
    
    // Kopeerime andmed ajutistesse massiividesse
    for (int i = 0; i < n1; i++) {
        vasak[i] = massiiv[algus + i];
    }
    for (int i = 0; i < n2; i++) {
        parem[i] = massiiv[keskmine + 1 + i];
    }
    
    // Ühendame ajutised massiivid
    int i = 0, j = 0, k = algus;
    while (i < n1 && j < n2) {
        if (vasak[i] <= parem[j]) {
            massiiv[k] = vasak[i];
            i++;
        } else {
            massiiv[k] = parem[j];
            j++;
        }
        k++;
    }
    
    // Kopeerime allesjäänud elemendid vasakust massiivist kui neid on
    while (i < n1) {
        massiiv[k] = vasak[i];
        i++;
        k++;
    }
    
    // Kopeerime allesjäänud elemendid paremast massiivist kui neid on
    while (j < n2) {
        massiiv[k] = parem[j];
        j++;
        k++;
    }
}
```

### Dünaamiline Programmeerimine

```java
// Fibonacci dünaamilise programmeerimisega (tabuleerimine) - O(n) aeg, O(n) ruum
int fiboDünaamiline(int n) {
    if (n <= 1) return n;
    
    int[] f = new int[n + 1];
    f[0] = 0;
    f[1] = 1;
    
    for (int i = 2; i <= n; i++) {
        f[i] = f[i-1] + f[i-2];
    }
    
    return f[n];
}

// Optimeeritud dünaamiline programmeerimine - O(n) aeg, O(1) ruum
int fiboOptimeeritud(int n) {
    if (n <= 1) return n;
    
    int eelmine = 0;
    int praegune = 1;
    
    for (int i = 2; i <= n; i++) {
        int järgmine = eelmine + praegune;
        eelmine = praegune;
        praegune = järgmine;
    }
    
    return praegune;
}
```

Ajakeerukuse mõistmine on ülioluline efektiivsete algoritmide disainis ja implementeerimises. See võimaldab sul teha teadlikke otsuseid algoritmide valikul ja optimeerimismeetodite kasutamisel. Probleeme lahendades mõtle alati, kuidas sinu lahendus skaleerub erinevate sisendisuuruste korral.
