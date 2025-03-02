# Andmestruktuurid

Andmestruktuurid on viisid andmete organiseerimiseks ja salvestamiseks nii, et nendele saab efektiivselt ligi pääseda ja neid modifitseerida. Sobilike andmestruktuuride valimine ja kasutamine on oluline osa algoritmide disainist ja efektiivsest programmeerimisest.

## Sisukord
- [Abstraktsed Andmetüübid](#abstraktsed-andmetüübid)
- [Massiivid ja Järjendid](#massiivid-ja-järjendid)
- [Maatriksid](#maatriksid)
- [Sõned](#sõned)
- [Kahendpuud](#kahendpuud)
- [Magasinid](#magasinid)
- [Järjekorrad](#järjekorrad)
- [Eelistusjärjekorrad](#eelistusjärjekorrad)
- [Praktilised Näited](#praktilised-näited)

## Abstraktsed Andmetüübid

**Abstraktne andmetüüp (AAT)** (ingl. _abstract data type_, ADT) on matemaatiline mudel andmetüüpide jaoks, kus tüüp on defineeritud selle käitumise (semantika) järgi kasutaja vaatenurgast. AAT defineerib võimalikud väärtused, operatsioonid ja käitumise, kuid ei spetsifitseeri, kuidas seda implementeerida.

Olulisemad abstraktsed andmetüübid:
- Magasin (stack)
- Järjekord (queue)
- Eelistusjärjekord (priority queue)
- Nimekiri (list)
- Hulk (set)
- Kaardistus (map)
- Puu (tree)
- Graaf (graph)

## Massiivid ja Järjendid

Massiiv (ingl. _array_) on üks põhilisemaid andmestruktuure, kus elementide kogum on salvestatud järjestikustes mäluasukohtades. Java-s on massiivid:
- Fikseeritud suurusega
- Indeksitega juurdepääsetavad (esimene element on indeksiga 0)
- Homogeensed (kõik elemendid on sama tüüpi)

### Massiivide Loomine

```java
// Massiivi deklareerimine
int[] arvud;

// Massiivi loomine kindla suurusega
arvud = new int[5];

// Massiivi deklareerimine ja algväärtustamine ühel real
int[] arvud2 = {1, 2, 3, 4, 5};

// Massiivi läbimine
for (int i = 0; i < arvud.length; i++) {
    System.out.println(arvud[i]);
}

// Massiivi läbimine foreach tsükliga
for (int arv : arvud2) {
    System.out.println(arv);
}
```

### Osajärjend ja Alamjärjend

- **Osajärjend (ingl. _subsequence_)**: Mittetühi järjend, mis on saadud lähtejärjendist elementide valimisel indeksi kasvamise järjekorras. Elemendid ei pea olema järjestikused.
- **Alamjärjend (ingl. _subarray_)**: Mittetühi järjend, mis on saadud järjendist järjestikuste elementide valimisel.

```
Näide: 
Järjend: [1, 2, 3, 7, 4, 5, 6]

Osajärjendid: [3, 7, 5], [2, 7, 5, 6] jne.
Alamjärjendid: [1, 2, 3], [3, 7, 4, 5] jne.
```

### Järjendite Operatsioonid

Järjenditega saab sooritada järgmisi põhilisi operatsioone:
- **Läbimine**: Kõigi elementide külastamine
- **Filtreerimine**: Tingimustele vastavate elementide valimine
- **Teisendamine**: Kõigi elementide muutmine mingi reegli järgi
- **Sorteerimine**: Elementide järjestamine mingi kriteeriumi alusel

### Java Collections Framework

Java standardteek sisaldab `Collections Framework` paketti, mis pakub dünaamilisi järjendeid ja muid andmestruktuure:

```java
import java.util.ArrayList;
import java.util.List;

// ArrayList - dünaamiline massiiv
List<String> nimed = new ArrayList<>();
nimed.add("Mari");     // Elemendi lisamine
nimed.add("Jaan");
nimed.remove(0);       // Elemendi eemaldamine indeksi järgi
nimed.get(0);          // Elemendile ligipääs indeksi järgi
nimed.size();          // Järjendi pikkus
nimed.contains("Jaan"); // Elemendi olemasolu kontroll
```

Järjendite töötlemisel arvesta alati indeksipiiridega ja kasuta abimeetodeid korduvate operatsioonide jaoks.

## Maatriksid

Maatriks (ingl. _matrix_) on kahedimensionaalne massiiv ridade ja veergudega.

### Maatriksi Loomine

```java
// Maatriksi deklareerimine ja loomine
int[][] maatriks = new int[3][3];

// Maatriksi algväärtustamine
int[][] maatriks2 = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Maatriksi läbimine
for (int i = 0; i < maatriks.length; i++) {
    for (int j = 0; j < maatriks[i].length; j++) {
        System.out.print(maatriks[i][j] + " ");
    }
    System.out.println();
}

// Maatriksi läbimine foreach tsükliga
for (int[] rida : maatriks2) {
    for (int element : rida) {
        System.out.print(element + " ");
    }
    System.out.println();
}
```

### Maatriksite Erivormid

- **Ruutmaatriks**: Ridade ja veergude arv on võrdne
- **Kolmnurkmaatriks**: Ülemine või alumine osa diagonaalist on täidetud nullidega
- **Toeplitzi maatriks**: Kõik diagonaalid on konstantsed

### Maatriksite Põhioperatsioonid

- **Transponeerimine**: Ridade ja veergude vahetamine
- **Pööramine**: Maatriksi pööramine mingi nurga võrra
- **Mustrite tuvastamine**: Teatud elementide konfiguratsioonide otsimine

```java
// Maatriksi transponeerimine
public static int[][] transponeeri(int[][] maatriks) {
    int m = maatriks.length;
    int n = maatriks[0].length;
    int[][] tulemus = new int[n][m];
    
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            tulemus[j][i] = maatriks[i][j];
        }
    }
    
    return tulemus;
}

// Maatriksi pööramine 90° päripäeva
public static int[][] pööraPäripäeva(int[][] maatriks) {
    int n = maatriks.length;
    int[][] tulemus = new int[n][n];
    
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            tulemus[j][n-1-i] = maatriks[i][j];
        }
    }
    
    return tulemus;
}
```

```
Näide: Maatriksi pööramine 90° päripäeva:
[1 2 3]    [7 4 1]
[4 5 6] -> [8 5 2]
[7 8 9]    [9 6 3]
```

Maatrikseid läbides kasuta kahekordset tsüklit või rekursiooni. Hoia meeles indeksite piiranguid ja ole eriti hoolikas töötamisel maatriksi servadega.

## Sõned

Sõne (ingl. _string_) on sümbolite järjend, millel on spetsiaalsed operatsioonid. Java-s on sõned `String` klassi isendid, mis on immutaablid (muutumatud).

### Sõnede Loomine ja Manipuleerimine

```java
// Sõne loomine
String s1 = "Tere";
String s2 = new String("Tere");

// Sõnede konkatenatsioon (liitmine)
String s3 = s1 + " " + "maailm";  // "Tere maailm"

// Sõne pikkus
int pikkus = s1.length();  // 4

// Sümbol indeksi järgi
char c = s1.charAt(0);  // 'T'

// Alamsõne
String alamsõne = s3.substring(0, 4);  // "Tere"

// Sõnede võrdlemine
boolean võrdne = s1.equals(s2);  // true
boolean võrdneIgnore = s1.equalsIgnoreCase("TERE");  // true

// Sõnede töötlemine
String lowerCase = s1.toLowerCase();  // "tere"
String upperCase = s1.toUpperCase();  // "TERE"
String trimmed = "  Tere  ".trim();   // "Tere"
String replaced = s1.replace('e', 'a');  // "Tara"
```

### Sõnede Erilised Omadused

- **Alamsõne (ingl. _substring_)**: Järjestikused sümbolid sõne sees
- **Heterogramm**: Sõne, kus kõik sümbolid on unikaalsed
- **Anagramm**: Sõned, mis erinevad ainult sümbolite järjestuse poolest

```
Näited:
- "programmeerimine" ei ole heterogramm (m ja e korduvad)
- "algoritm" on heterogramm (kõik sümbolid on unikaalsed)
- "kured" ja "ruked" on anagrammid
```

### Sõnede Töötlemine

```java
// Sõne sümbolhaaval läbimine
String sõne = "programmeerimine";
for (int i = 0; i < sõne.length(); i++) {
    System.out.println(sõne.charAt(i));
}

// Sõne sümbolite loendamine
public static boolean onHeterogramm(String s) {
    boolean[] nähtud = new boolean[256]; // Eeldame ASCII-sümboleid
    
    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        if (nähtud[c]) {
            return false; // Sümbol on juba esinenud
        }
        nähtud[c] = true;
    }
    
    return true;
}

// Palindroomi kontrollimine
public static boolean onPalindroom(String s) {
    int i = 0;
    int j = s.length() - 1;
    
    while (i < j) {
        if (s.charAt(i) != s.charAt(j)) {
            return false;
        }
        i++;
        j--;
    }
    
    return true;
}
```

Sõnede töötlemisel kasuta sümbolite loendamist või sümbolhaaval läbimist. Java String objektid on immutaablid, mis tähendab, et sõne muutmisel luuakse alati uus objekt.

## Kahendpuud

Kahendpuu (ingl. _binary tree_) on puu struktuur, kus igal tipul on maksimaalselt kaks alluvat (vasak ja parem alampuu).

### Kahendpuu Struktuur

```java
// Kahendpuu tipu klass
class KahendpuuTipp {
    int väärtus;
    KahendpuuTipp vasak;
    KahendpuuTipp parem;
    
    public KahendpuuTipp(int väärtus) {
        this.väärtus = väärtus;
        this.vasak = null;
        this.parem = null;
    }
}

// Kahendpuu näide
KahendpuuTipp juur = new KahendpuuTipp(1);
juur.vasak = new KahendpuuTipp(2);
juur.parem = new KahendpuuTipp(3);
juur.vasak.vasak = new KahendpuuTipp(4);
juur.vasak.parem = new KahendpuuTipp(5);
```

### Kahendpuu Omadused

- **Tipu sügavus (ingl. _node depth_)**: Tee pikkus juurest selle tipuni
- **Puu kõrgus (ingl. _tree height_)**: Tee pikkus juurest sügavaima leheni
- **Täistipp (ingl. _full node_)**: Tipp, millel on täpselt kaks alluvat
- **Täis puu (ingl. _full tree_)**: Puu, kus kõigil vahetippudel on kaks alluvat
- **Kompaktne puu (ingl. _complete tree_)**: Kõik tasemed on täidetud, välja arvatud võib-olla viimane

```
Näide:
    A
   / \
  B   C
 /     \
D       E

- Tipu D sügavus on 2
- Puu kõrgus on 2
- Täistipp on ainult A
```

### Kahendpuu Läbimised

Kahendpuu läbimiseks on erinevad järjestused:

- **Eesjärjestus (ingl. _pre-order_)**: juur -> vasak alampuu -> parem alampuu
- **Keskjärjestus (ingl. _in-order_)**: vasak alampuu -> juur -> parem alampuu
- **Lõppjärjestus (ingl. _post-order_)**: vasak alampuu -> parem alampuu -> juur
- **Tasemejärjestus (ingl. _level-order_)**: läbimõõt tasemete kaupa (kasutades järjekorda)

```java
// Eesjärjestus
public static void eesjärjestus(KahendpuuTipp juur) {
    if (juur == null) return;
    
    System.out.print(juur.väärtus + " ");  // Juur
    eesjärjestus(juur.vasak);               // Vasak alampuu
    eesjärjestus(juur.parem);               // Parem alampuu
}

// Keskjärjestus
public static void keskjärjestus(KahendpuuTipp juur) {
    if (juur == null) return;
    
    keskjärjestus(juur.vasak);              // Vasak alampuu
    System.out.print(juur.väärtus + " ");   // Juur
    keskjärjestus(juur.parem);              // Parem alampuu
}

// Lõppjärjestus
public static void lõppjärjestus(KahendpuuTipp juur) {
    if (juur == null) return;
    
    lõppjärjestus(juur.vasak);              // Vasak alampuu
    lõppjärjestus(juur.parem);              // Parem alampuu
    System.out.print(juur.väärtus + " ");   // Juur
}

// Tasemejärjestus
public static void tasemejärjestus(KahendpuuTipp juur) {
    if (juur == null) return;
    
    java.util.Queue<KahendpuuTipp> järjekord = new java.util.LinkedList<>();
    järjekord.add(juur);
    
    while (!järjekord.isEmpty()) {
        KahendpuuTipp tipp = järjekord.poll();
        System.out.print(tipp.väärtus + " ");
        
        if (tipp.vasak != null) {
            järjekord.add(tipp.vasak);
        }
        
        if (tipp.parem != null) {
            järjekord.add(tipp.parem);
        }
    }
}
```

Kahendpuud kasutatakse paljudes algoritmides ja andmestruktuurides, nagu binaarotsingu puud, kuhilad (heaps) ja Huffmani koodid.

## Magasinid

Magasin (ingl. _stack_) on kogum, mis järgib **Viimane-Sisse-Esimene-Välja (LIFO)** põhimõtet, st element, mis lisatakse viimasena, eemaldatakse esimesena.

### Magasini Põhioperatsioonid

1. **isEmpty()** - Tagastab tõeväärtuse, kas magasin on tühi
2. **push(element)** - Lisab elemendi magasini tippu
3. **pop()** - Eemaldab ja tagastab magasini tipust elemendi
4. **peek()** - Tagastab magasini tipu elemendi seda eemaldamata

### Magasini Implementatsioonid

#### Massiivipõhine Implementatsioon

```java
public class Magasin<T> {
    private Object[] elemendid;
    private int tipuIndeks;
    private static final int ALGSUUR = 10;
    
    public Magasin() {
        elemendid = new Object[ALGSUUR];
        tipuIndeks = -1;
    }
    
    public boolean isEmpty() {
        return tipuIndeks == -1;
    }
    
    public void push(T element) {
        if (tipuIndeks == elemendid.length - 1) {
            suurendaMassiivi();
        }
        elemendid[++tipuIndeks] = element;
    }
    
    @SuppressWarnings("unchecked")
    public T pop() {
        if (isEmpty()) {
            throw new IllegalStateException("Magasin on tühi");
        }
        return (T) elemendid[tipuIndeks--];
    }
    
    @SuppressWarnings("unchecked")
    public T peek() {
        if (isEmpty()) {
            throw new IllegalStateException("Magasin on tühi");
        }
        return (T) elemendid[tipuIndeks];
    }
    
    private void suurendaMassiivi() {
        Object[] uusMassiiv = new Object[elemendid.length * 2];
        System.arraycopy(elemendid, 0, uusMassiiv, 0, elemendid.length);
        elemendid = uusMassiiv;
    }
}
```

#### Ahelpõhine Implementatsioon

```java
public class Magasin<T> {
    private class Sõlm {
        T väärtus;
        Sõlm järgmine;
        
        Sõlm(T väärtus) {
            this.väärtus = väärtus;
            this.järgmine = null;
        }
    }
    
    private Sõlm tipp;
    
    public Magasin() {
        tipp = null;
    }
    
    public boolean isEmpty() {
        return tipp == null;
    }
    
    public void push(T element) {
        Sõlm uusSõlm = new Sõlm(element);
        uusSõlm.järgmine = tipp;
        tipp = uusSõlm;
    }
    
    public T pop() {
        if (isEmpty()) {
            throw new IllegalStateException("Magasin on tühi");
        }
        T väärtus = tipp.väärtus;
        tipp = tipp.järgmine;
        return väärtus;
    }
    
    public T peek() {
        if (isEmpty()) {
            throw new IllegalStateException("Magasin on tühi");
        }
        return tipp.väärtus;
    }
}
```

### Magasini Rakendused

1. **Funktsioonikutsete haldamine**
   - Funktsioonikutsete ja tagastuste haldamine (väljakutsete magasin)
   - Täitmise konteksti jälgimine rekursiooni ajal

2. **Avaldiste hindamine**
   - Infiksavaldiste teisendamine postfiksiks/prefiksiks
   - Postfiksavaldiste hindamine
   - Sulgude tasakaalu kontrollimine

3. **Tagurdamisalgoritmid**
   - Labürindi lahendamine
   - Mängu otsimispuu uurimine

4. **Tagasivõtmise (undo) mehhanismid rakendustes**
   - Tekstiredaktorid
   - Graafilise disaini tööriistad

## Järjekorrad

Järjekord (ingl. _queue_) on kogum, mis järgib **Esimene-Sisse-Esimene-Välja (FIFO)** põhimõtet, st element, mis lisatakse esimesena, eemaldatakse ka esimesena.

### Järjekorra Põhioperatsioonid

1. **isEmpty()** - Tagastab tõeväärtuse, kas järjekord on tühi
2. **enqueue(element)** või **add(element)** - Lisab elemendi järjekorra lõppu
3. **dequeue()** või **remove()** - Eemaldab ja tagastab järjekorra esimese elemendi
4. **peek()** või **element()** - Tagastab järjekorra esimese elemendi seda eemaldamata

### Järjekorra Implementatsioonid

#### Massiivipõhine Implementatsioon

```java
public class Järjekord<T> {
    private Object[] elemendid;
    private int algus, lõpp, suurus;
    private static final int ALGSUUR = 10;
    
    public Järjekord() {
        elemendid = new Object[ALGSUUR];
        algus = 0;
        lõpp = -1;
        suurus = 0;
    }
    
    public boolean isEmpty() {
        return suurus == 0;
    }
    
    public void enqueue(T element) {
        if (suurus == elemendid.length) {
            suurendaMassiivi();
        }
        lõpp = (lõpp + 1) % elemendid.length;
        elemendid[lõpp] = element;
        suurus++;
    }
    
    @SuppressWarnings("unchecked")
    public T dequeue() {
        if (isEmpty()) {
            throw new IllegalStateException("Järjekord on tühi");
        }
        T element = (T) elemendid[algus];
        algus = (algus + 1) % elemendid.length;
        suurus--;
        return element;
    }
    
    @SuppressWarnings("unchecked")
    public T peek() {
        if (isEmpty()) {
            throw new IllegalStateException("Järjekord on tühi");
        }
        return (T) elemendid[algus];
    }
    
    private void suurendaMassiivi() {
        Object[] uusMassiiv = new Object[elemendid.length * 2];
        
        for (int i = 0; i < suurus; i++) {
            uusMassiiv[i] = elemendid[(algus + i) % elemendid.length];
        }
        
        elemendid = uusMassiiv;
        algus = 0;
        lõpp = suurus - 1;
    }
}
```

#### Ahelpõhine Implementatsioon

```java
public class Järjekord<T> {
    private class Sõlm {
        T väärtus;
        Sõlm järgmine;
        
        Sõlm(T väärtus) {
            this.väärtus = väärtus;
            this.järgmine = null;
        }
    }
    
    private Sõlm algus, lõpp;
    
    public Järjekord() {
        algus = null;
        lõpp = null;
    }
    
    public boolean isEmpty() {
        return algus == null;
    }
    
    public void enqueue(T element) {
        Sõlm uusSõlm = new Sõlm(element);
        
        if (isEmpty()) {
            algus = uusSõlm;
        } else {
            lõpp.järgmine = uusSõlm;
        }
        
        lõpp = uusSõlm;
    }
    
    public T dequeue() {
        if (isEmpty()) {
            throw new IllegalStateException("Järjekord on tühi");
        }
        
        T väärtus = algus.väärtus;
        algus = algus.järgmine;
        
        if (algus == null) {
            lõpp = null;
        }
        
        return väärtus;
    }
    
    public T peek() {
        if (isEmpty()) {
            throw new IllegalStateException("Järjekord on tühi");
        }
        
        return algus.väärtus;
    }
}
```

### Järjekorra Rakendused

1. **Ressursside ajastamine**
   - CPU ülesannete ajastamine
   - Printeri töödejärjekord
   - Veebiserveris päringute käsitlemine

2. **Laiuti otsing graafides**
   - Tasemejärjestuses läbimine puudes
   - Lühima tee leidmine

3. **Puhverdamine**
   - I/O operatsioonid
   - Andmevoolu töötlemine

4. **Sõnumijärjekorrad hajutatud süsteemides**
   - Asünkroonne suhtlus
   - Koormuse tasakaalustamine

## Eelistusjärjekorrad

Eelistusjärjekord (ingl. _priority queue_) on järjekord, kus elemendid on seotud prioriteetidega ja elemendid eemaldatakse prioriteetide järjekorras.

### Eelistusjärjekorra Põhioperatsioonid

1. **isEmpty()** - Tagastab tõeväärtuse, kas eelistusjärjekord on tühi
2. **insert(element, prioriteet)** - Lisab elemendi antud prioriteediga
3. **extractMax()** / **extractMin()** - Eemaldab ja tagastab kõrgeima/madalaima prioriteediga elemendi
4. **peek()** - Tagastab kõrgeima/madalaima prioriteediga elementi seda eemaldamata

### Eelistusjärjekorra Implementatsioon

Java standardteegis on `PriorityQueue` klass, mis implementeerib minimaalse eelistusjärjekorra:

```java
import java.util.PriorityQueue;

public class EelistusjärjekorraDemo {
    public static void main(String[] args) {
        // Minimaalne eelistusjärjekord (vaikimisi)
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        
        pq.add(10);
        pq.add(5);
        pq.add(15);
        
        while (!pq.isEmpty()) {
            System.out.println(pq.poll()); // Väljastab: 5, 10, 15
        }
        
        // Kui tahame maksimaalset eelistusjärjekorda, saame muuta võrdlejat
        PriorityQueue<Integer> maxPq = new PriorityQueue<>((a, b) -> b - a);
        
        maxPq.add(10);
        maxPq.add(5);
        maxPq.add(15);
        
        while (!maxPq.isEmpty()) {
            System.out.println(maxPq.poll()); // Väljastab: 15, 10, 5
        }
    }
}
```

### Eelistusjärjekorra Rakendused

1. **Dijkstra lühima tee algoritm**
2. **A* otsingualgoritmid**
3. **Huffmani kodeerimine (andmete pakkimine)**
4. **Sündmustepõhised simulatsioonid**
5. **Ülesannete ajastamine prioriteedi alusel**

## Praktilised Näited

### Avaldiste Hindamine (Kasutades Magasini)

```java
// Postfiksavaldise hindamine
public static int hindaPostfiks(String avaldis) {
    java.util.Stack<Integer> magasin = new java.util.Stack<>();
    String[] elemendid = avaldis.split(" ");
    
    for (String element : elemendid) {
        if (element.matches("\\d+")) { // Kontrollib, kas on arv
            magasin.push(Integer.parseInt(element));
        } else { // Operaator
            int b = magasin.pop();
            int a = magasin.pop();
            
            switch (element) {
                case "+": magasin.push(a + b); break;
                case "-": magasin.push(a - b); break;
                case "*": magasin.push(a * b); break;
                case "/": magasin.push(a / b); break;
            }
        }
    }
    
    return magasin.pop();
}

// Näide:
// "5 3 + 2 *" = (5 + 3) * 2 = 16
```

### Tasakaalustatud Sulgude Kontroll

```java
public static boolean onTasakaalustatud(String avaldis) {
    java.util.Stack<Character> magasin = new java.util.Stack<>();
    String avamisSulud = "({[";
    String sulgemissulud = ")}]";
    
    for (int i = 0; i < avaldis.length(); i++) {
        char c = avaldis.charAt(i);
        
        if (avamisSulud.indexOf(c) != -1) {
            magasin.push(c);
        } else if (sulgemissulud.indexOf(c) != -1) {
            if (magasin.isEmpty()) {
                return false;
            }
            
            char laadisSulg = magasin.pop();
            if (avamisSulud.indexOf(laadisSulg) != sulgemissulud.indexOf(c)) {
                return false;
            }
        }
    }
    
    return magasin.isEmpty();
}

// Näited:
// "({[]})" -> true
// "({[})" -> false
```

### Laiuti Otsing (Kasutades Järjekorda)

```java
public static void laiutiOtsing(Map<String, List<String>> graaf, String algtipp) {
    java.util.Queue<String> järjekord = new java.util.LinkedList<>();
    Set<String> külastatud = new java.util.HashSet<>();
    
    järjekord.add(algtipp);
    külastatud.add(algtipp);
    
    while (!järjekord.isEmpty()) {
        String tipp = järjekord.poll();
        System.out.print(tipp + " ");
        
        for (String naaber : graaf.getOrDefault(tipp, new java.util.ArrayList<>())) {
            if (!külastatud.contains(naaber)) {
                külastatud.add(naaber);
                järjekord.add(naaber);
            }
        }
    }
}

// Näitlik graaf:
// A -> B, C
// B -> A, D, E
// C -> A, F
// D -> B
// E -> B, F
// F -> C, E
//
// Läbimine alates A: A B C D E F
```

Andmestruktuuride tundmine ja nende efektiivne kasutamine on oluline osa algoritmilisest mõtlemisest ja programmeerimisoskuste arendamisest. Õiget andmestruktuuri valides saad kirjutada efektiivsemat koodi ja lahendada probleeme optimaalsemal viisil.
