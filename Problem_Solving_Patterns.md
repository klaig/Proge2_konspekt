# Probleemilahenduse Mustrid

Probleemilahenduse mustrid on strateegilised lähenemisviisid, mis aitavad struktueerida algoritmilist mõtlemist ja lahendada keerukaid programmeerimisülesandeid. Need mustrid on programmeerimises universaalsed ja neid saab rakendada paljude erinevate tüüpide probleemide lahendamisel.

## Sisukord
- [Jaga ja Valitse](#jaga-ja-valitse)
- [Ammendav Otsing](#ammendav-otsing)
- [Dünaamiline Programmeerimine](#dünaamiline-programmeerimine)
- [Ahned Algoritmid](#ahned-algoritmid)
- [Tagurdamine](#tagurdamine)
- [Praktiline Probleemide Lahendamise Lähenemine](#praktiline-probleemide-lahendamise-lähenemine)

## Jaga ja Valitse

Jaga ja valitse (ingl. _divide and conquer_) on strateegia, mis jagab keeruka probleemi väiksemateks, lihtsamini lahendatavateks alamprobleemideks, lahendab need alamprobleemid rekursiivselt ja seejärel kombineerib nende lahendused algse probleemi lahenduseks.

### Põhisammud
1. **Jaga** - Jaota probleem väiksemateks alamprobleemideks
2. **Valitse** - Lahenda alamprobleemid rekursiivselt
3. **Kombineeri** - Ühenda alamprobleemide lahendused algse probleemi lahenduseks

### Levinud Rakendused
- **Merge Sort**
  ```java
  public static void mergeSort(int[] arr) {
      if (arr.length <= 1) {
          return;
      }
      
      int keskkoht = arr.length / 2;
      int[] vasak = new int[keskkoht];
      int[] parem = new int[arr.length - keskkoht];
      
      // Kopeeri elemendid vasak- ja parempoole massiividesse
      System.arraycopy(arr, 0, vasak, 0, keskkoht);
      System.arraycopy(arr, keskkoht, parem, 0, arr.length - keskkoht);
      
      // Sorteeri mõlemad pooled
      mergeSort(vasak);
      mergeSort(parem);
      
      // Ühenda tulemused
      merge(arr, vasak, parem);
  }
  
  private static void merge(int[] tulemus, int[] vasak, int[] parem) {
      int i = 0, j = 0, k = 0;
      
      while (i < vasak.length && j < parem.length) {
          if (vasak[i] < parem[j]) {
              tulemus[k++] = vasak[i++];
          } else {
              tulemus[k++] = parem[j++];
          }
      }
      
      while (i < vasak.length) {
          tulemus[k++] = vasak[i++];
      }
      
      while (j < parem.length) {
          tulemus[k++] = parem[j++];
      }
  }
  ```

- **Quick Sort**
- **Binaarotsing**
- **Matriksite korrutamine (Strasseni algoritm)**
- **Lähimad punktid tasandil**

### Eelised
- Sageli viib efektiivsetele algoritmidele, eriti suurte sisendite puhul
- Loomulikult sobilik paralleelseks töötlemiseks
- Kontseptuaalselt selge lähenemine probleemi lahendamisele

### Puudused
- Rekursiivsete väljakutsete üldkulud võivad väikeste sisendite puhul olla märkimisväärsed
- Võib vajada täiendavat mäluruumi ühendamisfaasi ajal
- Mitte alati kõige efektiivsem lähenemine kõigi probleemide jaoks

## Ammendav Otsing

Ammendav otsing (ingl. _exhaustive search_ või _brute force_) uurib süstemaatiliselt kõiki võimalikke lahendusi, et leida üks või kõik, mis lahendavad probleemi.

### Põhiomadused
- Garanteerib optimaalse lahenduse leidmise, kui see eksisteerib
- Tavaliselt lihtne implementeerida
- Sageli ebaefektiivne suurte probleemiruumide korral

### Levinud Rakendused
- **Kõigi Permutatsioonide Genereerimine**
  ```java
  public static void genereeriPermutatsioonid(char[] elemendid, int algus) {
      if (algus == elemendid.length - 1) {
          System.out.println(String.valueOf(elemendid));
          return;
      }
      
      for (int i = algus; i < elemendid.length; i++) {
          // Vaheta elemendid
          char temp = elemendid[algus];
          elemendid[algus] = elemendid[i];
          elemendid[i] = temp;
          
          // Rekursiivne väljakutse ülejäänud elementide jaoks
          genereeriPermutatsioonid(elemendid, algus + 1);
          
          // Taasta algne järjekord (tagurdamine)
          temp = elemendid[algus];
          elemendid[algus] = elemendid[i];
          elemendid[i] = temp;
      }
  }
  ```

- **Kõigi Alamhulkade Genereerimine**
  ```java
  public static void genereeriAlamhulgad(int[] elemendid, int indeks, List<Integer> praegune) {
      if (indeks == elemendid.length) {
          System.out.println(praegune);
          return;
      }
      
      // Jäta praegune element vahele
      genereeriAlamhulgad(elemendid, indeks + 1, new ArrayList<>(praegune));
      
      // Kaasa praegune element
      List<Integer> uus = new ArrayList<>(praegune);
      uus.add(elemendid[indeks]);
      genereeriAlamhulgad(elemendid, indeks + 1, uus);
  }
  ```

- **Rändkaupmehe Probleem (Naiivne Lähenemine)**
- **Tõeväärtusavaldiste Rahuldamine (SAT)**
- **Mõistatuste Lahendamine (nt Sudoku)**

### Optimeerimistehnikad
- Otsingupuu varajane kärpimine
- Piirangute levitamine
- Heuristikad otsingu suunamiseks
- Järk-järguline süvenemine

## Dünaamiline Programmeerimine

Dünaamiline programmeerimine (ingl. _dynamic programming_) on meetod keerukate probleemide lahendamiseks, jagades need lihtsamateks alamprobleemideks ja salvestades nende lahendused, et vältida korduvaid arvutusi.

### Põhiomadused
1. **Optimaalne alamstruktuur** - Probleemi optimaalne lahendus sisaldab alamprobleemide optimaalseid lahendusi
2. **Kattuvad alamprobleemid** - Samu alamprobleeme lahendatakse korduvalt

### Implementatsiooni Lähenemisviisid
1. **Memoiseerimine (Ülevalt-Alla)**
   ```java
   public static int fibonacciMemoiseerimine(int n, Integer[] memo) {
       if (memo[n] != null) {
           return memo[n];
       }
       
       if (n <= 1) {
           return n;
       }
       
       memo[n] = fibonacciMemoiseerimine(n-1, memo) + fibonacciMemoiseerimine(n-2, memo);
       return memo[n];
   }
   ```

2. **Tabuleerimine (Alt-Üles)**
   ```java
   public static int fibonacciTabuleerimine(int n) {
       if (n <= 1) {
           return n;
       }
       
       int[] dp = new int[n + 1];
       dp[0] = 0;
       dp[1] = 1;
       
       for (int i = 2; i <= n; i++) {
           dp[i] = dp[i-1] + dp[i-2];
       }
       
       return dp[n];
   }
   ```

### Levinud Rakendused
- **Pikim Ühine Alamjärjend**
  ```java
  public static int pikimÜhineAlamjärjend(String s1, String s2) {
      int[][] dp = new int[s1.length() + 1][s2.length() + 1];
      
      for (int i = 1; i <= s1.length(); i++) {
          for (int j = 1; j <= s2.length(); j++) {
              if (s1.charAt(i-1) == s2.charAt(j-1)) {
                  dp[i][j] = dp[i-1][j-1] + 1;
              } else {
                  dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
              }
          }
      }
      
      return dp[s1.length()][s2.length()];
  }
  ```

- **Seljakoti Probleem**
  ```java
  public static int seljakott(int[] kaalud, int[] väärtused, int maht) {
      int n = kaalud.length;
      int[][] dp = new int[n + 1][maht + 1];
      
      for (int i = 1; i <= n; i++) {
          for (int w = 0; w <= maht; w++) {
              if (kaalud[i-1] <= w) {
                  dp[i][w] = Math.max(väärtused[i-1] + dp[i-1][w - kaalud[i-1]], dp[i-1][w]);
              } else {
                  dp[i][w] = dp[i-1][w];
              }
          }
      }
      
      return dp[n][maht];
  }
  ```

- **Lühima Tee Probleemid**
- **Matriksite Ahelkorrutamine**
- **Redigeerimiskaugus**
- **Mündide Vahetamise Probleem**

### Eelised
- Elimineerib korduvad arvutused
- Sageli muudab eksponentsiaalse ajakeerukusega algoritmid polünomiaalseks
- Võib pakkuda optimaalseid lahendusi laiale probleemide ringile

### Puudused
- Võib vajada märkimisväärset mälu memoiseerimiseks või tabuleerimiseks
- Optimaalse alamstruktuuri tuvastamine võib olla keeruline
- Rekurrentsiseose korrektne formuleerimine on ülioluline

## Ahned Algoritmid

Ahned algoritmid (ingl. _greedy algorithms_) teevad igas etapis lokaalselt optimaalse valiku, lootes leida globaalset optimumi.

### Põhiomadused
- Teeb "parima" otsuse igal sammul, ilma ettevaatamiseta
- Ei kaalu kunagi uuesti varasemaid valikuid (erinevalt tagurdamisest)
- Lihtne ja sageli efektiivne, kuid ei leia alati optimaalset lahendust

### Levinud Rakendused
- **Mündide Vahetamine (kui mündid on teatud omadustega)**
  ```java
  public static int vahetaMündid(int[] mündid, int summa) {
      // Eeldame, et mündid on järjestatud kahanevalt
      Arrays.sort(mündid);
      int indeks = mündid.length - 1;
      
      int loendur = 0;
      while (summa > 0 && indeks >= 0) {
          while (summa >= mündid[indeks]) {
              summa -= mündid[indeks];
              loendur++;
          }
          indeks--;
      }
      
      return summa == 0 ? loendur : -1;  // Tagastab -1, kui täpset vahetust ei saa teha
  }
  ```

- **Tegevuste Valimine**
  ```java
  public class Tegevus {
      int algusAeg;
      int lõpuAeg;
      
      public Tegevus(int algusAeg, int lõpuAeg) {
          this.algusAeg = algusAeg;
          this.lõpuAeg = lõpuAeg;
      }
  }
  
  public static List<Tegevus> valiTegevused(List<Tegevus> tegevused) {
      // Sorteeri tegevused lõpuaja järgi
      Collections.sort(tegevused, Comparator.comparingInt(a -> a.lõpuAeg));
      
      List<Tegevus> valitud = new ArrayList<>();
      int viimaneAeg = 0;
      
      for (Tegevus tegevus : tegevused) {
          if (tegevus.algusAeg >= viimaneAeg) {
              valitud.add(tegevus);
              viimaneAeg = tegevus.lõpuAeg;
          }
      }
      
      return valitud;
  }
  ```

- **Huffmani Kodeerimine**
- **Murduv Seljakott**
- **Miinimumse Hõlmava Puu Leidmine (Prim, Kruskal)**
- **Dijkstra Lühima Tee Algoritm**

### Millal Kasutada Ahneid Algoritme
- Probleem omab optimaalset alamstruktuuri
- Probleem omab ahnet valikuomadust (lokaalselt optimaalne valik viib globaalselt optimaalse lahenduseni)
- Probleemid, mis hõlmavad ressursside jaotamist teatud piirangutega

### Eelised
- Tavaliselt lihtne implementeerida
- Tihti väga efektiivne täitmisaja mõttes
- Töötab hästi teatud optimeerimisprobleemide korral

### Puudused
- Ei too alati optimaalset lahendust
- Vajab tõestust, et ahne lähenemine töötab konkreetse probleemi korral
- Võib olla keeruline määrata, kas ahne lähenemine on kehtiv

## Tagurdamine

Tagurdamine (ingl. _backtracking_) on algoritmiline tehnika, mis ehitab lahenduskandidaate järk-järgult ja loobub kandidaadist ("tagurdab") niipea, kui määrab, et kandidaat ei saa viia sobiva lahenduseni.

### Põhiomadused
- Kasutab sügavuti otsingu lähenemist
- Uurib lahendusruumi süstemaatiliselt
- Kärpib harusid, mis ei saa viia kehtiva lahenduseni

### Levinud Rakendused
- **N-Lipu Probleem**
  ```java
  public static boolean lahendaNLipud(int[][] laud, int veerg, int n) {
      // Baasjuht: kui kõik lipud on paigutatud
      if (veerg >= n) {
          väljastalaud(laud);
          return true;
      }
      
      boolean tulemus = false;
      
      // Proovi paigutada lippu iga rea selles veerus
      for (int i = 0; i < n; i++) {
          // Kontrolli, kas on turvaline paigutada lipp [i][veerg]
          if (onTurvaline(laud, i, veerg, n)) {
              laud[i][veerg] = 1;  // Aseta lipp
              
              // Rekursiivselt paiguta ülejäänud lipud
              tulemus = lahendaNLipud(laud, veerg + 1, n) || tulemus;
              
              laud[i][veerg] = 0;  // Tagurdamine
          }
      }
      
      return tulemus;
  }
  
  private static boolean onTurvaline(int[][] laud, int rida, int veerg, int n) {
      // Kontrolli rida vasakule
      for (int j = 0; j < veerg; j++) {
          if (laud[rida][j] == 1) {
              return false;
          }
      }
      
      // Kontrolli ülemist diagonaali vasakule
      for (int i = rida, j = veerg; i >= 0 && j >= 0; i--, j--) {
          if (laud[i][j] == 1) {
              return false;
          }
      }
      
      // Kontrolli alumist diagonaali vasakule
      for (int i = rida, j = veerg; i < n && j >= 0; i++, j--) {
          if (laud[i][j] == 1) {
              return false;
          }
      }
      
      return true;
  }
  
  private static void väljastalaud(int[][] laud) {
      for (int[] rida : laud) {
          for (int element : rida) {
              System.out.print(element + " ");
          }
          System.out.println();
      }
      System.out.println();
  }
  ```

- **Sudoku Lahendaja**
  ```java
  public static boolean lahendaSudoku(int[][] laud) {
      for (int rida = 0; rida < 9; rida++) {
          for (int veerg = 0; veerg < 9; veerg++) {
              // Leia tühi ruut
              if (laud[rida][veerg] == 0) {
                  // Proovi asetada number 1-9
                  for (int arv = 1; arv <= 9; arv++) {
                      if (onKehtiv(laud, rida, veerg, arv)) {
                          laud[rida][veerg] = arv;
                          
                          // Rekursiivselt proovi lahendada
                          if (lahendaSudoku(laud)) {
                              return true;
                          }
                          
                          // Kui lahendus ei töötanud, tagurda
                          laud[rida][veerg] = 0;
                      }
                  }
                  return false;  // Lahendust ei leitud
              }
          }
      }
      return true;  // Kõik ruudud on täidetud
  }
  
  private static boolean onKehtiv(int[][] laud, int rida, int veerg, int arv) {
      // Kontrolli rida
      for (int j = 0; j < 9; j++) {
          if (laud[rida][j] == arv) {
              return false;
          }
      }
      
      // Kontrolli veergu
      for (int i = 0; i < 9; i++) {
          if (laud[i][veerg] == arv) {
              return false;
          }
      }
      
      // Kontrolli 3x3 plokki
      int blokkRida = rida - rida % 3;
      int blokkVeerg = veerg - veerg % 3;
      
      for (int i = blokkRida; i < blokkRida + 3; i++) {
          for (int j = blokkVeerg; j < blokkVeerg + 3; j++) {
              if (laud[i][j] == arv) {
                  return false;
              }
          }
      }
      
      return true;  // Arv on kehtiv
  }
  ```

- **Hamiltoni Tee**
- **Graafi Värvimine**
- **Alamhulga Summa**
- **Krüptaritmeetilised Mõistatused**

### Eelised
- Saab efektiivselt lahendada probleeme piirangutega
- Uurib süstemaatiliselt lahendusruumi
- Väldib tarbetut tööd läbi varajase kärpimise

### Puudused
- Võib olla eksponentsiaalselt aeglane halvimal juhul
- Vajab hoolikat implementatsiooni, et vältida tarbetuid arvutusi
- Rekursiivse kutsesteki mälukasutus võib olla märkimisväärne

## Praktiline Probleemide Lahendamise Lähenemine

Edukas probleemide lahendamine hõlmab struktureeritud lähenemist, mis ei sõltu ainult ühest tehnikast.

1. **Mõista probleemi põhjalikult**
   - Identifitseeri piirangud ja nõuded
   - Selgita välja sisendi/väljundi spetsifikatsioonid
   - Kaalu ääretingimusi ja erandeid

2. **Jaga probleem osadeks**
   - Identifitseeri alamprobleemid
   - Määra kindlaks seosed alamprobleemide vahel
   - Otsi mustreid või sarnaseid probleeme

3. **Vali sobiv strateegia**
   - Arvesta aja- ja ruumikeerukuse nõudeid
   - Hinda, kas probleem omab optimaalset alamstruktuuri või kattuvaid alamprobleeme
   - Kaalu, kas ahne lähenemine võiks töötada

4. **Implementeeri lahendus**
   - Alusta lihtsa, korrektse implementatsiooniga
   - Lisa optimeerimisi vastavalt vajadusele
   - Testi erinevate sisenditega, eriti äärejuhtudega

5. **Analüüsi ja täiusta**
   - Mõõda tegelikku jõudlust
   - Identifitseeri pudelikaelad
   - Kaalu alternatiivseid lähenemisi, kui vaja

### Näidisprobleemi Lahendamine

**Probleem**: Leia maksimaalne alammassiivi summa massiivi järjestikustest elementidest.

**Näide**: 
```
Sisend: [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Väljund: 6 (alammassiiv [4, -1, 2, 1])
```

**1. Brutaaljõuline Lähenemine** (O(n³) ajakeerukus):
```java
public static int maxAlammassiivSumma_Brute(int[] massiiv) {
    int n = massiiv.length;
    int maksSumma = Integer.MIN_VALUE;
    
    // Proovi kõiki alammassiive
    for (int algus = 0; algus < n; algus++) {
        for (int lõpp = algus; lõpp < n; lõpp++) {
            int summa = 0;
            for (int i = algus; i <= lõpp; i++) {
                summa += massiiv[i];
            }
            maksSumma = Math.max(maksSumma, summa);
        }
    }
    
    return maksSumma;
}
```

**2. Parem Brutaaljõuline Lähenemine** (O(n²) ajakeerukus):
```java
public static int maxAlammassiivSumma_Better(int[] massiiv) {
    int n = massiiv.length;
    int maksSumma = Integer.MIN_VALUE;
    
    // Proovi kõiki alammassiive
    for (int algus = 0; algus < n; algus++) {
        int summa = 0;
        for (int lõpp = algus; lõpp < n; lõpp++) {
            summa += massiiv[lõpp];
            maksSumma = Math.max(maksSumma, summa);
        }
    }
    
    return maksSumma;
}
```

**3. Dünaamiline Programmeerimine (Kadane'i algoritm)** (O(n) ajakeerukus):
```java
public static int maxAlammassiivSumma_Kadane(int[] massiiv) {
    int n = massiiv.length;
    int praeguSumma = 0;
    int maksSumma = Integer.MIN_VALUE;
    
    for (int i = 0; i < n; i++) {
        praeguSumma = Math.max(massiiv[i], praeguSumma + massiiv[i]);
        maksSumma = Math.max(maksSumma, praeguSumma);
    }
    
    return maksSumma;
}
```

Erinevad probleemid võivad nõuda erinevaid lähenemisviise või isegi nende kombinatsioone. Oskus ära tunda, milline muster on probleemi jaoks kõige sobivam, tuleb kogemuse ja praktikaga.

Probleemilahenduse mustrid on programmeerimises võimsad tööriistad. Neid tundma õppides arendad sa oma algoritmilist mõtlemist ja muudad keerukate probleemide lahendamise lihtsamaks.
