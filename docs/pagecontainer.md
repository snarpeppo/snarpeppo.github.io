# Pagecontainer  

<hr>

## Descrizione generale  
Il componente “**pagecontainer**” è un contenitore per i filtri, i risultati della pagina di ricerca, e  le icone per la loro impaginazione (a *griglia* o ad *elenco*) che si trova sia in *Archivio* che in *Biblioteca*.  

## Comportamenti specifici  

###Il metodo ```openFiler()```:  
 setta lo stato del bottone dei filtri a *```true```*, verranno quindi visualizzati i filtri, manda allo *store* le azioni del metodo ```showHideScroll``` (```.dispatch```) e permette la visualizzazione dello scrollbar a lato pagina quando i filtri sono attivi.  

```java
openFilter () {
	this.isOpen = !this.isOpen
	this.$store.dispatch('showHideScroll', this.isOpen)
}
```