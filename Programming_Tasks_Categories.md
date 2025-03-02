# Programmeerimisülesannete Kategooriad

Programmeerimisülesanded võib jagada erinevatesse kategooriatesse vastavalt nende lahendusstrateegiaid nõudvatele mustritele ja struktuuridele. Selles dokumendis kirjeldame põhilisi programmeerimisülesannete kategooriaid koos näidete ja juhistega.

## Sisukord

- [Arvutusülesanded](#arvutusülesanded)
- [Järjendite Töötlemine](#järjendite-töötlemine)
- [Maatriksite Töötlemine](#maatriksite-töötlemine)
- [Rekursiivne Töötlemine](#rekursiivne-töötlemine)
- [Sõnede Töötlemine](#sõnede-töötlemine)
- [Kahendpuude Töötlemine](#kahendpuude-töötlemine)
- [Näiteülesanded ja Lahendused](#näiteülesanded-ja-lahendused)

## Arvutusülesanded

Arvutusülesanded (ingl. _computational tasks_) keskenduvad matemaatiliste arvutuste ja algoritmide rakendamisele, arvuteooria probleemidele ning loogilistele tingimusele ja avaldistele.

### Tüüpilised Probleemid

- Matemaatilised arvutused
- Arvuteooria probleemid (algar, SÜT, VÜK)
- Loogilised avaldised ja nende hindamine
- Funktsioonide implementeerimine

### Näide: Fibonacci Arvud

```java
/**
 * Arvutab Fibonacci jada n-nda liikme.
 * @param n Fibonacci arvu järjekorranumber (n >= 0)
 * @return Fibonacci jada n-s liige
 */
public static int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    
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

### Näide: Algarvu Kontroll

```java
/**
 * Kontrollib, kas antud arv on algarv.
 * @param n Kontrollitav arv (n > 1)
 * @return true, kui n on algarv, vastasel juhul false
 */
public static boolean onAlgarv(int n) {
    if (n <= 1) {
        return false;
    }
    if (n <= 3) {
        return true;
    }
    if (n % 2 == 0 || n % 3 == 0) {
        return false;
    }
    
    // Kõik algarvud on kujul 6k±1, v.a 2 ja 3
    for (int i = 5; i * i <= n; i += 6) {
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }
    
    return true;
}
```

### Juhised

- Keskendu valemite täpsele rakendamisele ja äärejuhtude käsitlemisele
- Analüüsi algoritmi ajakeerukust ja otsi optimeerimise võimalusi
- Tee kindlaks, kas saad kasutada dünaamilist programmeerimist või memoiseerimist korduvate arvutuste vältimiseks
- Testi lahendust erinevate sisenditega, eriti äärejuhtudega (0, negatiivsed arvud, suured arvud jne)

## Järjendite Töötlemine

Järjendite töötlemine (ingl. _sequence processing_) hõlmab operatsioone nagu järjendite läbimine, muutmine, uute järjendite loomine ja järjendites mustrite tuvastamine ning analüüs.

### Tüüpilised Probleemid

- Massiivide läbimine ja elemnetide otsimine
- Järjendite muutmine (filtreerimine, teisendamine)
- Alamjärjendite ja osajärjendite leidmine
- Mustrite tuvastamine järjendites
- Maksimum/miinimum elementide leidmine

### Näide: Maksimaalse Alamjärjendi Summa

```java
/**
 * Leiab maksimaalse summa järjestikuste elementide alamjärjendis (Kadane'i algoritm).
 * @param massiiv Sisendmassiiv
 * @return Maksimaalne alamjärjendi summa
 */
public static int maksimaalneSumma(int[] massiiv) {
    if (massiiv.length == 0) {
        return 0;
    }
    
    int maksSumma = massiiv[0];
    int jooksevSumma = massiiv[0];
    
    for (int i = 1; i < massiiv.length; i++) {
        // Leia kas praegune element alustab uut alamjärjendit
        // või lisandub jooksvale alamjärjendile
        jooksevSumma = Math.max(massiiv[i], jooksevSumma + massiiv[i]);
        
        // Uuenda maksimaalset summat
        maksSumma = Math.max(maksSumma, jooksevSumma);
    }
    
    return maksSumma;
}
```

Näide: massiiva `[−2, 1, −3, 4, −1, 2, 1, −5, 4]` korral on vastus `6` (alamjärjend `[4, −1, 2, 1]`).

### Näide: Osajärjendi ja Alamjärjendi Genereerimine

```java
/**
 * Leiab kõik osajärjendid (mitte tingimata järjestikused elemendid).
 * @param massiiv Sisendmassiiv
 * @return Kõik osajärjendid
 */
public static List<List<Integer>> osajärjendid(int[] massiiv) {
    List<List<Integer>> tulemus = new ArrayList<>();
    genereeriOsajärjendid(massiiv, 0, new ArrayList<>(), tulemus);
    return tulemus;
}

private static void genereeriOsajärjendid(int[] massiiv, int indeks, List<Integer> praegune, List<List<Integer>> tulemus) {
    if (indeks == massiiv.length) {
        if (!praegune.isEmpty()) {
            tulemus.add(new ArrayList<>(praegune));
        }
        return;
    }
    
    // Jäta praegune element vahele
    genereeriOsajärjendid(massiiv, indeks + 1, praegune, tulemus);
    
    // Lisa praegune element
    praegune.add(massiiv[indeks]);
    genereeriOsajärjendid(massiiv, indeks + 1, praegune, tulemus);
    
    // Taasta praegune list
    praegune.remove(praegune.size() - 1);
}

/**
 * Leiab kõik alamjärjendid (järjestikused elemendid).
 * @param massiiv Sisendmassiiv
 * @return Kõik alamjärjendid
 */
public static List<List<Integer>> alamjärjendid(int[] massiiv) {
    List<List<Integer>> tulemus = new ArrayList<>();
    
    for (int algus = 0; algus < massiiv.length; algus++) {
        for (int lõpp = algus; lõpp < massiiv.length; lõpp++) {
            List<Integer> alamjärjend = new ArrayList<>();
            for (int i = algus; i <= lõpp; i++) {
                alamjärjend.add(massiiv[i]);
            }
            tulemus.add(alamjärjend);
        }
    }
    
    return tulemus;
}
```

### Juhised

- Kasuta tsükleid järjendite läbimiseks
- Kasuta abimassive või -andmestruktuure andmete salvestamiseks
- Arvesta alati indeksipiiridega, et vältida piiridest väljumist
- Optimeeri oma lahendust, vähendades läbimiste arvu või kasutades täiendavat mälu

## Maatriksite Töötlemine

Maatriksite töötlemine (ingl. _matrix processing_) hõlmab mustrite joonistamist, läbimise algoritme, teisendusi ja maatriksite loomist.

### Tüüpilised Probleemid

- Maatriksites mustrite joonistamine
- Maatriksi läbimise algoritmid (ridade/veergude kaupa, diagonaalselt)
- Maatriksite teisendused (pööramine, peegeldamine, transponeerimine)
- Maatriksite loomine kindlate mustrite alusel

### Näide: Maatriksi 90° Pööramine

```java
/**
 * Pöörab maatriksit 90 kraadi päripäeva.
 * @param maatriks Sisendmaatriks
 * @return Pööratud maatriks
 */
public static int[][] pööraMaatriks90(int[][] maatriks) {
    int n = maatriks.length;
    int[][] tulemus = new int[n][n];
    
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            tulemus[j][n - 1 - i] = maatriks[i][j];
        }
    }
    
    return tulemus;
}
```

Näide:
```
[1 2 3]    [7 4 1]
[4 5 6] -> [8 5 2]
[7 8 9]    [9 6 3]
```

### Näide: Spiraalse Maatriksi Loomine

```java
/**
 * Loob spiraalselt täidetud maatriksi.
 * @param n Maatriksi suurus
 * @return Spiraalse mustriga maatriks
 */
public static int[][] looSpiraalneMaatriks(int n) {
    int[][] maatriks = new int[n][n];
    
    int väärtus = 1;
    int ülemine = 0, alumine = n - 1;
    int vasak = 0, parem = n - 1;
    
    while (väärtus <= n * n) {
        // Ülemine rida
        for (int j = vasak; j <= parem; j++) {
            maatriks[ülemine][j] = väärtus++;
        }
        ülemine++;
        
        // Parem veerg
        for (int i = ülemine; i <= alumine; i++) {
            maatriks[i][parem] = väärtus++;
        }
        parem--;
        
        // Alumine rida
        if (ülemine <= alumine) {
            for (int j = parem; j >= vasak; j--) {
                maatriks[alumine][j] = väärtus++;
            }
            alumine--;
        }
        
        // Vasak veerg
        if (vasak <= parem) {
            for (int i = alumine; i >= ülemine; i--) {
                maatriks[i][vasak] = väärtus++;
            }
            vasak++;
        }
    }
    
    return maatriks;
}
```

### Juhised

- Maatriksi läbimisel arvesta alati indeksite piiridega
- Kasuta kahekordset tsüklit ridade ja veergude läbimiseks
- Joonista keerulisemad mustrid paberile, et mõista vajalikke indeksi manipulatsioone
- Pööra tähelepanu äärejuhtudele (tühi maatriks, üheelemendiline maatriks)

## Rekursiivne Töötlemine

Rekursiivne töötlemine (ingl. _recursive processing_) hõlmab probleeme, mis on lahendatavad rekursiivsete algoritmidega, kus funktsioon kutsub iseennast välja.

### Tüüpilised Probleemid

- Binaarse rekursiooni mustrid
- Rekursiivsete variantide loetlemine 
- Rekursiivsed puu läbimised
- Sõltuvad rekursiooni harud

### Näide: Fibonacci Rekursiivselt

```java
/**
 * Arvutab Fibonacci arvu rekursiivselt (ebaefektiivne lähenemine).
 * @param n Arvu järjekorranumber
 * @return n-is Fibonacci arv
 */
public static int fibonacciRek(int n) {
    if (n <= 1) {
        return n;
    }
    return fibonacciRek(n - 1) + fibonacciRek(n - 2);
}

/**
 * Arvutab Fibonacci arvu rekursiivselt memoiseerimisega (efektiivne).
 * @param n Arvu järjekorranumber
 * @param memo Meeldejätmise massiiv
 * @return n-is Fibonacci arv
 */
public static int fibonacciMemo(int n, Integer[] memo) {
    if (memo[n] != null) {
        return memo[n];
    }
    
    if (n <= 1) {
        memo[n] = n;
    } else {
        memo[n] = fibonacciMemo(n - 1, memo) + fibonacciMemo(n - 2, memo);
    }
    
    return memo[n];
}
```

### Näide: Faktoriaal Rekursiivselt

```java
/**
 * Arvutab faktoriaali rekursiivselt.
 * @param n Arv, mille faktoriaal arvutatakse
 * @return n! (n faktoriaal)
 */
public static int faktoriaalRek(int n) {
    if (n <= 1) {
        return 1;
    }
    return n * faktoriaalRek(n - 1);
}
```

### Juhised

- Määratle alati selge baasjuht rekursiooni lõpetamiseks
- Jälgi, et rekursiooni sügavus ei muutuks liiga suureks (stack overflow)
- Keerulisemate probleemide korral joonista rekursioonipuu mõistmiseks
- Kaalu memoiseerimine (tulemuste meelespidamine), et vältida korduvaid arvutusi

## Sõnede Töötlemine

Sõnede töötlemine (ingl. _string processing_) hõlmab probleeme, mis on seotud tekstide otsimise, manipuleerimise ja analüüsimisega.

### Tüüpilised Probleemid

- Sõnedes otsimine ja mustrite sobitamine
- Sõnede loomine ja teisendamine
- Teksti töötlemine ja parsimine
- Rekursiivne sõnede manipuleerimine

### Näide: Palindroomi Kontrollimine

```java
/**
 * Kontrollib, kas sõne on palindroom.
 * @param sõne Kontrollitav sõne
 * @return true, kui sõne on palindroom, vastasel juhul false
 */
public static boolean onPalindroom(String sõne) {
    int algus = 0;
    int lõpp = sõne.length() - 1;
    
    while (algus < lõpp) {
        // Ignoreeri tühikuid ja suur/väike tähtede erinevust
        while (algus < lõpp && !Character.isLetterOrDigit(sõne.charAt(algus))) {
            algus++;
        }
        while (algus < lõpp && !Character.isLetterOrDigit(sõne.charAt(lõpp))) {
            lõpp--;
        }
        
        if (Character.toLowerCase(sõne.charAt(algus)) != Character.toLowerCase(sõne.charAt(lõpp))) {
            return false;
        }
        
        algus++;
        lõpp--;
    }
    
    return true;
}
```

Näide: `"kasuema amesuak"` on palindroom.

### Näide: Anagrammide Kontroll

```java
/**
 * Kontrollib, kas kaks sõnet on anagrammid.
 * @param s1 Esimene sõne
 * @param s2 Teine sõne
 * @return true, kui sõned on anagrammid, vastasel juhul false
 */
public static boolean onAnagrammid(String s1, String s2) {
    // Eemalda tühikud ja muuda väiketähtedeks
    s1 = s1.replaceAll("\\s", "").toLowerCase();
    s2 = s2.replaceAll("\\s", "").toLowerCase();
    
    // Kui pikkused ei ole võrdsed, ei ole anagramm
    if (s1.length() != s2.length()) {
        return false;
    }
    
    // Loenda tähti
    int[] loendur = new int[256]; // Eeldame ASCII-d
    
    for (int i = 0; i < s1.length(); i++) {
        loendur[s1.charAt(i)]++;
        loendur[s2.charAt(i)]--;
    }
    
    // Kontrolli, kas kõik loenduri väärtused on 0
    for (int count : loendur) {
        if (count != 0) {
            return false;
        }
    }
    
    return true;
}
```

Näide: `"kured"` ja `"ruked"` on anagrammid.

### Juhised

- Sõnede töötlemisel kasuta sõne indekseid või alamstringide meetodeid
- Arvesta, et String on Java-s immutaabel (muutumatu), seega sõne muutmisel luuakse alati uus objekt
- Kasuta sümbolite loendamist või sümbolhaaval läbimist tuvastamisülesannetes
- Jälgi äärejuhte: tühi sõne, ühetäheline sõne, ainult tühikud

## Kahendpuude Töötlemine

Kahendpuude töötlemine (ingl. _binary tree processing_) hõlmab puu läbimise, muutmise, loomise algoritme ja puu omaduste analüüsi.

### Tüüpilised Probleemid

- Puu läbimise algoritmid (eesjärjestuses, keskjärjestuses, järeljärjestuses, tasemete kaupa)
- Puu muutmise tehnikad (lisamine, eemaldamine, tasakaalustamine)
- Puu loomine ja konstrueerimine
- Puu omaduste analüüs (kõrgus, laiendus, sümmeetria)

### Näide: Kahendpuu Läbimine

```java
class Tipp {
    int väärtus;
    Tipp vasak;
    Tipp parem;
    
    public Tipp(int väärtus) {
        this.väärtus = väärtus;
        this.vasak = null;
        this.parem = null;
    }
}

/**
 * Läbib puu eesjärjestuses (juur -> vasak -> parem).
 * @param juur Puu juur
 */
public static void eesjärjestus(Tipp juur) {
    if (juur == null) {
        return;
    }
    
    System.out.print(juur.väärtus + " ");  // Töötle juur
    eesjärjestus(juur.vasak);               // Läbi vasak alampu
    eesjärjestus(juur.parem);               // Läbi parem alampu
}

/**
 * Läbib puu keskjärjestuses (vasak -> juur -> parem).
 * @param juur Puu juur
 */
public static void keskjärjestus(Tipp juur) {
    if (juur == null) {
        return;
    }
    
    keskjärjestus(juur.vasak);              // Läbi vasak alampu
    System.out.print(juur.väärtus + " ");   // Töötle juur
    keskjärjestus(juur.parem);              // Läbi parem alampu
}

/**
 * Läbib puu järeljärjestuses (vasak -> parem -> juur).
 * @param juur Puu juur
 */
public static void järeljärjestus(Tipp juur) {
    if (juur == null) {
        return;
    }
    
    järeljärjestus(juur.vasak);             // Läbi vasak alampu
    järeljärjestus(juur.parem);             // Läbi parem alampu
    System.out.print(juur.väärtus + " ");   // Töötle juur
}

/**
 * Läbib puu tasemete kaupa (laiuti otsing).
 * @param juur Puu juur
 */
public static void tasemeteKaupa(Tipp juur) {
    if (juur == null) {
        return;
    }
    
    java.util.Queue<Tipp> järjekord = new java.util.LinkedList<>();
    järjekord.add(juur);
    
    while (!järjekord.isEmpty()) {
        Tipp praegune = järjekord.poll();
        System.out.print(praegune.väärtus + " ");
        
        if (praegune.vasak != null) {
            järjekord.add(praegune.vasak);
        }
        if (praegune.parem != null) {
            järjekord.add(praegune.parem);
        }
    }
}
```

### Näide: Kahendpuu Kõrguse Leidmine

```java
/**
 * Leiab kahendpuu kõrguse.
 * @param juur Puu juur
 * @return Puu kõrgus
 */
public static int puuKõrgus(Tipp juur) {
    if (juur == null) {
        return 0;
    }
    
    int vasakKõrgus = puuKõrgus(juur.vasak);
    int paremKõrgus = puuKõrgus(juur.parem);
    
    return Math.max(vasakKõrgus, paremKõrgus) + 1;
}
```

### Juhised

- Puudega töötamisel määratle selge andmestruktuur tipu kirjeldamiseks
- Kasuta rekursiooni puude läbimiseks
- Jaga keerulisemad ülesanded alamülesanneteks, mis lahendatakse vasaku ja parema alampu kaudu
- Arvesta erinevate äärejuhtudega: tühi puu, üksik tipp, asymmeetriline puu

## Näiteülesanded ja Lahendused

### Ülesanne 1: Paarisarvude Summa

**Probleem**: Leia massiivi kõigi paarisarvude summa.

**Kategooria**: Järjendite töötlemine

**Lahendus**:
```java
public static int paarisarvudeSumma(int[] massiiv) {
    int summa = 0;
    
    for (int arv : massiiv) {
        if (arv % 2 == 0) {
            summa += arv;
        }
    }
    
    return summa;
}
```

### Ülesanne 2: Maatriksi Transponeerimine

**Probleem**: Transponeeri antud maatriks (ridade ja veergude vahetamine).

**Kategooria**: Maatriksite töötlemine

**Lahendus**:
```java
public static int[][] transponeeritud(int[][] maatriks) {
    int n = maatriks.length;
    int m = maatriks[0].length;
    
    int[][] tulemus = new int[m][n];
    
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            tulemus[j][i] = maatriks[i][j];
        }
    }
    
    return tulemus;
}
```

### Ülesanne 3: Sõne Ümberpööramine

**Probleem**: Pööra ümber antud sõne.

**Kategooria**: Sõnede töötlemine

**Lahendus**:
```java
public static String pööratudSõne(String sõne) {
    char[] tähed = sõne.toCharArray();
    int algus = 0;
    int lõpp = tähed.length - 1;
    
    while (algus < lõpp) {
        // Vaheta tähed
        char temp = tähed[algus];
        tähed[algus] = tähed[lõpp];
        tähed[lõpp] = temp;
        
        algus++;
        lõpp--;
    }
    
    return new String(tähed);
}
```

### Ülesanne 4: Faktoriaal Rekursiivselt

**Probleem**: Arvuta faktoriaal rekursiivselt.

**Kategooria**: Rekursiivne töötlemine

**Lahendus**:
```java
public static int faktoriaal(int n) {
    // Baasjuht
    if (n <= 1) {
        return 1;
    }
    
    // Rekursiivne samm
    return n * faktoriaal(n - 1);
}
```

### Ülesanne 5: Kahendpuu Lehe Arv

**Probleem**: Leia kahendpuu lehtede arv.

**Kategooria**: Kahendpuude töötlemine

**Lahendus**:
```java
public static int lehedeArv(Tipp juur) {
    // Baasjuht: tühi puu
    if (juur == null) {
        return 0;
    }
    
    // Baasjuht: leht
    if (juur.vasak == null && juur.parem == null) {
        return 1;
    }
    
    // Rekursiivne samm
    return lehedeArv(juur.vasak) + lehedeArv(juur.parem);
}
```

Nende kategooriate ja näidetega saad paremini mõista erinevate programmeerimisülesannete olemust ning valida sobivaima lähenemisviisi iga probleemi lahendamiseks.
