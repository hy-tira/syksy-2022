---
title: "Sanojen etsiminen Javalla"
hidden: true
---

# Sanojen etsiminen Javalla

Kurssin I-osan aloitusluennolla käytiin läpi esimerkki, jossa etsitään suomen ja englannin kielen yhteisiä sanoja. Käytössä ovat seuraavat aineistot:

* [suomen kielen sanalista](../assets/suomi.txt) (91591 sanaa)
* [englannin kielen sanalista](../assets/englanti.txt) (109582 sanaa)

Seuraava ohjelma lukee sanalistat listoihin ja etsii sitten yhteiset sanat. Silmukka käy läpi kaikki suomen kielen sanat ja tulostaa jokaisen sanan, joka on myös englannin kielen sana.

```python
import java.util.*;
import java.io.*;

public class Sanat {
    public static void main(String[] args) throws Exception {
        ArrayList<String> finnishWords = new ArrayList<>();
        ArrayList<String> englishWords = new ArrayList<>();

        Scanner scanner;
        scanner = new Scanner(new File("suomi.txt"));
        while (scanner.hasNext()) {
            finnishWords.add(scanner.next());
        }
        scanner = new Scanner(new File("englanti.txt"));
        while (scanner.hasNext()) {
            englishWords.add(scanner.next());
        }

        for (String word : finnishWords) {
            if (englishWords.contains(word)) {
                System.out.println(word);
            }
        }
    }
}
```

Ohjelman suoritus näyttää seuraavalta:

```
$ java Sanat
abo
adagio
adonis
aerobic
afrikaans
afro
agar
agenda
ah
ai
...
```

Suoritetaan ohjelma vielä `time`-komennon kautta, jotta saamme tietää sen suoritusajan:

```
$ time java Sanat
abo
adagio
adonis
...
zombie
zucchini
zulu

real	2m39.073s
user	2m39.608s
sys	0m0.125s
```

Sanojen etsiminen vei siis aikaa 2 minuuttia ja 39 sekuntia.

Ohjelman pullonkaula on seuraava rivi, joka tarkastaa, onko sana englannin kielen sana:

```java
            if (englishWords.contains(word)) {
```

Tämä tarkastus on hidas, koska englannin kielen sanat ovat listassa, josta on hidasta etsiä alkioita. Tehokkaampi tapa on muuttaa koodia niin, että käytössä onkin hajautustaulu:

```java
        HashSet<String> englishWords = new HashSet<>();
```

Tämän muutoksen seurauksena ohjelma toimii hyvin nopeasti:

```
$ time java Sanat
abo
adagio
adonis
...
zombie
zucchini
zulu

real	0m0.333s
user	0m0.834s
sys	0m0.052s
```

Tämä on kurssin tavoite: haluamme oppia käyttämään tietorakenteita ja algoritmeja niin, että saamme aikaan tehokkaita ohjelmia.
