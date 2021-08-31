# Veränderung der wahrgenommenen Bildqualität durch Presets

***

## Seminar Visuelle Wahrnehmung und Bildqualität SoSe 2021
### TU Berlin


Katharina Wohlrab und Anne Gabler


```python
import pandas as pd    # module to work with data in DataFrames.
import seaborn as sns  # module to plot DataFrames in an easy way
import matplotlib.pyplot as plt

sns.set_context('talk')

import scipy 
import statsmodels.api as sm  
from statsmodels.stats.multicomp import MultiComparison
```

## 1. Einleitung
***



Presets sind dafür gedacht, Fotos mit einem Klick so zu bearbeiten, dass die Bildqualität und das Gefallen der Bilder signifikant steigt. Ein Preset ist eine Reihe voreingestellter Einstellungen, die sich auf jedes Bild anwenden lassen. Unsere Forschungsfrage war, ob die Bearbeitung von Bildern mit sogenannten Presets einen positiven Einfluss auf die subjektiv wahrgenommene Bildqualität hat und ob dies abhängig von den Bildmotiven ist. 
Um diese Frage zu beantworten, haben wir ein Preset für eine bestimmte Bildkategorie in 4 Intensitäten auf Bilder verschiedener Kategorien gelegt und die Bildqualität über den Mean Opinion Score bewerten lassen. 
Dabei haben wir folgende Hypothesen geteset: 

1. Die subjektiv wahrgenommene Bildqualität kann durch die Bearbeitung mit Presets verbessert werden, abhängig von ihrem Bildinhalt.

2. Ein Preset für eine bestimmte Bildkategorie wirkt sich bei Anwendung auf Bilder anderer Kategorien negativ auf die subjektiv  wahrgenommene Bildqualität aus.  


## 2. Experimentelles Design
***

Zur Beantwortung der Forscungsfrage haben wir jeweils 5 Bilder aus den Kategorien Landschaft, Portrait und Produkt ausgewählt und das Preset in den Intensitäten 0%, 50%, 100% und 150% angewendet. 0% entspricht dabei dem originalen Bild, wobei 150% dem Bild mit 100% entsprechen, auf das erneut das Preset mit einer Intenstität von 50% angewendet wurde. 

Das Preset ist für die Kategorie Landschaft entwickelt worden. Zur besseren Veranschaulichung der Wirkung des Presets, haben wir das Histogramm ausgewertet und sind zu dem Ergebnis gekommen, dass das ausgewählte Preset im Bereich Landschaft besonders die Blautöne intensiviert und die Rottöne abschwächt.

![Preset_Auswertung](AA.png)


Die Anwendung des Presets erfolgte mittels der Software Photoshop. 

Die folgenden Bilder entsprechen unseren Stimuli, welche sich aus 3 Kategorien x 5 Bilder x 4 Preset-Intensitäten zu 60 Stimuli ergeben: 

### Kategorie Landschaft

| Bild | 0% | 50% | 100% | 150% | 
| :-: | :-: | :-: | :-: | :-: |
| A | ![A-1](1a.jpg) | ![A-2](1b.png) | ![A-3](1c.png) | ![A-4](1d.png) |
| B | ![B-1](2a.jpg) | ![B-2](2b.png) | ![B-3](2c.png) | ![B-4](files/2d.png) |
| C | ![C-1](3a.jpg) | ![C-2](3b.png) | ![C-3](3c.png) | ![C-4](files/3d.png) |
| D | ![D-1](4a.jpg) | ![D-2](4b.png) | ![D-3](4c.png) | ![D-4](files/4d.png) |
| E | ![E-1](2a.jpg) | ![E-2](2b.png) | ![E-3](2c.png) | ![E-4](files/2d.png) |

### Kategorie Produkt

| Bild | 0% | 50% | 100% | 150% | 
| :-: | :-: | :-: | :-: | :-: |
| F | ![F-1](6a.jpg) | ![F-2](6b.png) | ![F-3](6c.png) | ![F-4](6d.png) |
| G | ![G-1](7a.jpg) | ![G-2](7b.png) | ![G-3](7c.png) | ![G-4](7d.png) |
| H | ![H-1](8a.jpg) | ![H-2](8b.png) | ![H-3](8c.png) | ![H-4](8d.png) |
| I | ![I-1](9a.jpg) | ![I-2](9b.png) | ![I-3](9c.png) | ![I-4](9d.png) |
| J | ![J-1](10a.jpg) | ![J-2](10b.png) | ![J-3](10c.png) | ![J-4](10d.png) |

### Kategorie Portrait

