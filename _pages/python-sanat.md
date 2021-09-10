---
title: "Sanojen etsiminen Pythonilla"
hidden: true
---

# Sanojen etsiminen Pythonilla

Kurssin I-osan aloitusluennolla käytiin läpi esimerkki, jossa etsitään suomen ja englannin kielen yhteisiä sanoja. Käytössä ovat seuraavat aineistot:

* [suomen kielen sanalista](../assets/suomi.txt) (91591 sanaa)
* [englannin kielen sanalista](../assets/englanti.txt) (109582 sanaa)

Seuraava ohjelma lukee sanalistat listoihin ja etsii sitten yhteiset sanat. Silmukka käy läpi kaikki suomen kielen sanat ja tulostaa jokaisen sanan, joka on myös englannin kielen sana.

```python
words_finnish = open("suomi.txt").read().splitlines()
words_english = open("englanti.txt").read().splitlines()

for word in words_finnish:
    if word in words_english:
        print(word)
```

Ohjelman suoritus näyttää seuraavalta:

```
$ python3 sanat.py
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
$ time python3 sanat.py
abo
adagio
adonis
...
zombie
zucchini
zulu


real	1m46.488s
user	1m46.468s
sys	0m0.012s
```

Sanojen etsiminen vei siis aikaa 1 minuutin ja 46 sekuntia. Huomaa, että luennolla tuli eri aika, koska ohjelma suoritettiin eri koneessa ja samaan aikaan oli käynnissä Zoom.

Ohjelman pullonkaula on seuraava rivi, joka tarkastaa, onko sana englannin kielen sana:

```python
    if word in words_english:
```

Tämä tarkastus on hidas, koska englannin kielen sanat ovat listassa, josta on hidasta etsiä alkioita. Tehokkaampi tapa on muuttaa koodia niin, että käytössä onkin hajautustaulu:

```python
words_english = set(open("englanti.txt").read().splitlines())
```

Tämän muutoksen seurauksena ohjelma toimii hyvin nopeasti:

```
$ time python3 sanat.py
abo
adagio
adonis
...
zombie
zucchini
zulu

real	0m0.081s
user	0m0.069s
sys	0m0.012s
```

Tämä on kurssin tavoite: haluamme oppia käyttämään tietorakenteita ja algoritmeja niin, että saamme aikaan tehokkaita ohjelmia.
