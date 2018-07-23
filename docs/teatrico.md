# Teatri e compagnie  

<hr>  

## Descrizione generale  
La pagina “**teatri-e-compagnie**”, contenente tutti gli elementi sotto forma di *elenco*, ordinati in ordine alfabetico, appartenenti a quella categoria.  

## Comportamenti specifici  
La pagina è composta e richiama il componente: [browse](browse.md).  

```java
import AuiBrowse from '~/components/browse/browse.vue'
```
##

Esegue la funzione ```asyncData``` che permette di gestire le operazioni asincrone prima di impostare i dati del componente.  
Recupera i dati del componente ```browse-teatri```, aspettando finché non vengono mandate allo *store* le azioni del metodo ```getData()``` del componente e li restituisce passandoli alla variabile ```data```.  
Assegnerà alle proprietà ```total``` e ```result``` i rispettivi dati contenuti in ```data```.  

```java
async asyncData ({store, query}) {
	let data = await store.dispatch('browse-teatri/getData')
	return{
		total: data.total,
		result: data.result
	}
},
```

-Richiama la *query* dallo *store*:
```java
export const actions = {
	async getData (store) {
		var collection = 'ca_entities'
		var exclude = '83'
		let total = 0
		let query = {
			'table': collection,
			'access': 1,
			'type_id.id': {$nin: [exclude]}
		}
		let response = await this.$axios.$post('aggregate', {
			'table': 'data_it',
			'query': [{
				'$match': query
			},
			{
				'$project': {
					id: '$id',
					label: '$preferred_label',
					table: '$table'
				}
			}
	}
}
```

##

Imposta come titolo della pagina “*Teatri e compagnie*”.  

```java
head() {
	return{
		title: 'Stagioni'
  }
}
```