---
layout: separate-page
title: Datorseende med Python och OpenCV
author: William Sjöblom
permalink: /other/cv-lab/
---

# Datorseende med Python och OpenCV

## Introduktion
Denna laboration kommer göras i programmeringsspråket [Python](https://www.python.org/). Laborationen kommer inte kräva någon tidigare erfarenhet av programmering eller bildbehandling. Funktionerna vi kommer använda är förenklade varianter av de som finns i  programvaubiblioteket [OpenCV](https://opencv.org/). Om intresse finns att se vilka anrop som egentligen görs till OpenCV kan ni kolla i filen `vision.py`, det är dock inte nödvändligt för att klara av labben.

## Teori, HSV

Inom datorseende används ofta färgsystemet HSV istället för det vanligare systemet RGB. I RGB används tre heltal mellan 0 och 255 (bytes). Ofta uttrycks dessa heltal i bas 16, alltså blir intervallet 00 till FF. Dessa heltal betecknar den röda, gröna respektive blå färgkomponententerna i varje pixel. Exempelvis kan rött uttryckas som (255, 0, 0) eller (0xFF, 0, 0), rosa som (255, 0, 255) och ljusgrått som (200, 200, 200).

Trots att RGB är det vanligaste sättet att representera färger på så är det inte speciellt smidigt när man sysslar med bildbehandling. I HSV beskrivs istället en färg av kulör (H), mättnad (S) och ljusintensitet (V) (från engelskans Hue, Saturation och Value).

Den största anledningen att färgsystemet HSV är väl lämpade för datorseende är att denna skala separerar en färgs intensitet från dess faktiska färginnehåll. Detta gör det bland annat möjligt att på ett effektivt sätt beskriva färgintervall vilket vi snart kommer göra!

![alt text](https://henrydangprg.files.wordpress.com/2016/06/hsv_color_solid_cylinder_alpha_lowgamma.png?w=322&h=241)

_Färgsystemet HSV._

### 0. Uppstart
I det svarta terminalfönstret som bör finnas på er skärm: skriv `cd cv-lab`.
För att sedan testköra programmet ni snart ska skriva: skriv `python2 lab.py`.
För att slutligen stänga programmet: tryck `q`.

Det bör också finnas en texteditor på skärmen med filen `lab.py` öppen. Denna fil bör innehålla något i stil med detta:
{% highlight python %}
import vision

def find(image):
	# Skriv din kod här!
	
vision.run(find)
{% endhighlight %}

Ersätt `# Skriv din kod här` med de anrop du vill göra (ett anrop per rad). Information om dessa anrop kan ses under "Dokumentation".
Observera textindraget vid `# Skriv din kod här`, all kodrader ni skriver ska vara indragna på detta sätt. Detta indrag kommer din texteditor skapa åt dig automatiskt!

### 1. Visa bild
Till en början vill vi göra oss bekanta med anropet `image.show()`. Detta anrop används för att visa hur bilden förändrats efter pålagda transformationer. Vi börjar med att lägga till raden `image.show()` under `def find(image):`. (Glöm inte textindraget som besrkivs under "0. Uppstart"!) Det vi kommer se nu är bilden utan några pålagda transformationer. I bilden kommer kommer kulörkomponenten av färgen visas som röd, mättnadskomponenten som grön, och ljusintensitetskomponenten som blå. Detta för ge en bild av hur HSV-systemet fungerar.

### 2. Borttagning av brus
Av naturliga skäl vill vi få bilden mindre brusig. Under "Dokumentation" finns information om de anrop som går att göra. Använd något av dessa för att göra bilden mindre brusig.

### 3. Relevant färgintervall

Vi vill nu ta bort alla färger som inte ingår i objektet vi vill detektera. Använd ytterliggare ett anrop för att uppnå detta. Experimentera med olika HSV-värden tills önskad effekt är uppnådd.

### 4. Filtrera bort små detaljer
Vi kommer nu se att många detaljer i bilden som ej ingår i objektet hängt med även efter filtreringen av färg. Dessa detaljer är inget vi vill ha med oss när vi vill identifiera var bollen befinner sig på skärmen. En fördel för oss är dock att dessa detaljer ofta är små (förutsatt att din tröja nu inte har samma färg som objektet i fråga). Hitta ett sätt att med de återstående funktionerna filtrera bort dessa små områden från den slutgiltiga bilden.

Vi kommer nu se att många detaljer i bilden som ej ingår i objektet hängt med även efter filtreringen av färg är gjord. Dessa detaljer är inget vi vill ha med oss när vi vill identifiera var bollen befinner sig på skärmen. En fördel för oss är dock att dessa detaljer ofta är små (förutsatt att din tröja nu inte har samma färg som objektet i fråga). Hitta ett sätt att filtrera bort dessa små områden med hjälp av två funktioner i dokumentationen som du inte använt ännu.

### 5. Fruktmarkering
Nu vill vi slutligen ringa in frukten på skärmen, detta kommer ske med anropen `image.min_enclosing_circle(min_radius)` och `image.draw_cicle(x, y, r)`.

### 6. Extra (frivillig i mån av tid och tidigare programmeringskunskaper)
Om du har någon form av tidigare programmeringskunskaper och extra tid över får ni nu chansen att lägga till en svans som följer efter frukten. Man vill naturligt att längden på svansen ska vara begränsad (för att den till slut inte ska fylla skärm och arbetsminne). 

Detta kan ni göra på två sätt, antingen genom att använda en lista där man lagrar cirkelns mittpunkter över tid och för varje ny mittpunkt lägger till denna i listan och tar bort listans äldsta element. Till detta använder vi anropet `image.draw_trail(trail)`.

Den första lösningen som beskrevs kan dock resultera i prestandaproblem då listans innehåll behöver kopieras en gång för varje ny mittpunkt som läggs till. Detta kommer av hur Python implementerar listor. Man kan istället lösa problemet genom att använda sig av en så kallad [ringbuffer](https://en.wikipedia.org/wiki/Circular_buffer). Om ni känner er någorlunda bekväma i Python och med modulo-räkning kan istället välja denna lösning. Till detta använder vi anropet `image.draw_trail(trail, start_index)`.

## Dokumentation

### Visa bild
{% highlight python %}
image.show()
{% endhighlight %}
*Visa bilden efter de transformationer som gjorts på raderna över.*

### Oskärpa
{% highlight python %}
image.blur(n)
{% endhighlight %}
*Lägger på oskärpa på bilden. Ju högre värde på `n` desto större oskärpa!*
*`n` väljs lämpligen till ett värde mellan `0` och `50`.*

### Färgintervall
{% highlight python %}
image.in_range(lower, upper)
{% endhighlight %}
*De pixlar utanför färgintervallet avgränsat av `upper` och `lower` sätts till vitt och de utanför intevallet sätts till svart.*

Exempel:
Ta bort alla färger mellan `(3, 100, 2)` och `(35, 255, 255)`. Dessa färger är skriva i HSV-färgsystemet.
{% highlight python %}
image.in_range((3, 100, 2), (35, 255, 255))
{% endhighlight %}

### Minsta instängande cirkel
{% highlight python %}
image.min_enclosing_circle(min_radius)
{% endhighlight %}
*Hitta den minsta minsta cirkel med radie större än `min_radius` som stänger in någon av de vita områdena.*

Exempel:
Tilldela variablerna `x`, `y` och `r` med x-koordinat, y-koordinat respektive radien av den minsta instängande cirkeln med radien 40.
{% highlight python %}
x, y, r = image.min_enclosing_circle(40)
{% endhighlight %}

### Rita cirkel
{% highlight python %}
image.draw_circle(x, y, r)
{% endhighlight %}
*Rita en cirkel runt vid koordinaterna `x` och `y` med radien `r`*

### Rita svans (lista)
{% highlight python %}
image.draw_trail(trail)
{% endhighlight %}
*Rita en avsmalnande svans där funktionsargumentet trail är en lista innehållande koordinatpar*

### Rita svans (ringbuffer)
{% highlight python %}
image.draw_trail(trail, start_index)
{% endhighlight %}
*Rita en avsmalnande svans där funktionsargumentet `trail` är en ringbuffer innehållande koordinatpar och `start_index` är det index där ringbuffern börjar*

### Morfologi
![](../../assets/images/cv_original.png "Orginal")

*Originalbild.*

#### Erode
{% highlight python %}
image.erode(n)
{% endhighlight %}
*Krymper vita delar i bilden. Ju större värde på `n` desto större krympning.*
*`n` väljs lämpligen till ett värde mellan `0` och `50`.*

![](../../assets/images/cv_erode.png "Erode")

*Bild efter erode.*

#### Dilate
{% highlight python %}
image.dilate(n)
{% endhighlight %}
*Expanderar vita delar i bilden. Ju större värde på `n` desto större expansion.*
*`n` väljs lämpligen till ett värde mellan `0` och `50`.*

![](../../assets/images/cv_dilate.png "Dilate")

*Bild efter dilate.*