| Bild | 0% | 50% | 100% | 150% | 
| :-: | :-: | :-: | :-: | :-: |
| K | ![K-1](11a.jpg) | ![K-2](11b.png) | ![K-3](11c.png) | ![K-4](11d.png) |
| L | ![L-1](12a.jpg) | ![L-2](12b.png) | ![L-3](12c.png) | ![L-4](12d.png) |
| M | ![M-1](13a.jpg) | ![M-2](13b.png) | ![M-3](13c.png) | ![M-4](13d.png) |
| N | ![N-1](14a.jpg) | ![N-2](14b.png) | ![N-3](14c.png) | ![N-4](14d.png) |
| O | ![O-1](15a.jpg) | ![O-2](15b.png) | ![O-3](15c.png) | ![O-4](15d.png) |


Wir ließen die Versuchsteilnehmer_innen aufgrund ihres Empfindens die Bildqualität in 5 verschiedenen Stufen bewerten. Von 1 - sehr schlechte Qualität, hinzu 5 - sehr gute Qualität. Dies haben wir mittels Mean Opinion Score ausgewertet. Die Umfrage veranstalteten wir über die Plattform surveymonkey. 
Die Umfrage wurde von neun Versuchsteilnehmer_innen bearbeitet, welche keine Kenntnis über die Bearbeitung der Bilder sowie keine bekannte Farbsehschwäche hatten. 


## 3. Ergebnisse
***


```python
#einlesen der Daten unserer neun Versuchspersonen
#für jede Versuchsperson existiert eine eigene .csv Datei

df1 = pd.read_csv('P1.csv')
df1['observer'] = 'Person1'     
df2 = pd.read_csv('P2.csv')
df2['observer'] = 'Person2'     
df = pd.concat((df1, df2))       
df1 = pd.read_csv('P3.csv')
df1['observer'] = 'Person3'          
df = pd.concat((df, df1))        
df1 = pd.read_csv('P4.csv')
df1['observer'] = 'Person4'          
df = pd.concat((df, df1))        
df1 = pd.read_csv('P5.csv')
df1['observer'] = 'Person5'          
df = pd.concat((df, df1))        
df1 = pd.read_csv('P6.csv')
df1['observer'] = 'Person6'          
df = pd.concat((df, df1))        
df1 = pd.read_csv('P7.csv')
df1['observer'] = 'Person7'          
df = pd.concat((df, df1))        
df1 = pd.read_csv('P8.csv')
df1['observer'] = 'Person8'          
df = pd.concat((df, df1))        
df1 = pd.read_csv('P9.csv')
df1['observer'] = 'Person9'          
df = pd.concat((df, df1))        



```

Die folgenden Diagramme zeigen die Bewertungen der neun Versuchsteilnehmer_innen für jedes Bild. 
Die Auswertung erfolgt mittels Balkendiagrammen und dem Konfidenzintervall.

### Kategorie Landschaft

Bei den fünf Bildern der Kategorie Landschaft lässt sich beobachten, dass alle Konfidenzintervalle überlappen. Daher lässt sich kein statistisch signifikanter Unterschied zwischen den Bewertungen erkennen. 


```python
variable = 'Landschaft'
d= df[df['Kategorie'] == variable]
# %%  Using small multiples to visualize data from all pictures in one figure 
g = sns.catplot(x='Bearbeitung', y='Bewertung', data=d, 
                col='Bild', col_wrap = 3, kind='bar', ci=95, height=4,
                palette='Greens')
g.set_ylabels('Qualität')
g.set_xlabels('Bearbeitungsgrad')
g.set_titles('{col_name}')
g.set(ylim = (0,5))
```




    <seaborn.axisgrid.FacetGrid at 0x291e8e3f640>




    
![png](output_7_1.png)
    


### Kategorie Produkt

Auch bei den fünf Bildern der Kategorie Produkt überlappen alle Konfidenzintervalle, womit es auch hier keinen statisch signifikanten Unterschied zwischen den Bewertungen gibt.


```python
variable = 'Produkt'
d= df[df['Kategorie'] == variable]
# %%  Using small multiples to visualize data from all pictures in one figure 
g = sns.catplot(x='Bearbeitung', y='Bewertung', data=d, 
                col='Bild', col_wrap = 3, kind='bar', ci=95, height=4,
                palette='Greens')
g.set_ylabels('Qualität')
g.set_xlabels('Bearbeitungsgrad')
g.set_titles('{col_name}')
g.set(ylim = (0,5))
```




    <seaborn.axisgrid.FacetGrid at 0x291e8f1d520>




    
![png](output_9_1.png)
    


### Kategorie Potrait

