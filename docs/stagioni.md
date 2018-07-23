# Stagioni  

<hr>  

## Descrizione generale  
La pagina “**stagioni**”, contenente tutti gli elementi sotto forma di *elenco*, ordinati per stagione, appartenenti a quella categoria.  

## Comportamenti specifici  

La pagina è composta e richiama il componente: [browse](browse.md).  

```java
import AuiBrowse from '~/components/browse/browse.vue'
```
##

Esegue la funzione ```asyncData``` che permette di gestire le operazioni asincrone prima di impostare i dati del componente.   
Recupera i dati del componente ```browse-stagioni```, aspettando finché non vengono mandate allo *store* le azioni del metodo ```getData()``` del componente e li restituisce passandoli alla variabile ```data```.  
Assegnerà alle proprietà ```total``` e ```result``` i rispettivi dati contenuti in ```data```.  

```java
async asyncData ({store, query}) {
	let data = await store.dispatch('browse-stagioni/getData')
	return {
		total: data.total,
		result:data.result
	}
},
```

-Richiama la *query* dallo *store*:
```java
export const actions = {
	async getData (store) {
		let collection = 'ca_occurrences'
		let filter = '192'
		let total = 0
		let response = await this.$axios.$post('aggregate', {
			'table': 'data_it',
			'query': [{
				'$match': {
					'table': collection,
					'access': 1,
					'type_id.id': filter
				}
			},
			{
				'$project': {
					id: '$id',
					label: '$preferred_label',
					table: '$table',
					filtri: '$filtri'
				}
			}]
		})
	}

}
```

##

Imposta come titolo della pagina “*Stagioni*”.  

```java
head() {
	return{
		title: 'Stagioni'
  }
}
```