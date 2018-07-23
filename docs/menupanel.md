# Menupanel  

<hr>  

## Descrizione generale  
Il componente “**menupanel**” è un menù che compare quando si clicca sull’apposita icona [figura 1].  
Permette gli accessi, tramite 8 voci, alle sezioni: “Home”, [Stagioni](stagioni.md), [Spettacoli](spettacoli.md), [Persone](persone.md), [Teatri e compagnie](teatrico.md), [Documenti e immagini](docimg.md), [Il Dramma, 1925 - 1983](dramma.md)  e [Cerca](cercapg.md), la quale permetterà la ricerca, dell’elemento voluto, all’interno dell’archivio.  
La sua posizione varia a seconda del dispositivo che si sta utilizzando, lo si troverà in alto a sinistra per gli utenti PC (qualsiasi browser), mentre si troverà in basso a sinistra per gli utenti Mobile (Tablet e Smartphone).  

<div id="didascalia">
<img src="../imgcomp/menupanel/menupanel_img.png" align="right" alt="menupanel logo"/>
<br>
<br>
<br>
<div style="margin-right:-10px; margin-top:-10px">
[figura 1]
</div>
</div>

## Comportamenti specifici  
- Al click della specifica icona si aprirà, da sinistra verso destra, un menù di selezione con le voci sopra citate.  
- Le voci del menù potranno essere modificate tramite WordPress.  
- La proprietà **mouseenter** permetterà, al passaggio del cursore su un elemento, il cambio del suo sfondo (**changeBg**), mentre quella **mouseleave** annullerà il cambio di sfondo. Lo sfondo della voce che verrà cambiato sarà lo stesso della pagina a cui quella voce reindirizza.  

```html
<li v-for="item in $store.state.menu.items">
	<nuxt-link :to="item.url" v-on:mouseenter.native="changeBg(item.attr_title)" v-on:mouseleave.native="currentBg  = null">
</li>
```
- Alla selezione, click, di un elemento della lista si verrà reindirizzati alla pagina corrispondente all’elemento desiderato.  