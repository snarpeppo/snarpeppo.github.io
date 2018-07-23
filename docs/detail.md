# Detail  

<hr>  

## Descrizione generale  
Il componente “**detail**” contiene al suo interno altri componenti: [metadati](metadati.md), [related](related.md) e [spettacoli-view](spettacoliview.md), che contiene al suo interno il componente [locandina](locandina.md).  
È la pagina in cui si viene reindirizzati quando si seleziona un elemento della pagina [Cerca](cercapg.md) o dalle altre pagine del menù.  
Esso mostra il nome dell’elemento, una gallery di immagini, una sua descrizione ([metadati](metadati.md)) e gli elementi ad esso collegati ([related](related.md)).  
Se si apre un elemento degli spettacoli, viene visualizzata la pagina dell’elemento con una descrizione ([metadati](metadati.md)), e gli elementi correlati sotto forma di *card* e a lato un immagine della locandina dello spettacolo ([spettacoli-view](spettacoliview.md)/[locandina](locandina.md)) con sotto un elenco degli elementi correlati ([related](related.md)).  

## Comportamenti specifici  
Importa i componenti: [related](related.md), [gallery](gallery.md) e [metadati](metadati.md).  

```java
import AuiRelated from './related/related.vue'
import AuiGallery from './../gallery/gallery.vue'
import AuiMetadati from './metadati/metadati.vue'
```
##

### Il metodo ```imagesList()```:  

```java
imagesList () {
	return _.chain(this.item.representations)
	.filter(e =>  e.mimetype === 'image/jpeg')
	.map(e => {
		return {
			'url': e.url,
			'title': e.title
		}
	})
	.value()
},
```

<div id="elenco">
1.	richiamando la funzione <code>_.chain(this.item.representations)</code> [...] <code>.value()</code> verranno restituiti tutti gli elementi solo se saranno in formato .jpeg e che quindi saranno delle immagini (<code>e.mimetype === ‘image/jpeg’</code>).  
</div>
<div id="elenco">
2. richiamando la funzione <code>.map</code>, a tutti gli elementi della lista di immagini, verranno riportati il corrispondente URL e il titolo.
</div>

##

### Il metodo ```docList()```:  
 richiamando la funzione ```_.chain(this.item.representations)``` [...] ```.value()```, restituirà tutti gli elementi che saranno in un formato diverso da *.jpeg*  e che quindi saranno dei documenti (```e.mimetype !== ‘image/jpeg’```).  

```java
docList() {
	return _.chain(this.item.representations)
	.filter(e => e.mimetype !== 'image/jpeg')
	.value()
},
```
##

### Il metodo ```relSplitted()```:  

<div id="elenco">
1. riprende le proprietà dell’elemento e divide le entità (<code>items</code>) dalle relazioni (<code>relateds</code>), permettendo di modificare separatamente gli elementi senza che vi siano modifiche anche nelle loro relazioni.
</div>

```java
relSplitted () {
	return util.splitRelation(this.relateds)
}
```
```java
props: [
	'item',
	'relateds'
],
```
<div id="elenco">
2. richiamando <code><i>service/util.js</i></code> le entità vengono ordinate secondo una specifica disposizione predisposta.
</div>

```java
service.splitRelation = (relations) => {
	let splittedRelations = {}
	let orderEntities =['Autore', 'Autore_secondario', 'Regia', 'Scene', 'Costumi', 'Musiche', 'Interprete', 'Luoghi']
}
```
<div id="elenco">
3. attraverso il codice <i>.html</i> mostra le relazioni divise come oggetti (<code>relSplitted.objects</code>) verranno mostrate come delle card con immagini; quelle divise come entità (<code>relSplitted.entities</code>) verranno mostrate come un elenco che seguirà l’ordine imposto dal file <i>util.js</i>.
</div>

```html
<aui-related v-if="relSplitted.objects" :relateds="relSplitted.objects" :view="'images'"></aui-related>
<aui-related v-if="relSplitted.entities" :relateds="relSplitted.entities"></aui-related>
```