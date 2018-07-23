# Locandina  

<hr>  

##

- Il componente "**locandina**" è un contenitore per l'*immagine della locandina* dello spettacolo.  

##

- Prende in input solo la proprietà ```relateds```.  

```java
props: [
    'relateds'
],
```
##

- Prende l'array contenente tutte le relazioni (```_.chain(this.relateds)```), categorizzate come "*ca/objects*", è ritorna il primo (```.head()```) elemento di tipo "*Manifesti e locandine*".  

```java
computed: {
	locandina () {
		return _.chain(this.relateds).get('ca/objects').filter(item => item.type === 'Manifesti e locandine').head().value()
	}
}
```
##

- Attraverso il codice *.html* viene posta l'immagine della locandina ottenuta all'interno di un contenitore (*div-wrapper*).  

```html
<div v-if="locandina" class="locandina_wrapper">
	<img :src="locandina.img.url.mediumlarge">
</div>
```