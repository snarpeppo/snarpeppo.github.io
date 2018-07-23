# Related  

<hr>  

##

- Il componente "**related**" è una classe *html* ```class="related row"``` che contiene, sotto forma di "*card*" con preview o di elenco, tutte le opere, le immagini, i video, l'autore... collegate tramite una relazione a un elemento.  

<center>
![related card delle relazioni](imgsub/related/related_card.png)
![related card delle relazioni](imgsub/related/related_elenco.png)
</center>

##

- Richiama il componente: [card-view](cardview.md).  

```java
import AuiCard from '~/components/item-view/card-view/card.vue'
```
##

- Prende in input le proprietà ```relateds``` e ```view```.  

```java
props: [
    'relateds',
    'view'
]
```