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
##

Imposta come titolo della pagina “*Teatri e compagnie*”.  

```java
head() {
	return{
		title: 'Stagioni'
  }
}
```