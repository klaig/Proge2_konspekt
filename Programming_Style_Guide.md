# Programmeerimisstiili Juhend

Hea programmeerimisstiil on oluline, et tagada koodi loetavus, hooldatavus ja ühtsus. See dokument kirjeldab programmeerimiskursuse raames nõutavaid programmeerimisstiili reegleid ja soovitusi Java keele näitel.

## Sisukord
- [Üldnõuded](#üldnõuded)
- [Vormindamisnõuded](#vormindamisnõuded)
- [Dokumenteerimise Standardid](#dokumenteerimise-standardid)
- [Muutujate ja Meetodite Nimetamine](#muutujate-ja-meetodite-nimetamine)
- [Koodistruktuuri Parimad Praktikad](#koodistruktuuri-parimad-praktikad)
- [Välised Allikad ja Tsiteerimine](#välised-allikad-ja-tsiteerimine)

## Üldnõuded

* **Platvormi sõltumatus**: Lahendused peavad töötama sõltumatult arenduskeskkonnast või operatsioonisüsteemist.
* **Standardteek**: Lubatud on kasutada ainult Java standardteeki (Java API).
* **Kasutajaliides**: Lahendusprogramm ei tohi kasutajaga interakteeruda; kui väljundit on vaja, tuleb see suunata standardväljundisse (`System.out`).
* **Klassiväljade piiramine**: Klassiväljasid (muutujaid `static` võtmesõnaga) ei tohiks kasutada.
* **Lõimede piiramine**: Mitme lõime kasutamine pole lubatud.
* **Java versioon**: Lahendusprogramm peab töötama Java versiooniga 17.

**NB!** Programmikoodile võidakse seada täiendavaid piiranguid. Näiteks: kogu kood peab olema ühes failis; kood ei tohi sisaldada `import` käsku, mõistet `java` jne. **Iga kodutöö puhul täpsusta, millised piirangud on programmi koodil.**

## Vormindamisnõuded

Java programm peab algama päisega (kommentaariplokina):

```java
/***********************************
 * Programmeerimine II. LTAT.03.007
 * 2024/2025 kevadsemester
 *
 * Kodutöö nr TODO
 * Teema: TODO
 *
 * Autor: TODO
 *
 **********************************/
```

### Koodi Vormindus

* **Taanded**: Kasuta järjepidevalt 4 tühikut või 1 tabulaatorit taande jaoks.
* **Sulud**: Avav sulg paikneb rea lõpus, sulgev sulg eraldi real, joondatud sama kaugele kui vastav avav konstruktsioon:

```java
if (tingimus) {
    // kood
} else {
    // kood
}
```

* **Rea pikkus**: Piira ridade pikkust, et need oleksid loetavad (tavaliselt 80-120 sümbolit).
* **Tühikud**: Kasuta tühikuid operaatorite ümber, komade järel ja sulgudele vahetult järgnevalt.

```java
// Hea
int summa = a + b;
func(a, b, c);

// Halb
int summa=a+b;
func(a,b,c);
```

* **Tühjad read**: Kasuta tühje ridu loogiliselt seotud koodiblokkide eraldamiseks.

## Dokumenteerimise Standardid

Igal meetodil (välja arvatud peameetodil) peab olema oma väline spetsifikatsioon: eesmärk, parameetrite kirjeldus ja tagastusväärtus. Väline spetsifikatsioon võib olla Javadoc stiilis (vahetult enne meetodit) või esitatakse tavatekstina, mis koosneb reakomenteerimisjadast meetodi alguses:

### Javadoc Stiil (eelistatud):

```java
/**
 * Leiab massiivi summat rekursiivselt.
 * @param a Antud massiiv.
 * @param n Antud massiivi algusosa pikkus.
 * @return Massiivi a algusosa elementide summa: a[0]+a[1]+...+a[n-1]
 */
static int summaRek(int[] a, int n) {
    // kood siia
}
```

### Tavateksti Stiil:

```java
static int summaRek(int[] a, int n) {
    // Eesmärk: Leiab massiivi summat rekursiivselt.
    // Antud: massiiv a ja algusosa pikkus n
    // Tulemus: Massiivi a algusosa elementide summa: a[0]+a[1]+...+a[n-1]
    
    // kood siia
}
```

### Kommenteerimise Põhimõtted

* **Meetodi Dokumentatsioon**: Dokumendi kõik avalikud meetodid.
* **Algoritmi Kommentaarid**: Lisa meetodi sees olulised kommentaarid, eriti need, mis aitavad mõista algoritmi ideed.
* **Keerulised Kohad**: Kommenteeri koodi keerukamaid osi või mitte-intuitiivseid lahendusi.
* **Väldi Liigset Kommenteerimist**: Ära kommenteeri ilmselgeid asju - eelistage koodi loetavust.

```java
// Hea kommentaar
// Rakendame Kadane'i algoritmi maksimaalse alamjärjendi summa leidmiseks
int jooksevSumma = 0;
int maksSumma = Integer.MIN_VALUE;

// Halb kommentaar
// Suurendame i-d ühe võrra
i++;
```

## Muutujate ja Meetodite Nimetamine

### Keele Kasutus

Eesti keel peab olema esmatähtis, sealhulgas muutujate ja meetodite nimed ning kommentaarid. Anglitsisme tuleks võimalusel vältida!

### Nimetamise Reeglid

* **Klassinimed**: Klassinimed kirjutatakse suure algustähega ning kasutades nn kaamelkirja (CamelCase): `KlassiNimi`.
* **Meetodinimed**: Meetodinimed algavad väikese tähega ning kasutavad samuti kaamelkirja: `meetodiNimi`.
* **Muutujate nimed**: Muutujate nimed algavad väikese tähega ning kasutavad kaamelkirja: `muutujaNimi`.
* **Konstantide nimed**: Konstantide nimed kirjutatakse LÄBIVA SUURTÄHEGA ning sõnad eraldatakse alakriipsuga: `KONSTANDI_NIMI`.

```java
public class MatemaatilisedFunktsioonid {
    private static final double PI_VÄÄRTUS = 3.14159;
    
    public static double arvutaRingiPindala(double raadius) {
        double pindala = PI_VÄÄRTUS * raadius * raadius;
        return pindala;
    }
}
```

### Nimetamise Head Tavad

* **Kirjeldavad nimed**: Vali nimed, mis kirjeldavad täpselt, mida muutuja, meetod või klass teeb.
* **Lühidus vs täpsus**: Eelistatud on lühikesed, kuid täpsed nimed. Kui täpsus nõuab pikemat nime, eelista täpsust.
* **Vältida lühendeid**: Väldi mitmetähenduslikke lühendeid, välja arvatud väga levinud lühendid (nt `max`, `min`).
* **Järjepidevus**: Kasuta järjepidevalt sama nimetamisstiili kogu koodi ulatuses.

```java
// Hea
int kliendiVanus;
boolean onTäisealine;
List<Toode> ostukorv;

// Halb
int x;
boolean check;
List<Toode> list1;
```

## Koodistruktuuri Parimad Praktikad

### Meetodite Ülesehitus

* **Üks Vastutus**: Iga meetod peaks täitma ühte konkreetset ülesannet.
* **Pikkus**: Meetodid peaksid olema võimalikult lühikesed. Pikad meetodid tuleks jagada väiksemateks alameetodideks.
* **Parameetrite Arv**: Piira parameetrite arvu (tavaliselt mitte rohkem kui 3-4).
* **Abstraktsioon**: Eralda erinevatele abstraktsioonitasemetele kuuluv kood eraldi meetoditesse.

### Klasside Ülesehitus

* **Loogika Eraldamine**: Eralda erinevad vastutusalad erinevatesse klassidesse.
* **Liides vs Implementatsioon**: Eralda avalik liides (API) selle implementatsioonist.
* **Kapseldamine**: Kasuta `private` välju ja paku ligipääsu getterite ja setterite kaudu, kui see on asjakohane.

### Koodi Korduvuse Vältimine (DRY - Don't Repeat Yourself)

* **Funktsioonide Abstraktsioon**: Abstrakteeri korduv kood funktsioonidesse.
* **Üldistamine**: Kirjuta üldistatud kood, mis töötab erinevate sisendite korral.
* **Konstantide Kasutamine**: Kasuta konstantide definitsioone korduvate väärtuste jaoks.

```java
// Halb - koodikordus
if (vanus < 18) {
    System.out.println("Liiga noor");
    return false;
}

if (vanus > 65) {
    System.out.println("Liiga vana");
    return false;
}

// Parem - abstraktsioon
boolean onSobivVanus = kontrolliVanus(vanus, 18, 65);
if (!onSobivVanus) {
    return false;
}

// Abifunktsioon
private boolean kontrolliVanus(int vanus, int miinimum, int maksimum) {
    if (vanus < miinimum) {
        System.out.println("Liiga noor");
        return false;
    }
    
    if (vanus > maksimum) {
        System.out.println("Liiga vana");
        return false;
    }
    
    return true;
}
```

## Välised Allikad ja Tsiteerimine

Kodutööde eesmärk on testida üliõpilase võimet luua ja kasutada algoritme ning siduda ja kinnistada kursusel õpitut. Kui kodutöö juhendis pole selgesõnaliselt lubatud kasutada koodi välistest allikatest, eeldatakse, et kodutöö lahendus on täielikult üliõpilase poolt kirjutatud ja pärineb kursusesisestest allikatest.

### Viitamine ja Tsiteerimine

Kui kasutad välist allikat (mis on selgesõnaliselt lubatud):

* **Viita Selgelt**: Lisa viide originaalallikale kommentaaris.
* **Kirjelda Muudatusi**: Selgita, milliseid muudatusi või kohandusi oled teinud.
* **Piira Kopeerimist**: Väldi suure koguse koodi kopeerimist - mõista ja kohandada, mitte kopeerida.

```java
/**
 * Implementatsioon põhineb allikal:
 * "Algorithms, 4th Edition" by Robert Sedgewick and Kevin Wayne, p. 123
 * https://algs4.cs.princeton.edu/22merge/
 * 
 * Kohandused:
 * - Muudetud massiiviindekseid Java 0-põhiseks
 * - Lisatud kontroll tühja massiivi jaoks
 */
```

### Akadeemiline Ausus

* **Iseseisvus**: Lahenda ülesanded iseseisvalt, kui pole teisiti määratud.
* **Teiste Töö Kasutamine**: Ära esita teiste tööd enda omana.
* **Koostöö**: Kui koostöö on lubatud, määratle selgelt oma panus.

Programmeerimisstiili järgmine aitab luua loetavat, hooldatavat ja professionaalset koodi. Need standardid ei ole mõeldud ainult kursuse läbimiseks, vaid peegeldavad ka häid tavasid tööstuses.
