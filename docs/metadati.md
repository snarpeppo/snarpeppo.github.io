# Metadati  

<hr>  

##

- Il componente "**metadati**" è un contenitore per la descrizione (lista di metadati, importata dal componente [metadatilist](metadatilist.md)), all'interno del dettaglio di un elemento.  

##

- Richiama i componenti: [metadataService](metadataService.md) e [metadatilist](metadatilist.md).  

```java
import MetaDataService from './metadataService'
import AuiMetaDatiList from './metadatalist/metadatilist.vue'
```
##

- Prende in input le proprietà ```metadati```, ```summary``` e ```schedaBreve```.  

```java
props: [
    'metadati',
    'summary',
    'schedaBreve'
],
```
##

- In ```metadati``` verrà importata, nel codice *.html*, la lista di metadati (```metadatiList```) attraverso la libreria ```<aui-meta-dati-list>```.  

```html
<div>
	<aui-meta-dati-list :data="metadatiList"></aui-meta-dati-list>
</div>
```
##

### Il metodo data():  

```java
data() {
const metService = new MetaDataService(this.metadati)
let tempMetadata = metService.clearEmptyMetadata().formatMetadati()

return {
	metadatiList: tempMetadata.reduceForSummary(this.summary)
  }
}
```  
<div id="elenco">
1. Ritorna la variabile <code>metadatiList</code>.
</div>
<div id="elenco">
2. Passa, come parametro, alla classe <code>MetaDataService</code> i <code>metadati</code>  e assegna il valore ritornato alla variabile <i>costante</i>  <code>metService</code>.  
</div>
<div id="elenco">
3. Alla variabile <code>metService</code> vengono applicati i metodi, del sub-componente <a href="metadataService.md">metadataService</a>, <code>clearEmptyMetadata()</code> e <code>formatMetadati()</code> e, il valore ritornato viene assegnato alla variabile <code>tempMetadata</code>.
</div>
<div id="elenco">
4. Alla variabile <code>tempMetadata</code> viene applicato il metodo, del sub-componente <a href="metadataService.md">metadataService</a>, <code>reduceForSummary()</code> a cui viene passato il parametro summary e, il valore ritornato viene assegnato alla variabile <code>metadatiList</code>.
</div>