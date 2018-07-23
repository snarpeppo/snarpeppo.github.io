# Footer  

<hr>  

## Descrizione generale  
Il componente “*footer*” è un piè di pagina comune a tutte facciate.  
Esso mostra il logo del sito e dà informazioni generali, sui contatti, sul servizio al pubblico e sui social ad esso associati; quest’ultima categoria presenta dei link per ciascun social: Facebook, Twitter, YouTube e Instagram, che riconducono alla pagina social del sito.  

## Comportamenti specifici  
Il tag **<footer\>**, nel codice *.html*, avrà un contenitore al fondo della pagina che conterrà tutte le informazioni generali e, in più, un elenco di link che ricondurrà alla pagina di ciascun social.  

## 

```html
<footer id="footer" class="row py-4 bg-black text-sm-left text-center">
		<div class="container">
```
## 

```html
<div class="col-md-2 white pb-1">
	<h4 class="bold upp h6 white">Seguici su</h4>
	<ul class="social">
		<li>
			<a href="#">Facebook</a>
		</li>
```