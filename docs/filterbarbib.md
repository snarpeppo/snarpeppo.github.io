# Filterbarbiblioteca  

<hr>  

##

- Il componente "**filterbarbiblioteca**" sono i filtri della sezione *Biblioteca*.  

### La funzione ```generaOptions()```:  
 prende come parametri una ```lista``` (```filtri```) e una ```tipologia``` (```tipologiaObject``` o ```Autore```) passate dal metodo ```data()```.  
 A seconda della tipologia, ricerca tra tutti gli elementi della lista passata (tra tutti i *filtri*) quelli della stessa tipologia e ne ritorna un elenco (la variabile ```items```) ordinato per nome (*ordine alfabetico*).  

```java
function generaOptions (lista, tipologia) {
	let items = _.find(lista, item => item.data.path === tipologia)
	return items ? _.chain(items.children).map(item => item.data).orderBy('name').value() : []
}
```
##

### La funzione ```selezionaOptions()```:  
 prende come parametri la raccolta delle ```options``` (```generiOptions``` e ```autoriOptions```) e i filtri selezionati.  
 Restituisce il primo elemento nella collezione ```options``` che abbia un *id* corrisponde all’*id dei filtri selezionati* (```child.id```), se è presente restituirà *```true```* e quindi l’elemento.  

```java
function selezionaOptions (options, selezionati) {
	return _.find(options, (item) => {
		return _.some(selezionati, child => child.id === item.id)
	})
}
```
##

### Il ```metodo data()```:  
 richiama al suo interno,  due volte, la funzione ```generaOptions```, passandogli la lista di filtri e le tipologie: ```tipologiaObject``` e ```Autore```; ciascuna delle due volte, in cui viene richiamata, assegnerà il parametro che essa ritorna a una nuova variabile (```generiOptions```, ```autoriOptions```).  
 Il metodo richiama, inoltre, la funzione ```selezionaOptions``` passandogli le due variabili/opzioni ottenute precedentemente: ```generiOptions``` e ```autoriOtions``` e, i ```filtriSelezionati```. Assegna quindi, ciascuna delle due volte in cui viene richiamata, il parametro che essa ritorna a una nuova variabile (```genere```, ```autore```).  
 Il metodo restituisce infine queste quattro variabili (gli elenchi di filtri per genere e autore e, il genere e l’autore selezionati dall’elenco) e le variabili ```soggettoInterno``` e ```titoloInterno```, a cui vengono assegnate, rispettivamente, il soggetto e il titolo presi in input perché inseriti manualmente dall’utente.  

```java
data () {
	let generiOptions = generaOptions(this.filtri, '/tipologiaObject')
	let autoriOptions = generaOptions(this.filtri, '/Autore')
	let genere = selezionaOptions(generiOptions, this.filtriSelezionati)
	let autore = selezionaOptions(autoriOptions, this.filtriSelezionati)
	return{
		generiOptions,
		autoriOptions,
		genere,
		autore,
		soggettoInterno: this.soggetto,
		titoloInterno: this.titolo
	}
},
```
##

### Il metodo ```filtra()```:  
 richiama, come ascoltatore, il metodo ```setAdvSearch``` e gli passa come parametri: ```genere```, ```autore```, ```soggetto``` e ```titolo```.  

```java
methods: {
	filtra (){
		this.$emit('setAdvSearch', {
			genere: this.genere,
			autore: this.autore,
			soggetto: this.soggettoInterno,
			titolo: this.titoloInterno
		})
	}
}
```