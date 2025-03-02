# Java Programmeerimise Alused

See dokument annab ülevaate Java programmeerimiskeele põhikontseptsioonidest, mis on aluseks algoritmilise mõtlemise ja programmeerimisoskuste arendamisele.

## Sisukord
- [Klassid ja Objektid](#klassid-ja-objektid)
- [Andmetüübid](#andmetüübid)
- [Muutujad ja Väljad](#muutujad-ja-väljad)
- [Meetodid](#meetodid)
- [Juhtstruktuurid](#juhtstruktuurid)
- [Pärimine ja Liidesed](#pärimine-ja-liidesed)
- [Erandite Käsitlemine](#erandite-käsitlemine)
- [Tüübiteisendused](#tüübiteisendused)
- [Standardpaketid](#standardpaketid)

## Klassid ja Objektid

### Klass (Class)
Klass on šabloon, mis määratleb objektide struktuuri, funktsionaalsuse ja muud omadused. Kõigil klassidel (välja arvatud `Object`) on ülemklass. Programmeerimine Javas koosneb peamiselt klasside loomisest.

```java
public class Tudeng {
    // Väljad (Fields)
    private String nimi;
    private int vanus;
    
    // Konstruktor (Constructor)
    public Tudeng(String nimi, int vanus) {
        this.nimi = nimi;
        this.vanus = vanus;
    }
    
    // Meetodid (Methods)
    public String getNimi() {
        return nimi;
    }
    
    public int getVanus() {
        return vanus;
    }
}
```

### Objekt (Object)
Objekt on klassi tüüpi isend, mis eksisteerib programmi täitmise ajal. Objekte luuakse klassist `new` operaatori abil.

```java
Tudeng tudeng1 = new Tudeng("Mari Mets", 22);
Tudeng tudeng2 = new Tudeng("Jaan Jõgi", 20);
```

### Isend (Instance)
Isend on konkreetne klassi tüüpi objekt, mis on loodud programmi täitmise ajal. Igal isendil on omad väljad.

### Isendiloome (Instantiation)
Klassi tüüpi objekti loomine, mida tehakse `new` operaatori abil. See protsess hõlmab mälu eraldamist ja konstruktori käivitamist.

```java
// Tudeng klassi isendi loomine
Tudeng uusTudeng = new Tudeng("Peeter Puu", 23);
```

## Andmetüübid

Java on staatiliselt tüübitud keel, mis tähendab, et iga muutuja tüüp määratakse programmi kompileerimise ajal ja see ei saa programmi täitmise ajal muutuda.

### Algtüübid (Primitive Types)

Java-s on kaheksa primitiivset andmetüüpi:

1. **byte**: 8-bitised täisarvud (-128 kuni 127)
2. **short**: 16-bitised täisarvud (-32768 kuni 32767)
3. **int**: 32-bitised täisarvud (-2147483648 kuni 2147483647)
4. **long**: 64-bitised täisarvud
5. **float**: 32-bitised ujukomaarvud (7 tähenduslikku numbrit)
6. **double**: 64-bitised ujukomaarvud (15 tähenduslikku numbrit)
7. **char**: 16-bitised Unicode sümbolid
8. **boolean**: `true` või `false` väärtused

```java
byte a = 100;
short b = 1000;
int c = 100000;
long d = 10000000000L;  // L-täht märgib, et tegemist on long-tüüpi konstandiga
float e = 3.14f;        // f-täht märgib, et tegemist on float-tüüpi konstandiga
double f = 3.14159265359;
char g = 'A';
boolean h = true;
```

### Osutitüübid (Reference Types)

Osutitüübid viitavad objektidele, mitte ei sisalda neid otse:

1. **Klassitüübid**: Viited nimetatud klassi isenditele
2. **Massiivitüübid**: Viited kindla elemendi tüübiga massiividele
3. **Spetsiaalne `null` viide**: Kuulub kõigile osutitüüpidele ja tähistab, et viide ei osuta ühelegi objektile

```java
String nimi = "Mari";         // String on klass
Tudeng t = new Tudeng("Jaan", 20);  // Tudeng on klass
int[] arvud = {1, 2, 3, 4, 5};      // massiiv
Tudeng x = null;              // viide, mis ei osuta ühelegi objektile
```

### void

Tühi tüüp, mida kasutatakse ainult meetodite tagastustüübina, mis ei tagasta väärtust.

```java
public void tervita() {
    System.out.println("Tere!");
    // ei tagasta väärtust
}
```

## Muutujad ja Väljad

### Muutuja (Variable)
Muutuja on nimetatud mäluasukoht kindla tüübiga, mis võib väärtusi salvestada.

```java
int arv = 42;
String sõne = "Tere";
```

### Väli (Field)
Väli on klassi kehas deklareeritud muutuja.

```java
public class Auto {
    private String mark;      // väli
    private String mudel;     // väli
    private int aasta;        // väli
}
```

### Isendiväli (Instance Field)
Väli, mis kuulub klassi isendile. Igal isendil on omad isendiväljad.

```java
public class Isik {
    private String nimi;      // isendiväli
    private int vanus;        // isendiväli
}
```

### Klassiväli (Class Field)
`static` modifikaatoriga väli, mis kuulub klassile endale. Kõik isendid jagavad sama klassivälja.

```java
public class Isik {
    private String nimi;
    private int vanus;
    private static int isikuteArv = 0;  // klassiväli
    
    public Isik(String nimi, int vanus) {
        this.nimi = nimi;
        this.vanus = vanus;
        isikuteArv++;  // iga uue isendi loomisel suurendame arvu
    }
    
    public static int getIsikuteArv() {
        return isikuteArv;
    }
}
```

### Lokaalmuutuja (Local Variable)
Plokis deklareeritud muutuja, mis on ligipääsetav ainult selles plokis.

```java
public void arvuta() {
    int x = 10;  // lokaalmuutuja
    if (x > 5) {
        int y = 20;  // lokaalmuutuja, nähtav ainult if-plokis
        System.out.println(x + y);
    }
    // y pole siin nähtav
}
```

### Muutuja Algväärtustaja (Variable Initializer)
Avaldis või massiivi algväärtustaja, mis seab muutuja algväärtuse.

```java
int a = 5;  // 5 on algväärtustaja
int[] arvud = {1, 2, 3, 4, 5};  // {1, 2, 3, 4, 5} on massiivi algväärtustaja
```

### Väike-Algväärtus (Default Value)
Väärtus, mis määratakse automaatselt väljadele, kui neid ei algväärtustata eksplitsiitselt.

- Numbrilised tüübid: `0` (`int`, `long`, `byte`, `short`, `float`, `double`)
- `boolean`: `false`
- `char`: `\u0000` (null char)
- Osutitüübid: `null`

```java
public class Test {
    private int arv;       // algväärtus on 0
    private boolean tõene; // algväärtus on false
    private String sõne;   // algväärtus on null
    
    public void näita() {
        System.out.println("arv = " + arv);
        System.out.println("tõene = " + tõene);
        System.out.println("sõne = " + sõne);
    }
}
```

## Meetodid

### Meetod (Method)
Meetod on klassi kehas kirjeldatud funktsioon, mis määratleb käitumise.

```java
public int liida(int a, int b) {
    return a + b;
}
```

### Isendimeetod (Instance Method)
Meetod, mis töötab klassi isendiga ja saab ligi isendiväljadele.

```java
public class Isik {
    private String nimi;
    
    public String getNimi() {  // isendimeetod
        return nimi;
    }
}
```

### Klassimeetod (Class Method)
`static` meetod, mis kuulub klassile endale, mitte üksikutele isenditele.

```java
public class Matemaatika {
    public static int ruut(int arv) {  // klassimeetod
        return arv * arv;
    }
}

// Klassimeetodit kutsutakse klassi nime kaudu
int tulemus = Matemaatika.ruut(5);  // tulemus = 25
```

### Konstruktor (Constructor)
Spetsiaalne protseduur, mida kasutatakse isendi loomisel väljade initsialiseerimiseks.

```java
public class Isik {
    private String nimi;
    private int vanus;
    
    // Konstruktor
    public Isik(String nimi, int vanus) {
        this.nimi = nimi;
        this.vanus = vanus;
    }
}
```

### Vaikekonstruktor (Default Constructor)
Parameetriteta konstruktor, mis genereeritakse automaatselt, kui konstruktoreid pole defineeritud.

```java
public class Isik {
    private String nimi;
    private int vanus;
    
    // Kui see klass ei defineeri ühtegi konstruktorit,
    // siis kompilaator loob vaikekonstruktori:
    // public Isik() { }
}
```

### Peameetod (Main Method)
Nõutav sisenemispunkt iseseisvate rakenduste jaoks signatuuriga `public static void main(String[] args)`.

```java
public class Programm {
    public static void main(String[] args) {
        System.out.println("Tere, maailm!");
    }
}
```

### Signatuur (Signature)
Meetodi nimi ja formaalsete parameetrite tüüpide loend.

```java
// Meetodi nimi: "liida"
// Parameetrite tüübid: (int, int)
// Signatuur: liida(int, int)
public int liida(int a, int b) {
    return a + b;
}
```

## Juhtstruktuurid

### Plokk (Block)
Lausete jada, mis on ümbritsetud loogeliste sulgudega `{}`.

```java
{
    int x = 10;
    System.out.println(x);
}
```

### Direktiiv (Statement)
Keelekonstruktsioon, mis kirjeldab algoritmilisi tegevusi.

```java
int x = 10;  // avaldisdirektiiv
if (x > 5) { }  // tingimusdirektiiv
```

### Avaldisdirektiiv (Expression Statement)
Avaldisest ja sellele järgnevast semikoolonist koosnev direktiiv.

```java
x = 10;  // omistamisavaldis
System.out.println("Tere");  // meetodi väljakutse
x++;  // suurendamisavaldis
```

### Tingimusdirektiiv (Conditional Statement)
`if-else` konstruktsioon, mis võimaldab tingimuslikku täitmist.

```java
if (x > 10) {
    System.out.println("x on suurem kui 10");
} else if (x > 5) {
    System.out.println("x on suurem kui 5, aga mitte suurem kui 10");
} else {
    System.out.println("x ei ole suurem kui 5");
}
```

### Lülitidirektiiv (Switch Statement)
Mitmel juhul põhinev valik.

```java
int päev = 3;
switch (päev) {
    case 1:
        System.out.println("Esmaspäev");
        break;
    case 2:
        System.out.println("Teisipäev");
        break;
    case 3:
        System.out.println("Kolmapäev");
        break;
    // ... muud päevad
    default:
        System.out.println("Vigane päev");
}
```

### Tsüklidirektiivid (Loop Statements)

#### Eelkontrolliga tsüklidirektiiv (While Loop)
Tsükkel, mis kontrollib tingimust enne keha täitmist.

```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

#### Järelkontrolliga tsüklidirektiiv (Do-While Loop)
Tsükkel, mis kontrollib tingimust pärast keha täitmist.

```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 5);
```

#### Üldtsüklidirektiiv (For Loop)
Üldine tsükkel, millel on initsialiseerimise, tingimuse ja iteratsiooni osad.

```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

### Katkestusdirektiiv (Break Statement)
Väljub tsüklist või switch-direktiivist.

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;  // lõpetab tsükli, kui i = 5
    }
    System.out.println(i);
}
```

### Jätkamisdirektiiv (Continue Statement)
Liigub tsükli järgmisele iteratsioonile.

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        continue;  // jätab i = 5 vahele ja jätkab i = 6
    }
    System.out.println(i);
}
```

### Naasmisdirektiiv (Return Statement)
Väljub meetodist, tagastades valikuliselt väärtuse.

```java
public int ruut(int arv) {
    return arv * arv;  // tagastab arvu ruudu ja lõpetab meetodi
}
```

## Pärimine ja Liidesed

### Pärimine (Inheritance)
Mehhanism, mis lisab automaatselt ülemklassi ja liidese liikme deklaratsioonid klassile.

```java
// Ülemklass
public class Isik {
    protected String nimi;
    protected int vanus;
    
    public Isik(String nimi, int vanus) {
        this.nimi = nimi;
        this.vanus = vanus;
    }
    
    public void info() {
        System.out.println("Nimi: " + nimi + ", Vanus: " + vanus);
    }
}

// Alamklass
public class Tudeng extends Isik {
    private String eriala;
    
    public Tudeng(String nimi, int vanus, String eriala) {
        super(nimi, vanus);  // kutsub ülemklassi konstruktorit
        this.eriala = eriala;
    }
    
    @Override
    public void info() {
        super.info();  // kutsub ülemklassi meetodit
        System.out.println("Eriala: " + eriala);
    }
}
```

### Liides (Interface)
Abstraktsete meetodite kogum, mida klassid peavad implementeerima.

```java
public interface Joonisfiguur {
    double pindala();
    double ümbermõõt();
}

public class Ring implements Joonisfiguur {
    private double raadius;
    
    public Ring(double raadius) {
        this.raadius = raadius;
    }
    
    @Override
    public double pindala() {
        return Math.PI * raadius * raadius;
    }
    
    @Override
    public double ümbermõõt() {
        return 2 * Math.PI * raadius;
    }
}
```

### Abstraktne klass (Abstract Class)
Klass, mis sisaldab vähemalt ühte abstraktset meetodit ja mida ei saa isendada.

```java
public abstract class Kujund {
    protected String nimi;
    
    public Kujund(String nimi) {
        this.nimi = nimi;
    }
    
    public String getNimi() {
        return nimi;
    }
    
    // Abstraktne meetod - alamklassid peavad seda implementeerima
    public abstract double pindala();
}

public class Ristkülik extends Kujund {
    private double pikkus;
    private double laius;
    
    public Ristkülik(double pikkus, double laius) {
        super("Ristkülik");
        this.pikkus = pikkus;
        this.laius = laius;
    }
    
    @Override
    public double pindala() {
        return pikkus * laius;
    }
}
```

### Abstraktne meetod (Abstract Method)
Meetodi deklaratsioon ilma implementatsioonita (kehata).

```java
public abstract class Kujund {
    // Abstraktne meetod
    public abstract double pindala();
}
```

### Ülekate (Overriding)
Päritud meetodi uue implementatsiooni pakkumine sama signatuuriga.

```java
public class Isik {
    public void tervita() {
        System.out.println("Tere!");
    }
}

public class Tudeng extends Isik {
    @Override
    public void tervita() {
        System.out.println("Tere, olen tudeng!");
    }
}
```

### Üledefineerimine (Overloading)
Mitme sama nimega, kuid erineva signatuuriga meetodi omamine klassis.

```java
public class Matemaatika {
    // Meetodi üledefineerimine erinevate parameetritega
    public int liida(int a, int b) {
        return a + b;
    }
    
    public double liida(double a, double b) {
        return a + b;
    }
    
    public int liida(int a, int b, int c) {
        return a + b + c;
    }
}
```

## Erandite Käsitlemine

### Erind (Exception)
Erisituatsioon, mis võib programmi täitmise ajal tekkida.

### Erindiklass (Exception Class)
Klass, mis pärineb `Exception` klassist paketis `java.lang`.

```java
public class MinuErind extends Exception {
    public MinuErind(String sõnum) {
        super(sõnum);
    }
}
```

### Katsendidirektiiv (Try Statement)
Struktuur, mis sisaldab try-plokki, catch-klausleid ja valikulist finally-klauslit.

```java
try {
    // Kood, mis võib tekitada erindi
    int a = 10 / 0;  // Tekitab ArithmeticException
} catch (ArithmeticException e) {
    // Käsitleb ArithmeticException erindi
    System.out.println("Aritmeetiline viga: " + e.getMessage());
} finally {
    // Täidetakse alati, sõltumata sellest, kas erind tekkis või mitte
    System.out.println("Finally plokk");
}
```

### Püünis (Catch Clause)
Kood, mis käsitleb teatud tüüpi erandit.

```java
try {
    int[] a = new int[5];
    a[10] = 50;  // Tekitab ArrayIndexOutOfBoundsException
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Massiivi indeks väljas: " + e.getMessage());
}
```

### Epiloog (Finally Clause)
Kood, mis täidetakse sõltumata sellest, kas erind tekkis või mitte.

```java
FileReader fr = null;
try {
    fr = new FileReader("fail.txt");
    // Faili lugemine...
} catch (IOException e) {
    System.out.println("Viga faili lugemisel: " + e.getMessage());
} finally {
    // Sulgeme faili alati, isegi kui tekkis erind
    try {
        if (fr != null) fr.close();
    } catch (IOException e) {
        System.out.println("Viga faili sulgemisel: " + e.getMessage());
    }
}
```

### Erindiheite direktiiv (Throw Statement)
Loob ja heidab erindi objekti.

```java
public void kontrolliVanus(int vanus) throws MinuErind {
    if (vanus < 0) {
        throw new MinuErind("Vanus ei saa olla negatiivne");
    }
    // Jätkab, kui vanus on korrektne
}
```

## Tüübiteisendused

### Teisendus (Conversion)
Väärtuse tüübi muutmine, võimalik, et muutes ka väärtust ennast.

### Laiendav primitiivteisendus (Widening Primitive Conversion)
Teisendus primitiivsete tüüpide vahel ilma informatsiooni kaotuseta (nt `int` -> `long`).

```java
int i = 100;
long l = i;  // laiendav teisendus int -> long, ei vaja eksplitsiitset teisendust
```

### Kitsendav primitiivteisendus (Narrowing Primitive Conversion)
Teisendus primitiivsete tüüpide vahel võimaliku informatsiooni kaotusega (nt `double` -> `int`).

```java
double d = 100.9;
int i = (int) d;  // kitsendav teisendus double -> int, nõuab eksplitsiitset teisendust
// i väärtus on 100, murdosa läheb kaduma
```

### Laiendav viiteteisendus (Widening Reference Conversion)
Teisendus viitetüüpide vahel (nt alamklass -> ülemklass).

```java
class Isik { }
class Tudeng extends Isik { }

Tudeng t = new Tudeng();
Isik i = t;  // laiendav teisendus Tudeng -> Isik, ei vaja eksplitsiitset teisendust
```

### Kitsendav viiteteisendus (Narrowing Reference Conversion)
Teisendus viitetüüpide vahel, mis nõuab täitmisaegset kontrolli (nt ülemklass -> alamklass).

```java
Isik i = new Tudeng();
Tudeng t = (Tudeng) i;  // kitsendav teisendus Isik -> Tudeng, nõuab eksplitsiitset teisendust
```

### String teisendus (String Conversion)
Väärtuse teisendamine stringiks.

```java
int i = 42;
String s = "Väärtus on: " + i;  // täisarv teisendatakse stringiks ja liidetakse
```

## Standardpaketid

### Standardpakett (Standard Package)
Paketid, mis on kaasatud Java põhidistributsiooni:

- **java.lang**: Standardsed keele võimalused (automaatselt imporditud)
- **java.io**: Sisend-väljund võimalused
- **java.util**: Utiliitklassid (nt kollektsioonid)
- **java.net**: Võrgu võimalused
- **java.awt**: Abstract Window Toolkit graafikaks
- **java.applet**: Appleti programmeerimise võimalused

```java
import java.util.ArrayList;  // Konkreetse klassi import
import java.io.*;            // Kõigi paketi klasside import

public class Programm {
    public static void main(String[] args) {
        ArrayList<String> nimekiri = new ArrayList<>();
        nimekiri.add("Esimene");
        nimekiri.add("Teine");
        
        System.out.println(nimekiri);  // java.lang on automaatselt imporditud
    }
}
```
