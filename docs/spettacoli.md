# Spettacoli  

<hr>  

## Descrizione generale  
La pagina “**spettacoli**”, contenente tutti gli elementi sotto forma di *elenco*, ordinati per stagione, appartenenti a quella categoria.  

## Comportamenti specifici  
La pagina è composta e richiama il componente: [browse](browse.md).  

```java
import AuiBrowse from '~/components/browse/browse.vue'
```
##

Esegue la funzione ```asyncData``` che permette di gestire le operazioni asincrone prima di impostare i dati del componente.  
Recupera i dati del componente ```browse-spettacoli```, aspettando finché non vengono mandate allo *store* le azioni del metodo ```getData()``` del componente e li restituisce passandoli alla variabile ```data```.  
Assegnerà alle proprietà ```total``` e ```result``` i rispettivi dati contenuti in ```data```.  

```java
async asyncData ({store, query}) {
	let data = await store.dispatch('browse-spettacoli/getData')
	return{
		total: data.total,
		result: data.result
	}
},
```

-Richiama la *query* dallo *store*:
```java
export const actions = {
	async getData (store){
		let total = 0
		let query = {
			'table': collection,
			'access': 1,
			'type_id.id': {$in: [include]}
		}
	}
}
```

##

Imposta come titolo della pagina “*Spettacoli*”.  

```java
head() {
	return{
		title: 'Spettacoli'
  }
}
```