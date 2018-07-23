# Result  

<hr>  

##

Il componente "**result**" è la pagina che mostra tutti gli elementi risultati dalla ricerca, attraverso la barra di ricerca e i filtri.  

##

- Richiama i componenti: [sticky](sticky.md), [card-view](cardview.md) e [list-view](listview.md).  

```java
import AuiSticky from '~/components/sticky/sticky.vue'
import AuiCardView from'~/components/item-view/card_view/card.vue'
import AuiListView from '~/components/item-view/list-view/list.vue'
```

##

### Il metodo ```next()```:  
 richiama una funzione che controlla se il numero di ```skip``` (*passaggi alla pagina successiva*) moltiplicato per il numero di elementi per pagina (*sempre fisso a 30*) è minore degli elementi totali.  
  Se lo è, permette il passaggio alla pagina successiva, altrimenti, disabilita il bottone “**>**”.  

```java
'next': function () {
	if((this.skip + 1) * this.limit < this.count) {
		this.$emit('next')
	}
},
```

##

### Il metodo ```prev()```:  
 richiama una funzione che controlla se il numero di ```skip``` (*passaggi alla pagina successiva*) è maggiore di zero. Se lo è, vuol dire che si è su una pagina successiva alla prima e, quindi, è possibile tornare indietro; altrimenti viene disabilitato il bottone “**<**”.  

```java
'prev': function () {
	if (this.skip > 0) {
		this.$emit('prev')
	}
}
```