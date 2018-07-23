# Browse  

<hr>  

## Descrizione generale
Il componente “**browse**” contiene al suo interno altri componenti:  

 - [box](box.md)

 - [browsebar](browsebar.md)

 - [browsefilter](browsefilter.md)

 - [list](list.md)

## Comportamenti specifici  
Importa i componenti: [list](list.md), [box](box.md), [browsefilter](browsefilter.md) e [browsebar](browsebar.md).  

```java
import AuiList from './list/list.vue'
import AuiBox from './box/box.vue'
import AuiBrowsefilter from './browsefilter/browsefilter.vue'
import AuiBrowsebar from './browsebar/browsebar.vue'
```
##

Restituirà a ```filteredResult()``` la variabile ```tmp``` contenente tutti i gli elementi della proprietà ```result```, clonati ricorsivamente e in modo superficiale (```_.cloneDeep```).  
Assegnerà nel file .html ```filteredResult()``` in modo che gli elementi risultanti vengano visualizzati sotto forma di una “*card*” o di un *elenco*.  

```java
computed: {
	filteredResult (){
		let tmp = _.cloneDeep(this.result)
		if (this.autocomplete){
			tmp = _.map(tmp, e => {
				e.items = _.filter (e.items, i =>{
					return new RegExp (this.autocomplete, 'i').test(i.label)
				})
				return e	
			})
		}
		this.totale = _.reduce(tmp, (group, total) => {
			return group + _.size(total.items)
		}, 0)
		return tmp
	}
},
```
##

```html
<aui-box :data="filteredResult" v-if="view === 'box'"> </aui-box>
<aui-list :data="filteredResult" v-if="view === 'list'"> </aui-list>
```
##

### Il metodo ```setFilter()```:  
 aggiorna la *query* e, quindi, gli elementi risultanti nella pagina in base alla selezione di un filtro, grazie al metodo ```openSelect()``` per la pagina [Documenti e immagini](docimg.md) o, per *data* o *lettera alfabetica* nel componente [sticky](sticky.md) delle pagine: [Il Dramma](dramma.md), [Persone](persone.md), [Spettacoli](spettacoli.md), [Stagioni](stagioni.md) e [Teatri e compagnie](teatrico.md).  

```java
setFilter (filtro){
	if (this.filters){
		var currentFilter = this.$route.query.filtro || this.filters[0]._id
		if(currentFilter !== filtro._id) {
			this.aggiornaQuery({
				filtro: filtro._id === 'Tutti' ? '' : filtro._id
			})
		}
	}
},
```
##

### I metodi ```openSelect()``` e ```closeSelect()```:  
 al click della rispettiva icona, aprono e chiudono un menù di filtri a selezione, solamente nella pagina [Documenti e immagini](docimg.md).  

```java
openSelect ($event){
	var el = $($event.target)
	if (el.is('span.selected-tag') || el.is('i.open-indicator')){
		this.$refs['sselect'].open = true
	}
},
closeSelect(){
	this.$refs['sselect'].open = false
}
```