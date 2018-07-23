# Searchbar  

<hr>  

##

Il componente "**searchbar**" è la barra di ricerca presente in ogni pagina del menù a 8 voci.  

##

Nel metodo della searchbar vengono richiamate due funzioni:  

### ```updateTags()```:  
La prima, ```updateTags()```, prende in input, come parametro, i ```tags``` inseriti manualmente dalla barra di ricerca e li immette nella ```queryTags```.  

```java
'methods': {
	'updateTags': function (tags) {
		this.$emit('updateTags', tags)
	},
```

```java
updateTags (tags) {
	this.queryTags = tags
	this.aggiornaQuery()
},
```

##

### ```selectedSort()```:  
La seconda, ```selectedSort()```, prende in input ```value```, come parametro, il quale verrà richiamato dalla funzione ```updateSort()``` che controllerà se l’opzione (```option```), passata come parametro, e il valore corrente dell’ordinamento (```value```) sono diversi dal valore dell’opzione; in questo caso darà all’ordinamento correnta il valore dell’opzione.  

```java
'selectedSort': function (value) {
	this.$emit('updateSort', value)
}
```

```java
updateSort (option) {
	if (option && this.orderBy.currentSort.value !== option.value) {
		this.orderBy.currentSort = option
		this.aggiornaQuery()
	}
},
```
