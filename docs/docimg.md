# Documenti e immagini  

<hr>  

## Descrizione generale  
La pagina “**documenti-e-immagini**”, contenente tutti gli elementi sotto forma di “*card*”, con preview e ordinati per stagione, appartenenti a quella categoria.  
È possibile filtrarli secondo: **Fotografia**, **Rassegna stampa**, **Manifesti e locandine**, **Programma**, **Schede di sala**, **Copione**, **Comunicato stampa** e **Serie**.  

## Comportamenti specifici  
La pagina è composta e richiama il componente: [browse](browse.md).  

```java
import AuiBrowse from '~/components/browse/browse.vue'
```
##

Esegue la funzione ```asyncData``` che permette di gestire le operazioni asincrone prima di impostare i dati del componente.  
Recupera i dati dal componente ```browse-documenti```, aspettando finché non vengono mandate allo *store* le azioni dei metodi ```getFiltri``` e ```getData``` del componente e li restituisce passandoli rispettivamente alle variabili ```filters``` e ```data```.  
Assegnerà alle proprietà ```total```, ```result``` e ```filters``` i rispettivi dati contenuti in ```filters``` e ```data```.  

```java
wacthQuery: ['filtro'],
async asyncData({store, query}) {
  let filters = await store.dispatch('browse-documenti/getFiltri')
  let data = await store.dispatch('browse-documenti/getData', {
  	filter: query.filtro || filters[0]._id
  })
  return {
  	total: data.total,
  	result: data.result,
  	filters: filters
  }
},
```

-Richiama la *query* dallo *store*:
```java
export const actions = {
  async getFiltri (store) {
    let response = await this.$axios.$post('aggregate', {
      'table': 'data_it',
      'query':[{
        '$match': {
          'table': collection,
          'access': 1,
          'type_id.id':{ $nin: exclude }
        }
      }, ...pipeline,
      {
        '$group': {
          '_id': '$' + groupBy,
          'count': {
            $addToSet: '$id'
          }
        }
      }]
    })
  }
}
```

##

Imposta come titolo della pagina “*Documenti e immagini*”.  

```java
head() {
	return{
		title: 'Documenti e immagini'
  }
}
```