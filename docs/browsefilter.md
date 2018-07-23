# Browsefilter  

<hr>  

##

- Il componente "**browsefilter**" è un filtro sticky per l’insieme di *date* o le *lettere alfabetiche* che, se selezionate, permettono lo scorrimento della pagina fino alla sezione corrispondente.  

##

- Richiama il componente: [sticky](sticky.md).  

```java
import AuiSticky from '~/components/sticky/sticky.vue'
```
##

- Prende in input le proprietà ```data``` e ```nav```.  

```java
props: [
	'data',
	'nav'
],
```
##

- Ritorna in output un nuovo array contenente gli elementi dell’oggetto ```chars``` in cui è richiamato ```[].concat.apply()```.  
Attraverso il comando ```String.fromCharCode```, per ogni posizione dell’array viene assegnata, alla variabile ```char```, una stringa in un carattere del *codice UTF-16* corrispondente alla somma di 65 alla corrente posizione nell’array.  

```java
chars () {
	return [].concat.apply([], Array(26))
	.map((e, i) => {
		let char = String.fromCharCode(i + 65)
		return{
			'val': char,
			'available': _.find(this.data, e => {
				return e.id === char && e.items.length > 0
			})
		}
	})
},
```
##

- Assegna ad una variabile ```startDecade``` un primo valore e ritorna in output un nuovo array contenente gli elementi dell’oggetto ```dates``` in cui è richiamato ```[].concat.apply()```.  
Per ogni posizione dell’array viene trasformata ```startDecade``` in una Stringa e assegnata ad una variabile ```decade```, successivamente assegnata alla proprietà ```val``` e, al valore corrente in ```startDecade``` viene aggiunta una decina.  

```java
dates () {
	let startDecade = 1920
	return [].concat.apply([], Array(11))
	  .map((e, i) => {
		let decade = String(startDecade)
		startDecade = startDecade + 10
		return {
			'val': decade,
			'available': _.find(this.data, e => {
				return e.id === decade && e.items.length > 0
			})
		}
	})
}
```
