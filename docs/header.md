# Header  

<hr>  

## Descrizione generale  
Il componente “**header**” è l’insieme dei due componenti [menupanel](menupanel.md) e [searchpanel](searchpanel.md) e, del link-immagine che permette il reindirizzamento alla homepage del sito.  
L’icona del menupanel apre un menù ad 8 voci che condurranno alle relative pagine [figura 1].  
L’icona del searchpanel permette l’apertura di una barra di ricerca [figura 1].    
La sua posizione varia a seconda del dispositivo che si sta utilizzando, lo si troverà in alto a sinistra per gli utenti PC (qualsiasi browser), mentre si troverà in basso a sinistra per gli utenti Mobile (Tablet e Smartphone).  

<div id="didascalia">
<img src="../imgcomp/header/header_img.png" align="right" alt="header logo"/>
<br>
<br>
<br>
<br>
<br>
<div style="margin-right:10px; margin-top:-10px">
[figura 1]	
</div>
</div>

## Comportamenti specifici  

###Il metodo ```openMenu()```:  

```java
openMenu (){
	this.$store.commit('searchbar/setOpenSearch', false)
	this.$store.commit('menu/setOpenMenu', !this.$store.state.menu.isOpen)
	this.$store.dispatch('showHideScroll', this.$store.state.menu.isOpen)
},
```
<div id="elenco">
1. effettua una chiamata al metodo <code>setOpenSearch</code> (nel <i>searchbar.js</i>) e lo pone a <code><i>false</i></code>; questo fa in modo che, se il menù a 8 voci è aperto, non compaia l’icona per la ricerca.
</div>
<div id="elenco">
2. effettua una chiamata al metodo <code>setOpenMenu</code> (nel <i>menu.js</i>) e, negando lo stato nel menù <code>isOpen</code> che per default è a <code><i>false</i></code>, rende <code>isOpen</code> <code><i>true</i></code>; questo permette l’apertura del menù a 8 voci al click dell’apposita icona.
</div>
<div id="elenco">
3. manda allo <i>store</i> le azioni del metodo <code>showHideScroll</code> e controlla lo stato nel menù <code>isOpen</code>, che per default è a <code><i>false</i></code>; quindi non permetterà la visualizzazione dello <i>scrollbar</i> a lato pagina quando il menù a 8 voci è aperto.
</div>

### Il metodo ```openSearch()```:  

```java
openSearch (){
	this.$store.commit('menu/setOpenMenu', false)
	this.$store.commit('searchbar/setOpenSearch', !this.$store.state.searchbar.isOpen)
	this.$store.dispatch('showHideScroll', this.$store.state.searchbar.isOpen)
},
```
<div id="elenco">
1. effettua una chiamata al metodo <code>setOpenMenu</code> (nel <i>menu.js</i>) e lo pone a <code><i>false</i></code>; questo fa in modo che, se la barra di ricerca è attiva, venga cambiato lo stato del menù, senza che l’icona di esso scompaia al click di quella della ricerca.
</div>
<div id="elenco">
2. effettua una chiamata al metodo <code>setOpenSearch</code> (nel <i>searchbar.js</i>) e, negando lo stato nella searchbar <code>isOpen</code> che per default è a <code><i>false</i></code>, rende <code>isOpen</code> <code><i>true</i></code>; questo permette l’apertura della barra di ricerca al click dell’apposita icona.
</div>
<div id="elenco">
3. manda allo <i>store</i> le azioni del metodo <code>showHideScroll</code> e controlla lo stato nella searchbar <code>isOpen</code>, che per default è a <code><i>false</i></code>; quindi non permetterà la visualizzazione dello scrollbar a lato pagina quando la barra di ricerca è attiva.
</div>
