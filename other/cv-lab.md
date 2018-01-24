---
layout: separate-page
title: Datorseende med Python och OpenCV
author: William Sjöblom
permalink: /other/cv-lab/
---

# Datorseende med Python och OpenCV
## Teori
### HSV
Inom datorseende används ofta färgsystemet HSV istället för det vanligare systemet RGB. I RGB används för det mesta tre heltal mellan 0 och 255 som ofta skrivs i basen 16. I bas 16 alltså tre heltal mellan 0 och FF. Dessa heltal betecknar de röda, gröna respektive blå färgkomponententen (därav förkortningen RGB). I HSV beskrivs istället en färg av värden för kulör, mättnad och ljusintensitet (eller hue, saturation och value på engelska). Precis som tidigare beskrivs vardera av dessa värden av ett tal mellan 0 och 255.

Den största anledningen att färgsystem så som HSV är väl lämpade för datorseende är att denna skala separerar en färgs intensitet från dess faktiska färginnehåll. Detta gör det bland annat möjligt att på ett effektivt sätt beskriva färgintervall vilket vi snart kommer göra!

![alt text](https://henrydangprg.files.wordpress.com/2016/06/hsv_color_solid_cylinder_alpha_lowgamma.png?w=322&h=241)

_Färgsystemet HSV._

## Instruktioner
Denna laboration kommer göras i programspråket Python. Laborationen kommer inte kräva någon tidigare erfarenhet. Funktionerna vi kommer använda är förenklade varianter av de som programvaubiblioteket OpenCV innehåller. Om intresse att se vilka anrop som egentligen görs till OpenCV, se filen `lab.py`.

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


### 1. Borttagning av brus
Av flera skäl vill vi först få bilden mindre brusig. Under "Dokumentation" finns information om de anrop som går att göra. Använd något av dessa för att göra bilden mindre brusig.

### 2. Relevant färgintervall
Vi vill nu ta bort alla färger som inte ingår i objektet vi vill detektera. Använd ytterliggare ett anrop för att uppnå detta.

### 3. Filtrera bort små detaljer
Vi kommer nu se att många detaljer i bilden som ej ingår i objektet hängt med även efter filtreringen av färg. Dessa detaljer är inget vi vill ha med oss när vi ska identifiera var objektet befinner sig på skärmen. En fördel för oss är dock att dessa detaljer ofta är små (förutsatt att din tröja nu inte har samma färg som objektet i fråga). Hitta ett sätt att med de återstående funktionerna filtrera bort dessa små områden från den slutgiltiga bilden. (Använd de två resterande funktionerna som du ej använt i tidigare steg.)

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

### Morfologi
![alt text](https://docs.opencv.org/2.4/_images/Morphology_1_Tutorial_Theory_Original_Image.png)

*Originalbild.*

#### Erode
{% highlight python %}
image.erode(n)
{% endhighlight %}
*Krymper vita delar i bilden. Ju större värde på `n` desto större krympning.*
*`n` väljs lämpligen till ett värde mellan `0` och `50`.*

![alt text](https://docs.opencv.org/2.4/_images/Morphology_1_Tutorial_Theory_Erosion.png)

*Bild efter erode.*

#### Dilate
{% highlight python %}
image.dilate(n)
{% endhighlight %}
*Expanderar vita delar i bilden. Ju större värde på `n` desto större expansion.*
*`n` väljs lämpligen till ett värde mellan `0` och `50`.*

![alt text](https://docs.opencv.org/2.4/_images/Morphology_1_Tutorial_Theory_Dilation.png)

*Bild efter dilate.*
