# List-view  

<hr>  

##

Il componente "**list-view**" sono gli elementi mostrati in formato "*elenco*".  

##

Utilizza le proprietà: ```title```, ```type``` e ```link```, dichiarate nel file *.js*, per visualizzare gli elementi sotto forma di *elenco* nel file *.html*.  

```java
export default{
	props: [
		'title',
		'type',
		'link'
	]
}
```

##

Tutti gli elementi dell’elenco sono contenuti in un *contenitore* (**<div class=”list”\>**).  

```html
<div class="list">
```
##

Ogni elemento sarà un link che riporterà il titolo della pagina a cui esso ricollega.  

```html
<nuxt-link v-html="title" :to="link" class="primary-color"></div>nuxt-link>
```