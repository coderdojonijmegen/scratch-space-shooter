---
title: "Scratch - Space shooter"
date: 2020-10-06T21:00:00+02:00
draft: false
toc: true
headercolor: "teal-background"
---

Je gaat met Scratch een "space shooter" bouwen.

<!--more-->

## Benodigdheden

Deze opdrachten maak je met [Scratch](https://scratch.mit.edu/). Als je nog geen account had, maak dit dan eerst aan.

Zet in Scratch eerst de taal op Nederlands via de wereldbol linksboven.

## Inleiding

In deze opdracht ga je een "space shooter" spel bouwen, waarbij je een ruimteschip bestuurt dat meteorieten kapot moet schieten of ontwijken.

Dit zijn de stappen die je gaat programmeren:

1. Laat een ruimteschip bewegen met de pijltjestoetsen
2. Maak een bewegende achtergrond waardoor het lijkt alsof je door de ruimte vliegt
3. Laat meteorieten verschijnen en naar het ruimteschip vliegen
4. Zorg dat het ruimteschip op de meteorieten kan schieten

Als je hierna nog zin (en tijd) hebt dan zijn er nog allerlei uitbreidingen mogelijk, denk bijvoorbeeld aan het spel steeds iets moeilijker maken of geluid en andere _special effects_ toevoegen.

## Laat een ruimteschip bewegen met de pijltjestoetsen

Eerst moet je een sprite hebben voor je ruimteschip. Je kunt dit natuurlijk zelf ontwerpen, maar ook een bestaande sprite kiezen (bijvoorbeeld het _Rocketship_).

Zorg er eerst voor dat de sprite niet te groot is ten opzichte van het speelveld. Je kunt dit doen door het blok _maak grootte_ te gebruiken dat je vindt in het menu _Uiterlijken_. Speel een beetje met het percentage om de goede grootte te vinden. Zorg ook dat het ruimteschip in het midden onderaan begint door het op x = 0 te plaatsen (x loopt van links naar rechts) en y zo in te stellen dat het nog net in beeld is. Je programma zou er nu ongeveer zo uit moeten zien:

{{< scratch >}}
      wanneer groene vlag wordt aangeklikt
      maak grootte (25) %
      ga naar x: (0) y: (-150)
{{< /scratch >}}

De beweging van het ruimteschip kun je op verschillende manieren programmeren. Je kunt bijvoorbeeld iedere keer bij het indrukken van _pijltje links_ de sprite een stukje laten opschuiven. Bij dit spel gaat het iets anders: als je op een pijltjestoets drukt dan geef je het ruimteschip een bepaalde snelheid, die vervolgens weer naar 0 (dus stilstaan) gaat. Op deze manier zal het ruimteschip een mooie vloeiende beweging maken. Neem de volgende stappen:

- Maak een **variabele** _x-snelheid_ aan (in het menu Variabelen).
- Zet deze snelheid aan het begin van het spel op 0.
- Verander de snelheid naar een getal groter dan 0 als _pijltje rechts_ wordt ingedrukt, en kleiner dan 0 voor _pijltje links_.
- Verander vervolgens de (x-)positie van het ruimteschip met de waarde van de variabele _x-snelheid_.
- Laat de snelheid steeds iets verder afnemen tot deze uiteindelijk weer 0 is.

_Tip 1_: de laatste drie stappen in de lijst hierboven moet je in een _herhaal_ blok zetten.

_Tip 2_: je kunt de snelheid bijvoorbeeld laten afnemen door er een getal van af te trekken. Een andere manier is om de waarde te vermenigvuldigen met een getal kleiner dan 1.

{{< voorbeeld kop="Klik om te laten zien hoe je programma er nu ongeveer uit zou moeten zien." >}}
{{< scratch >}}
      wanneer groene vlag wordt aangeklikt
      maak grootte (25) %
      ga naar x: (0) y: (-150)
      maak [snelheid_x] (0)
      herhaal
      als &lt;toets [pijltje links v] ingedrukt?&gt; dan
      maak [snelheid_x] (5)
      end
      als &lt;toets [pijltje rechts v] ingedrukt?&gt; dan
      maak [snelheid_x] (-5)
      end
      verander x met snelheid: (snelheid_x)
      maak [snelheid_x] ((snelheid_x) * (0.9))
      end
{{< /scratch >}}
{{< /voorbeeld >}}

## Maak een bewegende achtergrond waardoor het lijkt alsof je door de ruimte vliegt

Download dit plaatje voor de achtergrond van het spel:

![Ruimte](imgs/ruimte.gif)

Volg deze stappen om van dit plaatje een sprite voor de achtergrond te maken:

1. Klik op het icoon voor een nieuwe sprite (rechtsonder, plaatje van de kat) en kies voor Upload sprite.
2. Upload het ruimte-plaatje.
3. Ga naar het tabblad Uiterlijken (linksboven, rechts naast het Code tabblad).
4. Maak in de editor het plaatje net zo groot als het hele speelveld door het op te rekken.

Laat de achtergrond aan het begin van het spel in het midden van het speelveld, dan zijn _x_ en _y_ allebei 0:

{{< scratch >}}
      wanneer groene vlag wordt aangeklikt
      ga naar x: (0) y: (0)
{{< /scratch >}}

Nu ga je de achtergrond laten bewegen zodat het net is of je schip door de ruimte vliegt. **Vraag**: als je wil dat je schip vooruit vliegt, welke kant moet de achtergrond dan op gaan?

Net als bij de snelheid van je ruimteschip moet je hier een variabele maken, nu voor de "scroll" snelheid van de ruimte. Vervolgens verander je steeds de positie van de achtergrond met de snelheid die je hebt ingesteld. **Vraag**: moet je nu de _x_ of de _y_ veranderen? En moet _x_ of _y_ steeds groter worden? Of juist kleiner?

{{< voorbeeld kop="Klik om de code te bekijken." >}}
{{< scratch >}}
      wanneer groene vlag wordt aangeklikt
      ga naar x: (0) y: (0)
      maak [snelheid_scrollen] (4)
      herhaal
      verander y met ((snelheid_scrollen) * (-1))
      end
{{< /scratch >}}
{{< /voorbeeld >}}

Als je nu het programma start, dan zie je dat er twee dingen fout gaan:

- je achtergrond verdwijnt uit beeld en komt niet meer terug
- er verschijnt een steeds groter wit vlak!

Een manier om deze twee problemen op te lossen staat beschreven in deze afbeelding:

![Scrollen](imgs/ruimte-scrollen.png)

Wat je ziet is dat je twee achtergronden nodig hebt: de sprite, en een _kloon_ van de sprite. Pijl (1) geeft aan dat de sprite en kloon allebei naar beneden schuiven. Pijl (2) geeft aan dat zodra er een achtergrond _uit beeld_ is verdwenen, je deze weer naar boven moet verplaatsen. Op deze manier zorg je ervoor dat je geen wit vlak meer zult zien! Je moet nu dus een stuk code schrijven dat _als_ de sprite uit beeld is (**vraag**: wat is dan de waarde van _y_?) deze weer naar boven verplaatst. En je moet deze code niet alleen schrijven voor de sprite zelf, maar ook voor de kloon van de sprite. Dit is best lastig, probeer het eerst eens alleen voor de sprite zelf.

{{< voorbeeld kop="Uiteindelijk is dit de code die zorgt voor een bewegende achtergrond." >}}
{{< scratch >}}
      wanneer groene vlag wordt aangeklikt
      ga naar x: (0) y: (0)
      maak een kloon van [mijzelf v]
      maak [snelheid_scrollen] (4)
      herhaal
      als &lt;(y-positie) > (-340)&gt; dan
      verander y met ((snelheid_scrollen) * (-1))
      anders
      ga naar x: (0) y: (345)
      end
      end

      wanneer ik als kloon start
      ga naar x: (0) y: (345)
      maak [snelheid_scrollen] (4)
      herhaal
      als &lt;(y-positie) > (-340)&gt; dan
      verander y met ((snelheid_scrollen) * (-1))
      anders
      ga naar x: (0) y: (345)
      end
      end

{{< /scratch >}}
{{< /voorbeeld >}}

## Laat meteorieten verschijnen en naar het ruimteschip vliegen

{{< voorbeeld kop="Code voor kogels 1" >}}
{{< scratch >}}
      wanneer groene vlag wordt aangeklikt
      maak grootte (50) %
      verdwijn
      herhaal
      als &lt;toets [spatiebalk v] ingedrukt?&gt; dan
      maak een kloon van (mijzelf v)
      wacht (0.5) sec.
      end
      end
{{< /scratch >}}
{{< /voorbeeld >}}

{{< voorbeeld kop="Code voor kogels 2" >}}
{{< scratch >}}
      wanneer ik als kloon start
      verschijn
      ga naar laag [voorgrond v]
      ga naar (Ruimteschip v)
      herhaal tot &lt;raak ik (rand v)?&gt;
      verander y met (10)
      end
      end
{{< /scratch >}}
{{< /voorbeeld >}}

{{< voorbeeld kop="Code voor meteorieten 1" >}}
{{< scratch >}}
      wanneer groene vlag wordt aangeklikt
      verdwijn
      maak grootte (20) %
      maak [score v] (0)
      herhaal
      wacht (4) sec.
      maak een kloon van (mijzelf v)
      end
{{< /scratch >}}
{{< /voorbeeld >}}

{{< voorbeeld kop="Code voor meteorieten 2" >}}
{{< scratch >}}
      wanneer ik als kloon start
      ga naar laag [voorgrond v]
      verschijn
      ga naar x: (willekeurig getal tussen (-200) en (200)) y: (180)
      herhaal tot &lt; (y-positie) < (-180)&gt;
      verander y met (-2)
      end
      verwijder deze kloon
{{< /scratch >}}
{{< /voorbeeld >}}

{{< voorbeeld kop="Code voor meteorieten 3" >}}
{{< scratch >}}
      wanneer ik als kloon start
      herhaal
      als &lt; raak ik (Kogel v)?&gt; dan
      verander [score v] met (1)
      verwijder deze kloon
      end
{{< /scratch >}}
{{< /voorbeeld >}}

{{< voorbeeld kop="Code voor meteorieten 4" >}}
{{< scratch >}}
      wanneer ik als kloon start
      herhaal
      als &lt; raak ik (Ruimteschip v)?&gt; dan
      maak [score v] (0)
      verwijder deze kloon
      end
{{< /scratch >}}
{{< /voorbeeld >}}

{{< voorbeeld kop="Klik om de voorbeeldcode te laten zien" >}}
{{< scratch >}}
      wanneer ik als kloon start
      als &lt;raak ik kleur [#9afeb6]?&gt; dan
      stop [alle v]
{{< /scratch >}}
{{< /voorbeeld >}}

## Uitbreidingen

Je kunt het spel natuurlijk nog veel mooier, spannender en moeilijker maken.
Hier heb je alvast een lijstje met ideeën als je nog verder wil programmeren
aan *Snake*:

* laat de appels na een tijdje weer verdwijnen
* maak een start- of eindscherm voor het spel
* laat de slang sneller gaan als je meer appels hebt gegeten
* laat het spel ook afgelopen zijn als je de rand raakt
* kies een mooie achtergrond voor je spel
* laat ook voorwerpen verschijnen die je juist moet ontwijken
* programmeer het spel voor twee spelers

{{< licentie rel="http://creativecommons.org/licenses/by-nc-sa/4.0/">}}
