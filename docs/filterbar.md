# Filterbar  

<hr>  

##

- Il componente "**filterbar**" sono i filtri della sezione *Archivio*.  

##

- Clonando il datepicker in filtriData, permette di aggiungere un filtro per range di date già predisposto dal framework Vue.js.  

```java
datepicker: _.clone(this.filtriData),
```
### Il metodo ```filtriConSelezione()```:  
 eseguirà, per tutti i filtri dell’*Archivio*, una funzione che assegnerà ad ogni figlio, del filtro in analisi, la proprietà ```.selected```, questa dirà che il filtro è già stato selezionato e restituirà a ```filtriConSelezione``` tutti i filtri con il campo ```.selected``` aggiunto.  

```java
filtriConSelezione (){
	return _.map(this.filtri, (filtro) => {
		filtro.children = _.map(filtro.children, (child) => {
			child.selected = Boolean(_.find(this.filtriSelezionati, item => item.id === child.data.it))
			return child
		})
		return filtro
	})
},
```
##

### Il metodo ```filtroMedia()```:  
 ricerca gli elementi che hanno, come valore della proprietà ```name```, ```‘Con media’```, se esistono tali elementi ritorna una variabile *booleana* a *```true```*.  

```java
filtroMedia (){
	return Boolean(_.find(this.filtriSelezionati, {'name': 'Con media'}))
}
```
##

###Il metodo getMedia():  
 controlla se il filtro selezionato ha elementi con media al loro interno allora mantiene il filtro nell’elenco dei filtri (```setFiltro```), altrimenti rimuove quel filtro dall’elenco (```removeFiltro```).  

```java
getMedia (e){
	if(e.target.checked){
		this.$emit('setFiltro', { 'id': '1a1f0b26aed8e2066e42b02e13dd10f4', 'name': 'Con media' })
	}else {
		this.$emit('removeFiltro', { 'id': '1a1f0b26aed8e2066e42b02e13dd19f4', 'name': 'Con media' })
	}
},
```