Die Beobachtung, dass alle Konfidenzintervalle überlappen, wird auch bei den Bildern der Kategorie Portrait sichtbar. 
Somit lässt sch auch hier kein statistisch signifikanter Unterschied erkenen. 



```python
variable = 'Portrait'
d= df[df['Kategorie'] == variable]

g = sns.catplot(x='Bearbeitung', y='Bewertung', data=d, 
                col='Bild', col_wrap = 3, kind='bar', ci=95, height=4,
                palette='Greens')
g.set_ylabels('Qualität')
g.set_xlabels('Bearbeitungsgrad')
g.set_titles('{col_name}')
g.set(ylim = (0,5))
```




    <seaborn.axisgrid.FacetGrid at 0x291e91fc100>




    
![png](output_11_1.png)
    


### Alle Bilder nach Kategorie

Bei der aggregierten Betrachtung aller Bilder einer Kategorie zeigen sich ebenfalls sich überlappende Konfidenzintervalle. Hier zeigt der t-test jedoch ein statistisch siginifkanter Unterschied zwischn den Bildern mit der Bearbeitungsstufe 0.5 und 1.5 in der Kategorie Portrait. 


```python
g = sns.catplot(x='Bearbeitung', y='Bewertung', data=df, 
                col='Kategorie', col_wrap = 3, kind='bar', ci=95, height=4,
                palette='Greens')
g.set_ylabels('Qualität')
g.set_xlabels('Bearbeitungsgrad')
g.set_titles('{col_name}')
g.set(ylim = (0,5))
```




    <seaborn.axisgrid.FacetGrid at 0x291e95044c0>




    
![png](output_13_1.png)
    


### Alle Bilder

Auch bei der aggregierten Betrachtung aller Bilder zeigen sich die überlappenden Konfidenzintervalle. Ein statistsch signifikanter Unterschied zwischen den einzelnen Bearbeitungsstufen liegt auch hier nicht vor.


```python
g = sns.catplot(x='Bearbeitung', y='Bewertung', data=df,
                kind='bar', ci=95, errwidth=2,
                palette='Greens')
g.set_ylabels('Qualität')
g.set_xlabels('Bearbeitungsgrad')
g.set(ylim = (0, 5))
```




    <seaborn.axisgrid.FacetGrid at 0x291e98bc070>




    
![png](output_15_1.png)
    


## 4. Diskussion
***

Auf Grundlage der Versuchsergbnisse lassen sich keine Tendenzen erkennen, ob das Preset die subjektiv wahrgenommene Bildqualität verbessert oder verschlechtert. Es lässt sich auch nicht beobachten, dass sich die Anwendung des Presets für eine bestimmte Kategorie auf eine andere Kategorie, negativ auf die subjektiv wahrgenomene Bildqualität auswirkt. 

Diese Ergebnisse stimmen nicht mit unseren Erwartungen überein. 

Aufgrund der kalten Atmosphäre, welches das Preset schafft, werden gerade die Bilder der Kategorie Portrait unvorteilhafter. So erscheinen Falten tiefer und die Gesichter wirken älter. 
Allerdings hat diese Beobachtung nichts mit der Bildqualität zu tun, sondern mit der Vorteilhaftigkeit des Presets für die Motive. Damit ergeben sich neue mögliche Fragestellungen. 


### Mögliche Probleme

Die Diskrepanz zwischen den Ergebnissen und unseren Erwartungen könnte jedoch auch an der ohnehin hohen Bildqualität unserer gewählten Bilder liegen. Außerdem wurden die ausgewählten Bilder mit hoher Wahrscheinlichkeit bereits ansprechend bearbeitet. Fraglich ist daher, ob das Preset bei Anwendung auf unbearbeitete Fotos bezeihungsweise "Amateuraufnahmen" eine andere Wirkung auf die subjekt wahrgenommene Bildqualität aufweist. 

Auch die Anzahl an Versuchteilnehmer_innen ist mit neun Personen recht gering. Eine Befragung weiterer Personen könnte die Ergebnisse klarer werden lassen. 

Die Wahl des Presets und die Auswahl der Bilder ist ebenfalls maßgeblich für die Ergebnisse dieses Versuchs. Mit einem anderen Preset oder anderen Motiven beziehungsweise Bildkategorien könnten unter Umständen andere Ergebnisse erzielt werden.


### Offene Fragen

Wie bereits diskutiert ergeben sich Möglichkeiten für neue Fragestellungen. So könnte statt nach der Bildqualiät besser nach dem Gefallen der Bearbeitung des Bildes gefragt werden. Auch die Frage nach der Veränderung der Stimmung durch das Preset wäre denkbar. Damit ändert sich auch die Aufgabenstellung für die Versuchsteilnehmer_innen. 







```python

```


```python

```
