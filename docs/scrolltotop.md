# Scrolltotop  

<hr>  

## Descrizione generale  
Il componente “**scrolltotop**” è un’icona [figura 1] con una freccia che punta verso l’alto (*↑*) che, viene visualizzata solo se ci si trova oltre il doppio dell’altezza della schermata e permette, se selezionato, di risalire alla testa della pagina.  

<div id="didascalia">
<img src="../imgcomp/scrolltotop/scroll_img.png" align="right" alt="scroll logo"/>
<br>
<br>
<br>
<div style="margin-right:-7px; margin-top:-10px">
[figura 1]	
</div>
</div>

## Comportamenti specifici  
Utilizza la libreria esterna ```jquery```.  

##

###Il metodo ```data()```:  
ritorna *```false```* e quindi non rende visibile il componente, se ci si trova a meno del doppio dell’altezza della schermata.  

```java
export default {
	data () {
		return {
			isVisible: false
		}
	},
```

##


### Il metodo ```beforeMount()```:  
allega al gestore di eventi, window (la nostra finestra), l’evento creatosi nel metodo ```handScroll()```.  

```java
beforeMount () {
	window.addEventListener('scroll', this.handleScroll)
},
```

##

### Il metodo ```scrollTop()```:  
assegna ad una variabile ```body``` il relativo *body HTML* e l’elemento di scroll permette di ritornare all’inizio della pagina in 500ms con una funzione di andamento (```swing```) da usare per la transizione.  

```java
scrollTop () {
	var body = $('html, body')
	body.stop().animate({
		scrollTop: 0
	}, 500, 'swing')
},
```
##

### Il metodo ```handleScroll()```:  
evento → il componente viene visualizzato se la parte di schermata su cui si si trova è maggiore del doppio dell’altezza della schermata.  

```java
handleScroll () {
	this.isVisible = window.pageYOffset > (window.innerHeight * 2)
}
```