# Searchpanel  

<hr>  

## Descrizione generale  
Il componente “**searchpanel**” è una barra di ricerca che compare solo quando si clicca sull’apposita icona [figura 1].   
Permette la ricerca, attraverso inserimento manuale dell’elemento voluto, all’interno dell’archivio.  
La sua posizione varia a seconda del dispositivo che si sta utilizzando, lo si troverà in alto a sinistra per gli utenti PC (qualsiasi browser), mentre si troverà in basso a sinistra per gli utenti Mobile (Tablet e Smartphone).  

<div id="didascalia">
<img src="../imgcomp/searchpanel/search_img.png" align="right" alt="searchpanel logo"/>
<br>
<br>
<br>
<div style="margin-right:-10px; margin-top:-10px">
[figura 1]	
</div>
</div>

## Comportamenti specifici  
Al click della specifica icona [figura 2] si aprirà, da sinistra verso destra, una barra di ricerca e avverrà un cambio di icona che, se selezionata, chiuderà la barra di ricerca.  

<div id="didascalia">
<img src="../imgcomp/searchpanel/search_imgx.png" align="right" alt="searchpanel logo x"/>
<br>
<br>
<br>
<div style="margin-right:-10px; margin-top:-10px">
[figura 2]	
</div>
</div>

##

Nella barra di ricerca sarà presente la scritta “*Inizia a cercare…*”.  

```java
placeholder: 'inizia a cercare…'
```
<center>![searchpanel barra di ricerca](imgcomp/searchpanel/search_cerca.png)</center>

##

La ricerca viene effettuata secondo una “*query*”. Ossia tramite l’estrazione di *tags* (la/e parola/e cercata/e), che soddisfano un certo criterio di ricerca, da un *database* (l’elenco degli elementi dell’archivio).  

```java
goTo () {
	this.$router.push({ name: 'cerca', query: { tags: this.search } })
},
```

##

Al click sull’icona di ricerca verranno visualizzati gli elementi correlati alla ricerca, questo grazie al richiamo del metodo ```goTo()```, che avvia la ricerca se si clicca il bottone.  

```html
<button type="button" class="btn" @click.prevent="goTo()">
```

##

Al click sull’icona di chiusura della ricerca verrà chiusa la barra di ricerca, tornando allo stato iniziale; questo grazie al richiamo del metodo ```closeMenu()``` che, se si dà l’input di chiusura, porrà come *```false```* (chiuso) lo stato della barra di ricerca.  

```html
<input type="text" v-model="search" @keyup.esc="closeMenu()" :placeholder="placeholder">
```