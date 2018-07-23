# Dettaglio (_table)  

<hr>  

## Descrizione generale  
La pagina “**_table**” è la pagina di dettaglio di un elemento selezionato, sia dall’*Archivio*, sia dalla *Biblioteca*.   
Mostra il nome e il tipo dell’elemento selezionato, come titolo, una o più immagini (gallery), una descrizione, i documenti e gli elementi collegati (autore, spettacoli…) e, per gli spettacoli, mostra una locandina dello spettacolo al posto della gallery.  

## Comportamenti specifici  
La pagina è composta dall’unione dei componenti: [detail](detail.md) e [spettacoli-view](spettacoliview.md).  


```java
import AuiDetail from '~/components/detail/detail.vue'
import AuiDetailSpettacoli from '~/components/detail/spettacoli-view/spettacoli-view.vue'
```

##

Esegue la funzione ```asyncData``` che permette di gestire le operazioni asincrone prima di impostare i dati del componente.  
Recupera i dati del componente [detail](detail.md), aspettando finché non vengono mandate allo *store* le azioni del metodo ```getDetail()``` del componente e li restituisce passandoli alla variabile ```detail```.  
Assegnerà alle proprietà *id* e *table* le corrispondenti proprietà di ciascun parametro in input.  


```java
async asyncData ({store, params, error}) {
	let detail = await store.dispatch('detail/getDetail', {
		id: params.id,
		table: util.getTable(params.table)
	}) 
}
```


##

Controlla, se non ci sono metadati in ```detail``` mostra il messaggio d’errore: “*Dati non trovati*”.  

```java
if (!detail) {
	error ({statusCode: 404, message: 'Dati non trovati'})
	return
}
```

##

Recupera i dati del componente [detail](detail.md), aspettando finché non vengono mandate allo *store* le azioni del metodo ```getRelated()``` del componente e li restituisce passandoli alla variabile ```relateds```.  
Assegna alle proprietà *table* e *id*, rispettivamente, il table e l’id del componente [detail](detail.md).  

```java
let relateds = await store.dispatch('detail/getRelateds', {
	table: detail.table,
	id: detail.id
})
```
##

```java
detail.category = util.getCategory(detail.table, detail.type_id)
return{
	detail, relateds
}

```

##

Imposta come titolo della pagina il titolo dell’elemento selezionato e, prende l’URL della prima immagine della sua gallery e la usa per lo sfondo del titolo.  


```java
head () {
 return{
 	title: this.detail.preferred_label,
 	meta: [
 	{
 		'hid': 'og:title',
 		'property': 'og:title',
 		'content': this.detail.preferred_label
 	},
 	{
 		'hid': 'og:image',
 		'property': 'og:image',
 		'content': _.get(this.detail, 'primaryImg.url.mediumlarge')
 	}
   ]
 }
}
```

