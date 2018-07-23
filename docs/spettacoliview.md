# Spettacoli-view  

<hr>  

##

- Il componente "**spettacoli-view**" è la pagina del dettaglio per gli spettacoli (* es. produzioni*).  

##

- La pagina è composta da: il titolo con una classe *html* (```class="titolo-foglia white"```) , i [metadati](metadati.md), le [relazioni](related.md) e da una [locandina](locandina.md) per quell'elemento.  

##

- La locandina verrà importata, nel codice *.html*, attraverso la libreria ```<aui-locandina>```:  

```html
<aui-locandina :relateds="relateds" class="pb-2 d-none d-md-block"></aui-locandina>
```
##

- Richiama i componenti: [metadati](metadati.md), [related](related.md) e [locandina](locandina.md).  

```java
import AuiMetadati from '../metadati/metadati.vue'
import AuiRelated from '../related/related.vue'
import AuiLocandina from '../locandina/locandina.vue'
```
##

- Prende in input le proprietà ```items``` e ```relateds```.  

```java
props: [
    'items',
    'relateds'
],
```

### Il metodo ```relSplitted()```:  
riprende le proprietà dell’elemento e divide le entità (```items```) dalle relazioni (```relateds```), permettendo di modificare separatamente gli elementi senza che vi siano modifiche anche nelle loro relazioni.  

```java
relSplitted () {
    return util.splitRelation(this.relateds)
}
```