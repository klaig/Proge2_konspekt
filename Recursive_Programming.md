# Rekursiivne Programmeerimine

Rekursioon on võimas programmeerimistehnika, kus funktsioon kutsub iseennast, et lahendada väiksemaid alaülesandeid. See on eriti kasulik probleemide lahendamisel, mida saab loomulikult jagada väiksemateks alamprobleemideks.

## Sisukord
- [Rekursiooni Põhialused](#rekursiooni-põhialused)
- [Rekursiooni Tüübid](#rekursiooni-tüübid)
- [Rekursioonipuu](#rekursioonipuu)
- [Binaarse Rekursiooni Rakendused](#binaarse-rekursiooni-rakendused)
- [Rekursioon vs Iteratsioon](#rekursioon-vs-iteratsioon)
- [Rekursiooni Optimeerimine](#rekursiooni-optimeerimine)
- [Praktilised Näited](#praktilised-näited)

## Rekursiooni Põhialused

### Baasjuht (Base Case)
Baasjuht on triviaalne alamprobleem, mida saab lahendada otse ilma rekursioonita. Iga rekursiivne algoritm peab sisaldama vähemalt ühte baasjuhtu, et vältida lõpmatut rekursiooni.

### Rekursiivne Funktsioon
Rekursiivne funktsioon tagastab väärtuse, mis on arvutatud rekursiivsete väljakutsete kaudu. See funktsioon lahendab probleemi, kutsudes iseennast väiksema sisendiga.

```java
// Rekursiivne funktsioon faktoriaal arvutamiseks
static int faktoriaal(int n) {
    // Baasjuht
    if (n <= 1) {
        return 1;
    }
    
    // Rekursiivne väljakutse
    return n * faktoriaal(n - 1);
}
```

### Rekursiivne Protseduur
Rekursiivne protseduur muudab sisendparameetreid rekursiivsete väljakutsete kaudu. Erinevalt rekursiivsest funktsioonist ei pruugi see tagastada väärtust.

```java
// Rekursiivne protseduur massiivi elementide väljastamiseks
static void väljastaMassiiv(int[] massiiv, int indeks) {
    // Baasjuht
    if (indeks >= massiiv.length) {
        return;
    }
    
    // Töötlus
    System.out.print(massiiv[indeks] + " ");
    
    // Rekursiivne väljakutse
    väljastaMassiiv(massiiv, indeks + 1);
}
```

### Sisendparameeter ja Sisend-väljundparameeter
- **Sisendparameeter (Input Parameter)**: Väärtus, mida kasutatakse arvutuseks, kuid ei muudeta rekursiooni käigus.
- **Sisend-väljundparameeter (Input-output Parameter)**: Väärtus, mida muudetakse funktsiooni täitmise käigus ja millele koguneb lõpptulemus.

```java
// Näide mõlemast parameetri tüübist
static void summaRekursiooniga(int[] massiiv, int indeks, int[] tulemus) {
    // indeks - sisendparameeter
    // tulemus - sisend-väljundparameeter
    
    // Baasjuht
    if (indeks >= massiiv.length) {
        return;
    }
    
    // Muudame sisend-väljundparameetrit
    tulemus[0] += massiiv[indeks];
    
    // Rekursiivne väljakutse
    summaRekursiooniga(massiiv, indeks + 1, tulemus);
}

// Kasutamine:
int[] massiiv = {1, 2, 3, 4, 5};
int[] tulemus = {0};  // Alustame nullist
summaRekursiooniga(massiiv, 0, tulemus);
System.out.println("Summa: " + tulemus[0]);  // Summa: 15
```

## Rekursiooni Tüübid

### Unaarne Rekursioon (Lineaarne Rekursioon)
Unaarne rekursioon on rekursiooni tüüp, kus funktsiooni kehas on täpselt üks rekursiivne väljakutse. See on kõige lihtsam rekursiooni vorm.

```java
// Unaarne rekursioon: massiivi summa arvutamine
static int massiivisumma(int[] massiiv, int n) {
    // Baasjuht
    if (n <= 0) {
        return 0;
    }
    
    // Rekursiivne väljakutse (ainult üks kutse)
    return massiiv[n-1] + massiivisumma(massiiv, n-1);
}
```

#### Sabarekursioon (Tail Recursion)
Sabarekursioon on unaarse rekursiooni erijuht, kus rekursiivne väljakutse on viimane operatsioon funktsioonis. See tähendab, et pärast rekursiivset kutset ei tehta enam arvutusi.

```java
// Sabarekursioon: loendamine
static void loenda(int n) {
    // Baasjuht
    if (n <= 0) {
        return;
    }
    
    // Töötlus enne rekursiivset väljakutset
    System.out.println(n);
    
    // Sabarekursiivne väljakutse (viimane operatsioon)
    loenda(n-1);
}

// Sabarekursioon faktoriaal arvutamiseks (akumulaator-stiilis)
static int fakSabareksursiooniga(int n, int akumulaator) {
    // Baasjuht
    if (n <= 1) {
        return akumulaator;
    }
    
    // Sabarekursiivne väljakutse (viimane operatsioon)
    return fakSabareksursiooniga(n-1, n * akumulaator);
}

// Kasutamine:
int tulemus = fakSabareksursiooniga(5, 1);  // 5! = 120
```

Sabarekursiooni eelis on see, et mõned kompilaatorid saavad seda optimeerida, muutes selle iteratiivseks vormiks, mis ei kasuta täiendavat mälu rekursiivsete väljakutsete jaoks.

### Binaarne Rekursioon
Binaarne rekursioon on rekursiooni tüüp, kus funktsioon teeb kaks rekursiivset väljakutset. See on levinud jaga-ja-valitse algoritmides.

```java
// Binaarne rekursioon: Fibonacci arvude arvutamine
static int fibo(int n) {
    // Baasjuhud
    if (n <= 0) {
        return 0;
    }
    if (n == 1) {
        return 1;
    }
    
    // Kaks rekursiivset väljakutset
    return fibo(n-1) + fibo(n-2);
}
```

### Ternaarne Rekursioon
Ternaarne rekursioon on rekursiooni tüüp, kus funktsioon teeb kolm rekursiivset väljakutset. Näiteks võib tuua trepist ülesmineku probleemi, kus saab võtta 1, 2 või 3 astet korraga.

```java
// Ternaarne rekursioon: trepist ülesmineku võimaluste arv
static int trepist(int n) {
    // Baasjuhud
    if (n < 0) {
        return 0;
    }
    if (n == 0) {
        return 1;  // On täpselt üks viis mitte astuda ühtegi astet (kui ollakse juba tipus)
    }
    
    // Kolm rekursiivset väljakutset
    return trepist(n-1) + trepist(n-2) + trepist(n-3);
}
```

### Multirekursioon
Multirekursioon on rekursiooni tüüp, kus funktsioon teeb muutuva arvu rekursiivseid väljakutseid, mis võivad sõltuda sisendparameetritest. Näiteks permutatsioonide genereerimine.

```java
// Multirekursioon: permutatsioonide genereerimine
static void permutatsioonid(String s, String tulemus) {
    // Baasjuht
    if (s.length() == 0) {
        System.out.println(tulemus);
        return;
    }
    
    // Iga sümboli kohta teeme rekursiivse väljakutse
    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        String uusSõne = s.substring(0, i) + s.substring(i+1);
        
        // Rekursiivne väljakutse iga sümboliga
        permutatsioonid(uusSõne, tulemus + c);
    }
}
```

## Rekursioonipuu

Rekursioonipuu on rekursiivsete väljakutsete visuaalne esitus, kus:
- Tipud kujutavad funktsioonide väljakutseid konkreetsete parameetritega
- Servad kujutavad väljakutsuja-väljakutsutu suhteid
- Lehtedes on baasjuhud

Rekursioonipuu võimaldab analüüsida rekursiivse algoritmi aja- ja ruumikeerukust ning mõista täitmisvoolu.

### Näide: Fibonacci arvu `f(4)` rekursioonipuu

```
       f(4)
      /    \
    f(3)    f(2)
   /   \    /   \
f(2)   f(1) f(1) f(0)
/   \
f(1) f(0)
```

Sellest puust näeme, et mõningaid funktsiooniväljatkutseid (näiteks `f(2)` and `f(1)`) korratakse mitu korda, mis viitab ebaefektiivsusele. See illustreerib vajadust memoisation-tehnika (tulemuste meeldejätmise) järele.

## Binaarse Rekursiooni Rakendused

### Bitivektor Genereerimine
Bitvektorid on järjendid, mis koosnevad ainult bittidest (0 või 1). Rekursiooni abil saame genereerida kõik võimalikud bitvektorid pikkusega n.

```java
// Kõigi pikkusega n bitvektorite genereerimine
static void genereeribitvektor(int[] vektor, int indeks) {
    // Baasjuht: kui oleme täitnud kogu vektori
    if (indeks == vektor.length) {
        // Väljastame vektori
        for (int bit : vektor) {
            System.out.print(bit);
        }
        System.out.println();
        return;
    }
    
    // Proovime mõlemat võimalikku väärtust (0 ja 1) selle positsiooni jaoks
    vektor[indeks] = 0;
    genereeribitvektor(vektor, indeks + 1);
    
    vektor[indeks] = 1;
    genereeribitvektor(vektor, indeks + 1);
}

// Kasutamine:
int n = 3;
int[] vektor = new int[n];
genereeribitvektor(vektor, 0);
// Väljastab:
// 000
// 001
// 010
// 011
// 100
// 101
// 110
// 111
```

### Alamhulkade Genereerimine
Rekursiooni abil saame genereerida kõik antud hulga alamhulgad.

```java
// Kõigi alamhulkade genereerimine
static void genereeriAlamhulgad(int[] hulk, boolean[] kaasatud, int indeks) {
    // Baasjuht: kui oleme läbinud kogu hulga
    if (indeks == hulk.length) {
        // Väljasta aktiivne alamhulk
        System.out.print("{ ");
        for (int i = 0; i < hulk.length; i++) {
            if (kaasatud[i]) {
                System.out.print(hulk[i] + " ");
            }
        }
        System.out.println("}");
        return;
    }
    
    // Jätame elemendi vahele (ei kaasa alamhulka)
    kaasatud[indeks] = false;
    genereeriAlamhulgad(hulk, kaasatud, indeks + 1);
    
    // Kaasame elemendi alamhulka
    kaasatud[indeks] = true;
    genereeriAlamhulgad(hulk, kaasatud, indeks + 1);
}

// Kasutamine:
int[] hulk = {1, 2, 3};
boolean[] kaasatud = new boolean[hulk.length];
genereeriAlamhulgad(hulk, kaasatud, 0);
```

### Permutatsioonide Genereerimine
Juba eelnevalt nägime permutatsioonide genereerimist, kuid siin on teine lähenemine:

```java
// Permutatsioonide genereerimine vahetuste abil
static void genereeriPermutatsioonid(int[] massiiv, int algusIndeks) {
    // Baasjuht: kui oleme jõudnud massiivi lõppu
    if (algusIndeks == massiiv.length - 1) {
        // Väljastame permutatsiooni
        for (int num : massiiv) {
            System.out.print(num + " ");
        }
        System.out.println();
        return;
    }
    
    // Proovime kõiki võimalikke vahetusi
    for (int i = algusIndeks; i < massiiv.length; i++) {
        // Vahetame elemendid
        int temp = massiiv[algusIndeks];
        massiiv[algusIndeks] = massiiv[i];
        massiiv[i] = temp;
        
        // Rekursiivne väljakutse
        genereeriPermutatsioonid(massiiv, algusIndeks + 1);
        
        // Taastame algse oleku (backtracking)
        temp = massiiv[algusIndeks];
        massiiv[algusIndeks] = massiiv[i];
        massiiv[i] = temp;
    }
}

// Kasutamine:
int[] massiiv = {1, 2, 3};
genereeriPermutatsioonid(massiiv, 0);
```

## Rekursioon vs Iteratsioon

Nii rekursioon kui ka iteratsioon võivad lahendada samu probleeme, kuid neil on erinevad tugevused ja nõrkused.

### Eelised ja Puudused

| Rekursioon | Iteratsioon |
|------------|-------------|
| **Eelised** |
| Elegantne ja lühike kood | Tavaliselt kiirem (vähem üldist töö) |
| Loogiline mitme haru puhul | Parem mälukasutus (pole väljakutsete magasini) |
| Loomupärane jaga-ja-valitse probleemidele | Võib optimeerida silmustena |
| **Puudused** |
| Võib põhjustada magasini ületäitumist | Kood võib olla keerulisem/pikkusem |
| Aeglasem väljakutsete üldkulude tõttu | Keerulisem implementeerida mõne algoritmi puhul |
| Rohkem mälukasutust | |

### Rekursiivse koodi iteratiivseks teisendamine

Mõned rekursiivsed lahendused saab teisendada iteratiivseteks, eriti sabarekursiooni puhul.

```java
// Rekursiivne faktoriaal
static int faktoriaalRek(int n) {
    if (n <= 1) return 1;
    return n * faktoriaalRek(n-1);
}

// Iteratiivne faktoriaal
static int faktoriaalIter(int n) {
    int tulemus = 1;
    for (int i = 2; i <= n; i++) {
        tulemus *= i;
    }
    return tulemus;
}

// Rekursiivne Fibonacci (ebaefektiivne)
static int fiboRek(int n) {
    if (n <= 1) return n;
    return fiboRek(n-1) + fiboRek(n-2);
}

// Iteratiivne Fibonacci (efektiivne)
static int fiboIter(int n) {
    if (n <= 1) return n;
    
    int eelmine = 0;
    int praegune = 1;
    
    for (int i = 2; i <= n; i++) {
        int uus = eelmine + praegune;
        eelmine = praegune;
        praegune = uus;
    }
    
    return praegune;
}
```

## Rekursiooni Optimeerimine

### Memoiseerimine (Memoization)
Memoiseerimine on tehnika, kus salvestame juba arvutatud alamprobleemide lahendused, et vältida nende korduvat arvutamist. See on eriti kasulik dünaamilise programmeerimise probleemide puhul.

```java
// Fibonacci arvutamine memoiseerimisega
static int fiboMemo(int n, Integer[] memo) {
    // Baasjuhud
    if (n <= 1) {
        return n;
    }
    
    // Kui tulemus on juba arvutatud, tagastame selle
    if (memo[n] != null) {
        return memo[n];
    }
    
    // Arvutame ja salvestame tulemuse
    memo[n] = fiboMemo(n-1, memo) + fiboMemo(n-2, memo);
    return memo[n];
}

// Kasutamine:
int n = 10;
Integer[] memo = new Integer[n+1];
System.out.println(fiboMemo(n, memo));  // 55
```

### Sabarekursiooni Optimeerimine
Sabarekursioon on rekursiooni erijuht, kus rekursiivne väljakutse on viimane operatsioon. Mõned kompilaatorid optimeerivad sabarekursiooni, muutes selle iteratiivseks vormiks.

```java
// Tavaline faktoriaal
static int fakt(int n) {
    if (n <= 1) return 1;
    return n * fakt(n-1);
}

// Sabarekursiivne faktoriaal (akumulaatoriga)
static int faktSaba(int n, int akumulaator) {
    if (n <= 1) return akumulaator;
    return faktSaba(n-1, n * akumulaator);
}

// Kasutamine:
System.out.println(faktSaba(5, 1));  // 120
```

Java kompilaator ei optimeeri sabarekursiooni automaatselt, aga sabarekursiivsed algoritmid on tavaliselt lihtsam teisendada iteratiivseteks.

## Praktilised Näited

### Hannoi Tornid
Klassikaline rekursiooni näide, kus eesmärk on liigutada n ketast ühest vardast teise, kasutades kolmandat abivarrast.

```java
static void hanoi(int n, char algusVarras, char abiVarras, char lõppVarras) {
    // Baasjuht
    if (n == 1) {
        System.out.println("Liiguta ketas 1 varras " + algusVarras + " vardasse " + lõppVarras);
        return;
    }
    
    // Liiguta n-1 ketast algusest abivardasse
    hanoi(n-1, algusVarras, lõppVarras, abiVarras);
    
    // Liiguta alumine ketas algusest lõpp-vardasse
    System.out.println("Liiguta ketas " + n + " varras " + algusVarras + " vardasse " + lõppVarras);
    
    // Liiguta n-1 ketast abivardast lõpp-vardasse
    hanoi(n-1, abiVarras, algusVarras, lõppVarras);
}

// Kasutamine:
int n = 3;
hanoi(n, 'A', 'B', 'C');
```

### Kiire Astendamine
Rekursiivne algoritm arvude kiireks astendamiseks, kasutades jaga-ja-valitse põhimõtet.

```java
static long kiirAstendamine(long arv, int aste) {
    // Baasjuhud
    if (aste == 0) {
        return 1;
    }
    if (aste == 1) {
        return arv;
    }
    
    // Rekursiivne väljakutse
    long poolAste = kiirAstendamine(arv, aste / 2);
    
    // Kui aste on paaris
    if (aste % 2 == 0) {
        return poolAste * poolAste;
    } else {
        // Kui aste on paaritu
        return arv * poolAste * poolAste;
    }
}

// Kasutamine:
System.out.println(kiirAstendamine(2, 10));  // 1024
```

### Kahendpuu Läbimine
Rekursioon on loomulik viis puudega töötamiseks.

```java
class Tipp {
    int väärtus;
    Tipp vasak;
    Tipp parem;
    
    Tipp(int väärtus) {
        this.väärtus = väärtus;
        this.vasak = null;
        this.parem = null;
    }
}

// Keskjärjestuses läbimine (in-order traversal)
static void keskjärjestus(Tipp juur) {
    if (juur == null) {
        return;
    }
    
    keskjärjestus(juur.vasak);  // Esmalt vasak alampuu
    System.out.print(juur.väärtus + " ");  // Siis juur
    keskjärjestus(juur.parem);  // Lõpuks parem alampuu
}

// Eesjärjestuses läbimine (pre-order traversal)
static void eesjärjestus(Tipp juur) {
    if (juur == null) {
        return;
    }
    
    System.out.print(juur.väärtus + " ");  // Esmalt juur
    eesjärjestus(juur.vasak);  // Siis vasak alampuu
    eesjärjestus(juur.parem);  // Lõpuks parem alampuu
}

// Järeljärjestuses läbimine (post-order traversal)
static void järeljärjestus(Tipp juur) {
    if (juur == null) {
        return;
    }
    
    järeljärjestus(juur.vasak);  // Esmalt vasak alampuu
    järeljärjestus(juur.parem);  // Siis parem alampuu
    System.out.print(juur.väärtus + " ");  // Lõpuks juur
}
```

### Tagurdamine (Backtracking)
Tagurdamine on rekursiivne tehnika, kus uuritakse kõik võimalikud lahendused ja tagurdatakse, kui lahendus ei sobi.

```java
// N-malevannude probleem: paiguta n malevanda n×n malelaua nii, et ükski ei ründaks teist
static boolean nMalevandad(int[][] laud, int veerg, int n) {
    // Baasjuht: kui kõik lipud on paigutatud
    if (veerg >= n) {
        // Väljastame lahenduse
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                System.out.print(laud[i][j] + " ");
            }
            System.out.println();
        }
        System.out.println();
        return true;
    }
    
    boolean tulemus = false;
    
    // Proovime paigutada vanurit igasse ritta selles veerus
    for (int i = 0; i < n; i++) {
        // Kontrollime, kas saame paigutada vannuri positsiooni [i][veerg]
        if (onTurvaline(laud, i, veerg, n)) {
            // Paigutame vannuri
            laud[i][veerg] = 1;
            
            // Rekursiivne väljakutse
            tulemus = nMalevandad(laud, veerg + 1, n) || tulemus;
            
            // Tagurdamine (backtracking)
            laud[i][veerg] = 0;
        }
    }
    
    return tulemus;
}

static boolean onTurvaline(int[][] laud, int rida, int veerg, int n) {
    // Kontrollime rida vasakule
    for (int j = 0; j < veerg; j++) {
        if (laud[rida][j] == 1) {
            return false;
        }
    }
    
    // Kontrollime ülemist vasak diagonaali
    for (int i = rida, j = veerg; i >= 0 && j >= 0; i--, j--) {
        if (laud[i][j] == 1) {
            return false;
        }
    }
    
    // Kontrollime alumist vasak diagonaali
    for (int i = rida, j = veerg; i < n && j >= 0; i++, j--) {
        if (laud[i][j] == 1) {
            return false;
        }
    }
    
    return true;
}

// Kasutamine:
int n = 4;
int[][] laud = new int[n][n];
nMalevandad(laud, 0, n);
```

Rekursioon on võimas tehnika, mida kasutatakse paljudes algoritmides ja andmestruktuurides. See on eriti kasulik jaga-ja-valitse probleemide, puude ja graafide läbimise ning loendamise probleemide lahendamisel.
