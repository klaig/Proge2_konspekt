# Algoritmide Põhialused

Algoritmid on täpsed, järjestatud juhised arvutile probleemi lahendamiseks. Nad on arvutiteaduse üdimeks, võimaldades meil luua efektiivseid lahendusi erinevatele probleemidele.

## Sisukord
- [Otsingualgoritmid](#otsingualgoritmid)
- [Sorteerimisalgoritmid](#sorteerimisalgoritmid)
- [Puu Läbimise Algoritmid](#puu-läbimise-algoritmid)
- [Graafi Algoritmid](#graafi-algoritmid)
- [Mustrite Sobitamine](#mustrite-sobitamine)
- [Matemaatilised Algoritmid](#matemaatilised-algoritmid)
- [Praktilised Näited](#praktilised-näited)

## Otsingualgoritmid

Otsingualgoritmid on kavandatud elemendi asukoha leidmiseks andmestruktuuris või eesmärgile vastava oleku leidmiseks otsinguruumis.

### Lineaarotsing (Linear Search)

Lineaarotsing ehk järjestikune otsing vaatab elemendid läbi ükshaaval, kuni leiab otsitava elemendi või läbib kogu struktuuri.

```java
public static int lineaarotsing(int[] massiiv, int otsitav) {
    for (int i = 0; i < massiiv.length; i++) {
        if (massiiv[i] == otsitav) {
            return i;  // Tagasta leitud elemendi indeks
        }
    }
    return -1;  // Element puudub massiivis
}
```

- **Ajakeerukus**: O(n) - halvemal juhul peame kontrollima kõiki elemente
- **Ruumikeerukus**: O(1) - vajame ainult fikseeritud arvu muutujaid
- **Eelised**: Lihtne implementeerida, töötab sorteerimata andmetel
- **Puudused**: Aeglane suurte massiivide jaoks

### Binaarotsing (Binary Search)

Binaarotsing on oluliselt efektiivsem, kuid nõuab sorteeritud andmeid. Algoritm võrdleb otsitavat elementi keskmise elemendiga ja otsustab, kas jätkata otsimist vasakul või paremal alammassiivil.

```java
public static int binaarotsing(int[] massiiv, int otsitav) {
    int madal = 0;
    int kõrge = massiiv.length - 1;
    
    while (madal <= kõrge) {
        int kesk = madal + (kõrge - madal) / 2;
        
        // Kontrolli, kas otsitav element on keskel
        if (massiiv[kesk] == otsitav) {
            return kesk;
        }
        
        // Kui otsitav on suurem, ignoreeri vasakut poolt
        if (massiiv[kesk] < otsitav) {
            madal = kesk + 1;
        }
        // Kui otsitav on väiksem, ignoreeri paremat poolt
        else {
            kõrge = kesk - 1;
        }
    }
    
    return -1;  // Element puudub massiivis
}
```

- **Ajakeerukus**: O(log n) - iga sammuga jagame otsinguruumi poole väiksemaks
- **Ruumikeerukus**: O(1) - iteratiivne versioon vajab konstantset ruumi
- **Eelised**: Väga efektiivne suurte sorteeritud andmehulkade jaoks
- **Puudused**: Nõuab sorteeritud andmeid

#### Rekursiivne Binaarotsing

```java
public static int binarOrsingRekursiivne(int[] massiiv, int otsitav, int madal, int kõrge) {
    if (madal > kõrge) {
        return -1;  // Baas juht: element puudub massiivis
    }
    
    int kesk = madal + (kõrge - madal) / 2;
    
    // Kui element on keskel
    if (massiiv[kesk] == otsitav) {
        return kesk;
    }
    
    // Kui element on väiksem kui keskmine, otsi vasakus alammasiivis
    if (massiiv[kesk] > otsitav) {
        return binarOrsingRekursiivne(massiiv, otsitav, madal, kesk - 1);
    }
    
    // Muul juhul otsi paremas alammasiivis
    return binarOrsingRekursiivne(massiiv, otsitav, kesk + 1, kõrge);
}
```

### Hüppeotsing (Jump Search)

Hüppeotsing on lineaar- ja binaarotsingu vaheline algoritm, mis sorteeritud massiivis "hüppab" fikseeritud sammudega ja seejärel teeb lineaarotsingu vastavas blokis.

```java
public static int hüppeotsing(int[] massiiv, int otsitav) {
    int n = massiiv.length;
    int samm = (int) Math.floor(Math.sqrt(n));
    
    // Leia blokk, kus element võiks asuda
    int eelmineIndeks = 0;
    while (massiiv[Math.min(samm, n) - 1] < otsitav) {
        eelmineIndeks = samm;
        samm += (int) Math.floor(Math.sqrt(n));
        if (eelmineIndeks >= n) {
            return -1;
        }
    }
    
    // Tee lineaarotsing blokis
    while (massiiv[eelmineIndeks] < otsitav) {
        eelmineIndeks++;
        if (eelmineIndeks == Math.min(samm, n)) {
            return -1;
        }
    }
    
    // Kui element on leitud
    if (massiiv[eelmineIndeks] == otsitav) {
        return eelmineIndeks;
    }
    
    return -1;
}
```

- **Ajakeerukus**: O(√n) - optimaalne, kui sammude suurus on valitud √n
- **Ruumikeerukus**: O(1)
- **Eelised**: Parem kui lineaarotsing, kiirem kui binaarotsing väikeste massiivide korral
- **Puudused**: Nõuab sorteeritud andmeid, halvem kui binaarotsing suurte massiivide korral

## Sorteerimisalgoritmid

Sorteerimisalgoritmid järjestavad andmeid määratud kriteeriumite järgi, tavaliselt kasvavalt või kahanevalt.

### Mullidse Sorteerimine (Bubble Sort)

Mullide sorteerimine liigub läbi massiivi ja vahetab kõrvuti asetsevaid elemente, kui need on vales järjekorras.

```java
public static void mullideSorteerimine(int[] massiiv) {
    int n = massiiv.length;
    boolean vahetusi;
    
    for (int i = 0; i < n - 1; i++) {
        vahetusi = false;
        
        for (int j = 0; j < n - i - 1; j++) {
            if (massiiv[j] > massiiv[j + 1]) {
                // Vaheta elemendid
                int temp = massiiv[j];
                massiiv[j] = massiiv[j + 1];
                massiiv[j + 1] = temp;
                vahetusi = true;
            }
        }
        
        // Kui vahetusi pole tehtud, siis massiiv on juba sorteeritud
        if (!vahetusi) {
            break;
        }
    }
}
```

- **Ajakeerukus**: O(n²) halvimal ja keskmisel juhul, O(n) parimal juhul (juba sorteeritud)
- **Ruumikeerukus**: O(1)
- **Stabiilsus**: Stabiilne (säilitab võrdsete elementide algse järjekorra)
- **Eelised**: Lihtne implementeerida, efektiivne väikestel ja peaaegu sorteeritud massiividel
- **Puudused**: Ebaefektiivne suurtel massiividel

### Sisestussorteerimine (Insertion Sort)

Sisestussorteerimine ehitab lõpliku sorteeritud massiivi üks element korraga, võttes elemendid algsest massiivist ja sisestades need õigesse kohta.

```java
public static void sisestussorteerimine(int[] massiiv) {
    int n = massiiv.length;
    
    for (int i = 1; i < n; i++) {
        int võti = massiiv[i];
        int j = i - 1;
        
        // Liiguta elemente, mis on suuremad kui võti, ühe positsiooni võrra edasi
        while (j >= 0 && massiiv[j] > võti) {
            massiiv[j + 1] = massiiv[j];
            j = j - 1;
        }
        massiiv[j + 1] = võti;
    }
}
```

- **Ajakeerukus**: O(n²) halvimal ja keskmisel juhul, O(n) parimal juhul
- **Ruumikeerukus**: O(1)
- **Stabiilsus**: Stabiilne
- **Eelised**: Lihtne, efektiivne väikestel massiividel ja peaaegu sorteeritud massiividel, vähesed vahetused
- **Puudused**: Ebaefektiivne suurtel sorteerimata massiividel

### Valimissorteerimine (Selection Sort)

Valimissorteerimine leiab järjest massiivi minimaalse elemendi ja asetab selle algusesse.

```java
public static void valimissorteerimine(int[] massiiv) {
    int n = massiiv.length;
    
    for (int i = 0; i < n - 1; i++) {
        int minIndeks = i;
        
        // Leia väikseim element sorteerimata osas
        for (int j = i + 1; j < n; j++) {
            if (massiiv[j] < massiiv[minIndeks]) {
                minIndeks = j;
            }
        }
        
        // Vaheta leitud miinimum i-nda elemendiga
        int temp = massiiv[minIndeks];
        massiiv[minIndeks] = massiiv[i];
        massiiv[i] = temp;
    }
}
```

- **Ajakeerukus**: O(n²) kõigil juhtudel
- **Ruumikeerukus**: O(1)
- **Stabiilsus**: Ebastabiilne (võib muuta võrdsete elementide järjekorda)
- **Eelised**: Lihtne, minimaalne vahetuste arv
- **Puudused**: Aeglane suurtel massiividel, alati O(n²) isegi kui massiiv on juba sorteeritud

### Kiirsorteerimine (Quick Sort)

Kiirsorteerimine kasutab jaga-ja-valitse strateegiat. See valib elemendi (pöördelemendi) ja jagab massiivi alammassiivideks, kus ühes on väiksemad elemendid ja teises suuremad.

```java
public static void kiirsorteerimine(int[] massiiv, int algus, int lõpp) {
    if (algus < lõpp) {
        // Paiguta pivot element ja tagasta selle indeks
        int pivotIndeks = partitsioon(massiiv, algus, lõpp);
        
        // Rekursiivselt sorteeri elemendid enne ja pärast pivotit
        kiirsorteerimine(massiiv, algus, pivotIndeks - 1);
        kiirsorteerimine(massiiv, pivotIndeks + 1, lõpp);
    }
}

private static int partitsioon(int[] massiiv, int algus, int lõpp) {
    int pivot = massiiv[lõpp];  // Valime pivotiks viimase elemendi
    int i = (algus - 1);  // Väiksemate elementide indeks
    
    for (int j = algus; j < lõpp; j++) {
        // Kui praegune element on väiksem või võrdne pivotiga
        if (massiiv[j] <= pivot) {
            i++;
            
            // Vaheta massiiv[i] ja massiiv[j]
            int temp = massiiv[i];
            massiiv[i] = massiiv[j];
            massiiv[j] = temp;
        }
    }
    
    // Vaheta massiiv[i+1] ja massiiv[lõpp] (pivot)
    int temp = massiiv[i + 1];
    massiiv[i + 1] = massiiv[lõpp];
    massiiv[lõpp] = temp;
    
    return i + 1;
}
```

- **Ajakeerukus**: O(n log n) keskmisel juhul, O(n²) halvimal juhul
- **Ruumikeerukus**: O(log n) rekursiivsete kutsete tõttu
- **Stabiilsus**: Ebastabiilne
- **Eelised**: Tavaliselt kiirem kui teised O(n log n) algoritmid, hea vahemälukäitumisega
- **Puudused**: Halvim juht O(n²), ebastabiilne, rekursiivne

### Ühildusorteerimine (Merge Sort)

Ühildusorteerimine on stabiilne, rekursiivne algoritm, mis kasutab jaga-ja-valitse strateegiat. See jagab massiivi pooleks, sorteerib rekursiivselt need pooled ja seejärel ühildab sorteeritud alammassiivid.

```java
public static void ühildusorteerimine(int[] massiiv, int algus, int lõpp) {
    if (algus < lõpp) {
        int kesk = (algus + lõpp) / 2;
        
        // Sorteeri mõlemad pooled
        ühildusorteerimine(massiiv, algus, kesk);
        ühildusorteerimine(massiiv, kesk + 1, lõpp);
        
        // Ühilda sorteeritud pooled
        ühilda(massiiv, algus, kesk, lõpp);
    }
}

private static void ühilda(int[] massiiv, int algus, int kesk, int lõpp) {
    // Leia alammassiivide suurused
    int n1 = kesk - algus + 1;
    int n2 = lõpp - kesk;
    
    // Loo ajutised massiivid
    int[] vasak = new int[n1];
    int[] parem = new int[n2];
    
    // Kopeeri andmed ajutistesse massiividesse
    for (int i = 0; i < n1; i++) {
        vasak[i] = massiiv[algus + i];
    }
    for (int j = 0; j < n2; j++) {
        parem[j] = massiiv[kesk + 1 + j];
    }
    
    // Ühilda ajutised massiivid tagasi algmassiivi
    int i = 0, j = 0;
    int k = algus;
    
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
    
    // Kopeeri vasaku massiivi allesjäänud elemendid
    while (i < n1) {
        massiiv[k] = vasak[i];
        i++;
        k++;
    }
    
    // Kopeeri parema massiivi allesjäänud elemendid
    while (j < n2) {
        massiiv[k] = parem[j];
        j++;
        k++;
    }
}
```

- **Ajakeerukus**: O(n log n) kõigil juhtudel
- **Ruumikeerukus**: O(n)
- **Stabiilsus**: Stabiilne
- **Eelised**: Stabiilne, garanteeritud O(n log n) jõudlus
- **Puudused**: Vajab täiendavat mäluruumi, vähem efektiivne väikestel massiividel võrreldes sisestusmeetoditega

### Kuhjastussorteerimine (Heap Sort)

Kuhjastussorteerimine kasutab binaarkuhja andmestruktuuri massiivi sorteerimiseks.

```java
public static void kuhjasorteerimine(int[] massiiv) {
    int n = massiiv.length;
    
    // Ehita maks-kuhi
    for (int i = n / 2 - 1; i >= 0; i--) {
        kuhjasta(massiiv, n, i);
    }
    
    // Eemalda elemendid kuhjast üks haaval
    for (int i = n - 1; i > 0; i--) {
        // Liiguta juur lõppu
        int temp = massiiv[0];
        massiiv[0] = massiiv[i];
        massiiv[i] = temp;
        
        // Kuhjasta vähendatud kuhi
        kuhjasta(massiiv, i, 0);
    }
}

private static void kuhjasta(int[] massiiv, int n, int i) {
    int suurim = i;  // Algväärtusta suurim kui juur
    int vasak = 2 * i + 1;
    int parem = 2 * i + 2;
    
    // Kui vasak laps on suurem kui juur
    if (vasak < n && massiiv[vasak] > massiiv[suurim]) {
        suurim = vasak;
    }
    
    // Kui parem laps on suurem kui suurim seni
    if (parem < n && massiiv[parem] > massiiv[suurim]) {
        suurim = parem;
    }
    
    // Kui suurim ei ole juur
    if (suurim != i) {
        int vahetus = massiiv[i];
        massiiv[i] = massiiv[suurim];
        massiiv[suurim] = vahetus;
        
        // Rekursiivselt kuhjasta mõjutatud alamkuhi
        kuhjasta(massiiv, n, suurim);
    }
}
```

- **Ajakeerukus**: O(n log n) kõigil juhtudel
- **Ruumikeerukus**: O(1)
- **Stabiilsus**: Ebastabiilne
- **Eelised**: In-place, garanteeritud O(n log n) jõudlus
- **Puudused**: Ebastabiilne, aeglasem kui kiirsorteerimine praktikas

### Loendamissorteerimine (Counting Sort)

Loendamissorteerimine on mittevõrdluspõhine algoritm, mis töötab hästi teadaolevate piiridega täisarvude sorteerimisel.

```java
public static void loendamissorteerimine(int[] massiiv, int max) {
    int n = massiiv.length;
    int[] väljund = new int[n];
    int[] loendur = new int[max + 1];
    
    // Loenda elementide esinemist
    for (int i = 0; i < n; i++) {
        loendur[massiiv[i]]++;
    }
    
    // Muuda loendur kumulatiivseks
    for (int i = 1; i <= max; i++) {
        loendur[i] += loendur[i - 1];
    }
    
    // Ehita väljundmassiiv
    for (int i = n - 1; i >= 0; i--) {
        väljund[loendur[massiiv[i]] - 1] = massiiv[i];
        loendur[massiiv[i]]--;
    }
    
    // Kopeeri väljundmassiiv algmassivi
    for (int i = 0; i < n; i++) {
        massiiv[i] = väljund[i];
    }
}
```

- **Ajakeerukus**: O(n + k), kus k on võimalike väärtuste vahemik
- **Ruumikeerukus**: O(n + k)
- **Stabiilsus**: Stabiilne
- **Eelised**: Efektiivne, kui vahemik on väike võrreldes n-ga
- **Puudused**: Vajab teadmist vahemikust, täiendavat mälu

### Radixsorteerimine (Radix Sort)

Radixsorteerimine käsitleb arve ühe numbrikoha kaupa, alustades vähimtähtsast kohast (LSD) või kõigetähtsaimast kohast (MSD).

```java
public static void radixsorteerimine(int[] massiiv) {
    // Leia suurim number, et teada, mitu korda läbida
    int max = getMax(massiiv);
    
    // Tee loendamissorteerimist iga koha jaoks
    for (int exp = 1; max / exp > 0; exp *= 10) {
        loendamissortKohaJärgi(massiiv, exp);
    }
}

private static int getMax(int[] massiiv) {
    int max = massiiv[0];
    for (int i = 1; i < massiiv.length; i++) {
        if (massiiv[i] > max) {
            max = massiiv[i];
        }
    }
    return max;
}

private static void loendamissortKohaJärgi(int[] massiiv, int exp) {
    int n = massiiv.length;
    int[] väljund = new int[n];
    int[] loendur = new int[10]; // 0-9 numbrid
    
    // Loenda esinemised
    for (int i = 0; i < n; i++) {
        loendur[(massiiv[i] / exp) % 10]++;
    }
    
    // Muuda loendur kumulatiivseks
    for (int i = 1; i < 10; i++) {
        loendur[i] += loendur[i - 1];
    }
    
    // Ehita väljundmassiiv
    for (int i = n - 1; i >= 0; i--) {
        väljund[loendur[(massiiv[i] / exp) % 10] - 1] = massiiv[i];
        loendur[(massiiv[i] / exp) % 10]--;
    }
    
    // Kopeeri väljundmassiiv algmassivi
    for (int i = 0; i < n; i++) {
        massiiv[i] = väljund[i];
    }
}
```

- **Ajakeerukus**: O(d * (n + k)), kus d on suurima arvu numbrikohtade arv ja k on numbrite vahemik (tavaliselt 10)
- **Ruumikeerukus**: O(n + k)
- **Stabiilsus**: Stabiilne
- **Eelised**: Võib olla kiirem kui O(n log n) algoritmid, kui d on väike
- **Puudused**: Täiendav mälu, ebaefektiivne kui d on suur

## Puu Läbimise Algoritmid

Puu läbimise algoritmid külastavad puu kõiki tippe teatud järjekorras, võimaldades andmete töötlemist, otsimist ja muud.

### Eesjärjestuses Läbimine (Pre-order Traversal)

Eesjärjestuses läbimine külastab esmalt juure, seejärel vasakut alampu ja siis paremat alampu.

```java
// Puu tipp klass
class Tipp {
    int väärtus;
    Tipp vasak, parem;
    
    public Tipp(int väärtus) {
        this.väärtus = väärtus;
        this.vasak = this.parem = null;
    }
}

// Eesjärjestuses läbimine
public static void eesjärjestus(Tipp juur) {
    if (juur == null) {
        return;
    }
    
    // Esmalt töötleme juure
    System.out.print(juur.väärtus + " ");
    
    // Siis vasaku alampuu
    eesjärjestus(juur.vasak);
    
    // Lõpuks parema alampuu
    eesjärjestus(juur.parem);
}
```

- **Kasutusalad**: Puu koopiate loomine, poliisavaldiste konstrueerimine

### Keskjärjestuses Läbimine (In-order Traversal)

Keskjärjestuses läbimine külastab esmalt vasakut alampu, seejärel juurt ja siis paremat alampu.

```java
public static void keskjärjestus(Tipp juur) {
    if (juur == null) {
        return;
    }
    
    // Esmalt töötleme vasaku alampuu
    keskjärjestus(juur.vasak);
    
    // Siis juure
    System.out.print(juur.väärtus + " ");
    
    // Lõpuks parema alampuu
    keskjärjestus(juur.parem);
}
```

- **Kasutusalad**: Binaarotsingu puude elementidele järjestatud ligipääs

### Järeljärjestuses Läbimine (Post-order Traversal)

Järeljärjestuses läbimine külastab esmalt vasakut alampu, seejärel paremat alampu ja siis juurt.

```java
public static void järeljärjestus(Tipp juur) {
    if (juur == null) {
        return;
    }
    
    // Esmalt töötleme vasaku alampuu
    järeljärjestus(juur.vasak);
    
    // Siis parema alampuu
    järeljärjestus(juur.parem);
    
    // Lõpuks juure
    System.out.print(juur.väärtus + " ");
}
```

- **Kasutusalad**: Puu kustutamine, postfiks notatsiooni avaldiste hindamine

### Tasemejärjestuses Läbimine (Level-order Traversal)

Tasemejärjestuses läbimine külastab tippe tasemete kaupa, alustades juurest ja liikudes allapoole vasakult paremale.

```java
public static void tasemejärjestus(Tipp juur) {
    if (juur == null) {
        return;
    }
    
    // Kasuta järjekorda tippude salvestamiseks
    java.util.Queue<Tipp> järjekord = new java.util.LinkedList<>();
    järjekord.add(juur);
    
    while (!järjekord.isEmpty()) {
        // Eemalda ja töötle tipud
        Tipp praegune = järjekord.poll();
        System.out.print(praegune.väärtus + " ");
        
        // Lisa vasakud ja paremad lapsed järjekorda
        if (praegune.vasak != null) {
            järjekord.add(praegune.vasak);
        }
        if (praegune.parem != null) {
            järjekord.add(praegune.parem);
        }
    }
}
```

- **Kasutusalad**: Tasemete kaupa puu analüüs, laiuti otsing puus

## Graafi Algoritmid

Graafi algoritmid on kavandatud graafidega töötamiseks, võimaldades otsimist, lühimaid teid, sidusust ja muud.

### Laiuti Otsing (Breadth-First Search, BFS)

Laiuti otsing alustab algustipust ja uurib kõiki naabreid, enne kui liigub naabritest kaugemale.

```java
public static void bfs(int[][] graaf, int algusTipp) {
    int n = graaf.length;
    boolean[] külastatud = new boolean[n];
    
    // Kasuta järjekorda tippude jaoks
    java.util.Queue<Integer> järjekord = new java.util.LinkedList<>();
    
    // Märgi alustipp külastatud ja lisa järjekorda
    külastatud[algusTipp] = true;
    järjekord.add(algusTipp);
    
    while (!järjekord.isEmpty()) {
        // Eemalda tipp järjekorrast
        int praegune = järjekord.poll();
        System.out.print(praegune + " ");
        
        // Külasta kõiki praeguse tipu naabreid
        for (int i = 0; i < n; i++) {
            if (graaf[praegune][i] == 1 && !külastatud[i]) {
                külastatud[i] = true;
                järjekord.add(i);
            }
        }
    }
}
```

- **Ajakeerukus**: O(V + E), kus V on tippude arv ja E on servade arv
- **Ruumikeerukus**: O(V)
- **Kasutusalad**: Lühima tee leidmine kaalumata graafides, graafi ühenduvuse kontrollimine

### Sügavuti Otsing (Depth-First Search, DFS)

Sügavuti otsing uurib nii kaugele kui võimalik mööda haru, enne kui tagurdab ja uurib järgmist haru.

```java
public static void dfs(int[][] graaf, int praegune, boolean[] külastatud) {
    // Märgi praegune tipp külastatud
    külastatud[praegune] = true;
    System.out.print(praegune + " ");
    
    // Rekursiivselt külasta kõiki praeguse tipu külastamata naabreid
    for (int i = 0; i < graaf.length; i++) {
        if (graaf[praegune][i] == 1 && !külastatud[i]) {
            dfs(graaf, i, külastatud);
        }
    }
}

// Käivita DFS kõigi tippude jaoks (juhul kui graaf ei ole ühendatud)
public static void dfsKõigile(int[][] graaf) {
    int n = graaf.length;
    boolean[] külastatud = new boolean[n];
    
    for (int i = 0; i < n; i++) {
        if (!külastatud[i]) {
            dfs(graaf, i, külastatud);
        }
    }
}
```

- **Ajakeerukus**: O(V + E)
- **Ruumikeerukus**: O(V)
- **Kasutusalad**: Tsüklite tuvastamine, topoloogiline sorteerimine, sidusad komponendid

### Dijkstra Algoritm

Dijkstra algoritm leiab lühimad teed graafi algustipust kõigisse teistesse tippudesse.

```java
public static void dijkstra(int[][] graaf, int algusTipp) {
    int n = graaf.length;
    int[] kaugus = new int[n];
    boolean[] lühimTee = new boolean[n];
    
    // Algväärtusta kõik kaugused "lõpmatuks" ja lühimTee array false'ks
    for (int i = 0; i < n; i++) {
        kaugus[i] = Integer.MAX_VALUE;
        lühimTee[i] = false;
    }
    
    // Kaugus algustipust iseendasse on 0
    kaugus[algusTipp] = 0;
    
    for (int count = 0; count < n - 1; count++) {
        // Vali miinimum kaugusega tipp mitte-töödeldud tippude hulgast
        int u = miinimumKaugus(kaugus, lühimTee, n);
        
        // Märgi valitud tipp töödeldud
        lühimTee[u] = true;
        
        // Uuenda valitud tipu naabertippude kaugusi
        for (int v = 0; v < n; v++) {
            // Uuenda kaugust ainult kui:
            // 1. On serv u-st v-sse
            // 2. v pole veel töödeldud
            // 3. Tee algustipust u kaudu v-sse on lühem kui praegune kaugus v-ni
            if (!lühimTee[v] && graaf[u][v] != 0 && kaugus[u] != Integer.MAX_VALUE
                    && kaugus[u] + graaf[u][v] < kaugus[v]) {
                kaugus[v] = kaugus[u] + graaf[u][v];
            }
        }
    }
    
    // Väljasta lahendus
    väljastaTulemus(kaugus, n);
}

private static int miinimumKaugus(int[] kaugus, boolean[] lühimTee, int n) {
    int min = Integer.MAX_VALUE, minIndeks = -1;
    
    for (int v = 0; v < n; v++) {
        if (!lühimTee[v] && kaugus[v] <= min) {
            min = kaugus[v];
            minIndeks = v;
        }
    }
    
    return minIndeks;
}

private static void väljastaTulemus(int[] kaugus, int n) {
    System.out.println("Lühimad teed algustipust:");
    for (int i = 0; i < n; i++) {
        System.out.println("Tippu " + i + ": " + kaugus[i]);
    }
}
```

- **Ajakeerukus**: O(V²), optimeeritult prioriteedi järjekorraga O((V + E) log V)
- **Ruumikeerukus**: O(V)
- **Kasutusalad**: GPS navigatsioon, võrguliikluse marsruutimine, transportvõrkude optimeerimine

## Mustrite Sobitamine

Mustrite sobitamise algoritmid leiavad teksti sees mustri esinemiskohad.

### Naiivne Mustrite Sobitamine

Naiivne lähenemine võrdleb mustrit kõigi võimalike positsioonidega tekstis.

```java
public static void naiivneSobitamine(String tekst, String muster) {
    int n = tekst.length();
    int m = muster.length();
    
    for (int i = 0; i <= n - m; i++) {
        int j;
        
        // Kontrolli sobituvust alates positsioonist i
        for (j = 0; j < m; j++) {
            if (tekst.charAt(i + j) != muster.charAt(j)) {
                break;
            }
        }
        
        // Kui j == m, siis muster sobitub täielikult
        if (j == m) {
            System.out.println("Muster leitud positsioonil: " + i);
        }
    }
}
```

- **Ajakeerukus**: O((n-m+1) * m) - halvimal juhul O(n*m)
- **Ruumikeerukus**: O(1)
- **Eelised**: Lihtne implementeerida, efektiivne lühikeste mustrite korral
- **Puudused**: Ebaefektiivne pikkade tekstide ja mustrite korral

### Knuth-Morris-Pratt (KMP) Algoritm

KMP algoritm kasutab eeltöötlust, et vältida ülearuseid võrdlusi mustri mittesobitumise korral.

```java
public static void kmpSobitamine(String tekst, String muster) {
    int n = tekst.length();
    int m = muster.length();
    
    // Loo eelneva eesliite sufiks (lps) array
    int[] lps = looLPS(muster, m);
    
    int i = 0;  // Indeks teksti jaoks
    int j = 0;  // Indeks mustri jaoks
    
    while (i < n) {
        // Kui sümbolid sobituvad, liigu edasi mõlemas
        if (muster.charAt(j) == tekst.charAt(i)) {
            i++;
            j++;
        }
        
        // Kui j jõuab mustri lõppu, leidsime sobituse
        if (j == m) {
            System.out.println("Muster leitud positsioonil: " + (i - j));
            j = lps[j - 1];  // Jätka otsimist järgmise sobituse jaoks
        }
        // Kui ei sobi, kasuta lps-i, et määrata järgmine j
        else if (i < n && muster.charAt(j) != tekst.charAt(i)) {
            if (j != 0) {
                j = lps[j - 1];
            } else {
                i++;
            }
        }
    }
}

private static int[] looLPS(String muster, int m) {
    int[] lps = new int[m];
    int pikkus = 0;
    
    lps[0] = 0;  // lps[0] on alati 0
    
    int i = 1;
    while (i < m) {
        if (muster.charAt(i) == muster.charAt(pikkus)) {
            pikkus++;
            lps[i] = pikkus;
            i++;
        } else {
            if (pikkus != 0) {
                pikkus = lps[pikkus - 1];
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
    
    return lps;
}
```

- **Ajakeerukus**: O(n + m)
- **Ruumikeerukus**: O(m)
- **Eelised**: Efektiivne pikkade tekstide ja mustrite korral
- **Puudused**: Keerulisem implementeerida kui naiivne algoritm

## Matemaatilised Algoritmid

### Eukleidese Algoritm (Suurim Ühistegur)

Eukleidese algoritm leiab kahe arvu suurima ühisteguri (SÜT).

```java
public static int suurimÜhistegur(int a, int b) {
    if (b == 0) {
        return a;
    }
    return suurimÜhistegur(b, a % b);
}
```

- **Ajakeerukus**: O(log min(a, b))
- **Ruumikeerukus**: O(log min(a, b)) rekursiivsete kutsete tõttu
- **Kasutusalad**: Murdude taandamine, krüptograafia, arvuteooria

### Sieve of Eratosthenes (Algearvude Leidmine)

Sõel teatud piirini kõigi algearvude leidmiseks.

```java
public static boolean[] eratostheneSõel(int n) {
    boolean[] onAlgarv = new boolean[n + 1];
    
    // Algväärtusta kõik arvud algarvudeks
    for (int i = 2; i <= n; i++) {
        onAlgarv[i] = true;
    }
    
    // Korruta iga algarvu kordsed mitte-algarvudeks
    for (int p = 2; p * p <= n; p++) {
        // Kui p on algarv, märgi kõik selle kordsed
        if (onAlgarv[p]) {
            for (int i = p * p; i <= n; i += p) {
                onAlgarv[i] = false;
            }
        }
    }
    
    return onAlgarv;
}
```

- **Ajakeerukus**: O(n log log n)
- **Ruumikeerukus**: O(n)
- **Kasutusalad**: Algearvude loendite genereerimine, krüptograafia

### Kiire Astendamine

Algoritm efektiivseks astendamiseks.

```java
public static long kiirAstendamine(long arv, long aste) {
    if (aste == 0) {
        return 1;
    }
    
    long pool = kiirAstendamine(arv, aste / 2);
    
    if (aste % 2 == 0) {
        return pool * pool;
    } else {
        return arv * pool * pool;
    }
}

// Kiire astendamine mooduli korral (krüptograafias kasulik)
public static long kiirAstendamineMoodul(long arv, long aste, long moodul) {
    arv = arv % moodul;
    long tulemus = 1;
    
    while (aste > 0) {
        // Kui aste on paaritu, korruta tulemust arvuga
        if ((aste & 1) == 1) {
            tulemus = (tulemus * arv) % moodul;
        }
        
        // Aste on nüüd paaris, kahekordista arv ja poolita aste
        aste >>= 1;  // aste = aste / 2
        arv = (arv * arv) % moodul;
    }
    
    return tulemus;
}
```

- **Ajakeerukus**: O(log n)
- **Ruumikeerukus**: O(log n) rekursiivsete kutsete tõttu
- **Kasutusalad**: Krüptograafia, modulaarne aritmeetika, efektiivne astendamine

## Praktilised Näited

### Palindroomi Kontrollimine

```java
public static boolean onPalindroom(String sõne) {
    int algus = 0;
    int lõpp = sõne.length() - 1;
    
    while (algus < lõpp) {
        // Ignoreeri mittealfanumerilisi sümboleid
        if (!Character.isLetterOrDigit(sõne.charAt(algus))) {
            algus++;
        } else if (!Character.isLetterOrDigit(sõne.charAt(lõpp))) {
            lõpp--;
        } else {
            // Võrdle sümboleid tõstutundetult
            if (Character.toLowerCase(sõne.charAt(algus)) != Character.toLowerCase(sõne.charAt(lõpp))) {
                return false;
            }
            algus++;
            lõpp--;
        }
    }
    
    return true;
}
```

### Kaks massiivi liitmine

```java
public static int[] liidaMassiivid(int[] a, int[] b) {
    int n = a.length;
    int m = b.length;
    int[] tulemus = new int[n + m];
    
    int i = 0, j = 0, k = 0;
    
    // Sega elemendid võrreldes
    while (i < n && j < m) {
        if (a[i] <= b[j]) {
            tulemus[k++] = a[i++];
        } else {
            tulemus[k++] = b[j++];
        }
    }
    
    // Kopeeri allesjäänud elemendid
    while (i < n) {
        tulemus[k++] = a[i++];
    }
    
    while (j < m) {
        tulemus[k++] = b[j++];
    }
    
    return tulemus;
}
```

### Anagrammi Kontroll

```java
public static boolean onAnagramm(String sõne1, String sõne2) {
    // Eemalda tühikud ja muuda väiketähtedeks
    sõne1 = sõne1.replaceAll("\\s", "").toLowerCase();
    sõne2 = sõne2.replaceAll("\\s", "").toLowerCase();
    
    // Kui pikkused ei ole võrdsed, ei ole anagramm
    if (sõne1.length() != sõne2.length()) {
        return false;
    }
    
    // Loenda sümbolite esinemiskordi
    int[] loendur = new int[256];  // Eeldame ASCII sümboleid
    
    for (int i = 0; i < sõne1.length(); i++) {
        loendur[sõne1.charAt(i)]++;
        loendur[sõne2.charAt(i)]--;
    }
    
    // Kui kõik loenduri väärtused on 0, on tegemist anagrammiga
    for (int count : loendur) {
        if (count != 0) {
            return false;
        }
    }
    
    return true;
}
```

### Puuduvate arvude leidmine massiivis

```java
public static List<Integer> leiaPuuduvadArvud(int[] massiiv, int n) {
    List<Integer> puuduvad = new ArrayList<>();
    boolean[] olemas = new boolean[n + 1];
    
    // Märgi kõik massiivis olevad arvud
    for (int arv : massiiv) {
        if (arv >= 1 && arv <= n) {
            olemas[arv] = true;
        }
    }
    
    // Lisa puuduvad arvud tulemusse
    for (int i = 1; i <= n; i++) {
        if (!olemas[i]) {
            puuduvad.add(i);
        }
    }
    
    return puuduvad;
}
```

Algoritmide tundmine on kriitilise tähtsusega efektiivsete lahenduste loomiseks. Õppides tundma erinevaid algoritme ja nende rakendusi, saad paremini valida sobiva lähenemise iga probleemi jaoks.
