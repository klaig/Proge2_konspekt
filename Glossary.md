# Programmeerimise Terminoloogia Sõnastik

See sõnastik sisaldab programmeerimises kasutatavaid termineid inglise ja eesti keeles. Terminid on grupeeritud kategooriate järgi, mis aitab neid paremini konteksti asetada.

## Sisukord
- [Objektorienteeritud Programmeerimine](#objektorienteeritud-programmeerimine)
- [Andmetüübid ja Muutujad](#andmetüübid-ja-muutujad)
- [Juhtstruktuurid](#juhtstruktuurid)
- [Andmestruktuurid](#andmestruktuurid)
- [Algoritmid ja Probleemilahendus](#algoritmid-ja-probleemilahendus)
- [Rekursioon](#rekursioon)
- [Ajakeerukus](#ajakeerukus)
- [Erandite Käsitlemine](#erandite-käsitlemine)
- [Üldised Programmeerimisterminid](#üldised-programmeerimisterminid)

## Objektorienteeritud Programmeerimine

| Inglise keeles | Eesti keeles | Selgitus |
|----------------|--------------|----------|
| Class | Klass | Šabloon, mis määratleb objektide struktuuri, funktsionaalsuse ja muud omadused |
| Object | Objekt | Klassi tüüpi objekt, mis eksisteerib programmi töö ajal |
| Instance | Isend | Konkreetne objekti näide klassi tüübist |
| Instantiation | Isendiloome | Klassi tüüpi objekti loomine, tehakse `new` operaatoriga |
| Inheritance | Pärimine | Mehhanism, mis lisab automaatselt ülemklassi ja liidese liikme deklaratsioonid klassile |
| Interface | Liides | Abstraktsete meetodite kogum, mida klassid peavad implementeerima |
| Abstract class | Abstraktne klass | Klass, mis sisaldab vähemalt ühte abstraktset meetodit ja mida ei saa isendada |
| Abstract method | Abstraktne meetod | Meetodi deklaratsioon ilma implementatsioonita (kehata) |
| Overriding | Ülekate | Päritud meetodi uue implementatsiooni pakkumine sama signatuuriga |
| Overloading | Üledefineerimine | Mitme sama nimega, kuid erineva signatuuriga meetodi omamine klassis |
| Constructor | Konstruktor | Spetsiaalne protseduur, mida kasutatakse isendi loomisel väljade initsialiseerimiseks |
| Default constructor | Vaikekonstruktor | Parameetriteta konstruktor, mis genereeritakse automaatselt, kui konstruktoreid pole defineeritud |

## Andmetüübid ja Muutujad

| Inglise keeles | Eesti keeles | Selgitus |
|----------------|--------------|----------|
| Primitive type | Algtüüp | Javas on 8 primitiivset tüüpi: byte, short, int, long, float, double, char, boolean |
| Reference type | Osutitüüp | Viitab klassi isendile, massiivile või spetsiaalsele `null` viitele |
| Variable | Muutuja | Nimetatud mäluasukoht kindla tüübiga, mis saab väärtusi salvestada |
| Field | Väli | Klassi kehas deklareeritud muutuja |
| Instance field | Isendiväli | Väli, mis kuulub klassi isendile |
| Class field | Klassiväli | `static` modifikaatoriga väli, mis kuulub klassile endale |
| Local variable | Lokaalmuutuja | Plokis deklareeritud muutuja, ligipääsetav ainult selles plokis |
| Variable initializer | Muutuja algväärtustaja | Avaldis või massiivi algväärtustaja, mis seab muutuja algväärtuse |
| Default value | Väike-algväärtus | Väärtus, mis määratakse automaatselt muutuja loomisel (nt `0` numbrilistele tüüpidele, `null` viitetüüpidele) |
| Widening primitive conversion | Laiendav primitiivteisendus | Teisendus primitiivsete tüüpide vahel ilma informatsiooni kaotuseta |
| Narrowing primitive conversion | Kitsendav primitiivteisendus | Teisendus primitiivsete tüüpide vahel võimaliku informatsiooni kaotusega |

## Juhtstruktuurid

| Inglise keeles | Eesti keeles | Selgitus |
|----------------|--------------|----------|
| Block | Plokk | Lausete jada, mis on ümbritsetud loogeliste sulgudega `{}` |
| Statement | Direktiiv | Keelekonstruktsioon, mis kirjeldab algoritmilisi tegevusi |
| Expression statement | Avaldisdirektiiv | Avaldisest ja sellele järgnevast semikoolonist koosnev direktiiv |
| Conditional statement | Tingimusdirektiiv | `if-else` konstruktsioon |
| Switch statement | Lülitidirektiiv | Valik, mis põhineb mitmel juhul |
| While loop | Eelkontrolliga tsüklidirektiiv | Tsükkel, mis kontrollib tingimust enne keha täitmist |
| Do-while loop | Järelkontrolliga tsüklidirektiiv | Tsükkel, mis kontrollib tingimust pärast keha täitmist |
| For loop | Üldtsüklidirektiiv | Üldine tsükkel, millel on initsialiseerimise, tingimuse ja iteratsiooni osad |
| Break statement | Katkestusdirektiiv | Väljub tsüklist või switch-direktiivist |
| Continue statement | Jätkamisdirektiiv | Liigub tsükli järgmisele iteratsioonile |
| Return statement | Naasmisdirektiiv | Väljub meetodist, tagastades valikuliselt väärtuse |

## Andmestruktuurid

| Inglise keeles | Eesti keeles | Selgitus |
|----------------|--------------|----------|
| Array | Massiiv | Sama tüüpi muutujate kogum indekseeritud juurdepääsuga |
| Array element | Massiivi element | Üksik element massiivis |
| Array creation | Massiiviloome | Massiivobjekti loomine kasutades `new` operaatorit |
| Array initializer | Massiivialgati | Struktuur, mis määrab massiivi algsed väärtused |
| Multidimensional array | Mitmemõõtmeline massiiv | Massiiv, mille elemendid on samuti massiivid |
| List | Järjend | Andmestruktuur, mis säilitab elementide järjestust |
| Stack | Magasin | Andmestruktuur, mis järgib LIFO (viimane-sisse-esimene-välja) põhimõtet |
| Queue | Järjekord | Andmestruktuur, mis järgib FIFO (esimene-sisse-esimene-välja) põhimõtet |
| Priority Queue | Eelistusjärjekord | Järjekord, kus elemendid on järjestatud prioriteedi järgi |
| Binary Tree | Kahendpuu | Puu, milles igal tipul on maksimaalselt kaks alluvat |
| Matrix | Maatriks | Kahedimensionaalne massiiv ridade ja veergudega |
| String | Sõne | Sümbolite jada, millel on erilised operatsioonid |
| Subsequence | Osajärjend | Mittetühi järjend, mis on saadud lähtejärjendist elementide valimisel indeksi kasvamise järjekorras |
| Subarray | Alamjärjend | Mittetühi järjend, mis on saadud järjendist järjestikuste elementide valimisel |
| Substring | Alamsõne | Järjestikused sümbolid sõne sees |
| Heterogram | Heterogramm | Sõne, kus kõik sümbolid on unikaalsed |
| Anagram | Anagramm | Sõned, mis erinevad ainult sümbolite järjestuse poolest |

## Algoritmid ja Probleemilahendus

| Inglise keeles | Eesti keeles | Selgitus |
|----------------|--------------|----------|
| Algorithm | Algoritm | Eeskirjade kogum, mis lahendab teatud probleemi |
| Complexity | Keerukus | Algoritmi ressursikasutuse mõõt |
| Divide and conquer | Jaga ja valitse | Strateegia, mis jagab probleemi väiksemateks alamprobleemideks |
| Dynamic programming | Dünaamiline programmeerimine | Tehnika, mis kasutab alamprobleemide lahenduste meelde jätmist |
| Greedy algorithm | Ahne algoritm | Algoritm, mis teeb igal sammul lokaalselt optimaalse valiku |
| Backtracking | Tagurdamine | Algoritmiline tehnika, mis ehitab lahendusi ja "tagurdab", kui lahendus ei sobi |
| Exhaustive search | Ammendav otsing | Kõigi võimalike lahenduste süstemaatiline läbivaatamine |
| Binary search | Kahendotsing | Otsimisalgoritm sorteeritud järjendites |
| Sorting algorithm | Sorteerimisalgoritm | Algoritm, mis järjestab elemendid |
| Merge sort | Liitmismeetod | Jaga-ja-valitse sorteerimisalgoritm |

## Rekursioon

| Inglise keeles | Eesti keeles | Selgitus |
|----------------|--------------|----------|
| Recursion | Rekursioon | Tehnika, kus funktsioon kutsub iseennast välja alamprobleemi lahendamiseks |
| Base case | Baasjuht | Triviaalne alamprobleem, mida saab lahendada otse ilma rekursioonita |
| Recursive function | Rekursiivne funktsioon | Tagastab väärtuse, mis on arvutatud rekursiivsete väljakutsete kaudu |
| Recursive procedure | Rekursiivne protseduur | Muudab sisendparameetreid rekursiivsete väljakutsete kaudu |
| Input parameter | Sisendparameeter | Väärtus, mida kasutatakse arvutuseks |
| Input-output parameter | Sisend-väljundparameeter | Väärtus, mida muudetakse täitmise käigus |
| Unary recursion | Unaarne rekursioon | Üks rekursiivne väljakutse funktsiooni kehas |
| Binary recursion | Binaarne rekursioon | Kaks rekursiivset väljakutset funktsiooni kehas |
| Ternary recursion | Ternaarne rekursioon | Kolm rekursiivset väljakutset funktsiooni kehas |
| Multiple recursion | Multirekursioon | Muutuv arv rekursiivseid väljakutseid |
| Tail recursion | Sabarekursioon | Rekursiivne väljakutse on viimane operatsioon |
| Recursion tree | Rekursioonipuu | Rekursiivsete väljakutsete visuaalne esitus |

## Ajakeerukus

| Inglise keeles | Eesti keeles | Selgitus |
|----------------|--------------|----------|
| Time complexity | Ajakeerukus | Kirjeldab, kuidas algoritmi täitmisaeg kasvab koos sisendi suurusega |
| O-notation | O-notatsioon | Ülemine piir (halvima juhu stsenaarium) |
| Θ-notation | Θ-notatsioon | Täpne piir (täpne kasvukiirus) |
| Ω-notation | Ω-notatsioon | Alumine piir (parima juhu stsenaarium) |
| Elementary operation | Elementaarne operatsioon | Arvutuse põhisamm, mille täitmisaeg on piiratud konstandiga |
| Best case | Parim juht | Minimaalne operatsioonide arv, mida vajatakse |
| Average case | Keskmine juht | Eeldatav operatsioonide arv tavalistes tingimustes |
| Worst case | Halvim juht | Maksimaalne operatsioonide arv, mida vajatakse |
| Amortized analysis | Amortiseeritud analüüs | Analüüs, mis arvestab operatsioonide keskmist jõudlust operatsioonide jadas |

## Erandite Käsitlemine

| Inglise keeles | Eesti keeles | Selgitus |
|----------------|--------------|----------|
| Exception | Erind | Erisituatsioon, mis võib programmi täitmise ajal tekkida |
| Exception class | Erindiklass | Klass, mis pärineb `Exception` klassist paketis `java.lang` |
| Try statement | Katsendidirektiiv | Struktuur, mis sisaldab try-plokki, catch-klausleid ja valikulist finally-klauslit |
| Catch clause | Püünis | Kood, mis käsitleb teatud tüüpi erandit |
| Finally clause | Epiloog | Kood, mis täidetakse sõltumata sellest, kas erand tekkis või mitte |
| Throw statement | Erindiheite direktiiv | Loob ja heidab erindi objekti |

## Üldised Programmeerimisterminid

| Inglise keeles | Eesti keeles | Selgitus |
|----------------|--------------|----------|
| Method | Meetod | Klassi kehas kirjeldatud funktsioon, mis määratleb käitumise |
| Instance method | Isendimeetod | Meetod, mis töötab klassi isendiga |
| Class method | Klassimeetod | `static` meetod, mis kuulub klassile endale, mitte üksikutele isenditele |
| Main method | Peameetod | Nõutav sisenemispunkt iseseisvate rakenduste jaoks signatuuriga `public static void main(String[])` |
| Signature | Signatuur | Meetodi nimi ja formaalsete parameetrite tüüpide loend |
| Package | Pakett | Kompilatsiooniüksuste kogum, mis algavad sama paketi deklaratsiooniga |
| Accessibility | Juurdepääsetavus | Deklaratsiooni nähtavuse ulatus, mida kontrollitakse modifikaatoritega |
| Thread | Lõim | Suhteliselt iseseisev protsess alamülesande täitmiseks |
| Synchronized statement | Sünkroondirektiiv | Tagab eksklusiivse juurdepääsu objektile ploki täitmise ajal |
| Standard package | Standardpakett | Paketid, mis on kaasatud Java põhidistributsiooni |
