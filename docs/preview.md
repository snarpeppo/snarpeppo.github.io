# Preview  

<hr>  

## Descrizione generale  
Il componente “**preview**”, attraverso il click di uno specifico bottone [figura 1] sull’elemento desiderato, mostra un’anteprima delle immagini della gallery di quell’elemento.  
In caso di più immagini è possibile scorrerle attraverso due frecce direzionali ai lati di esse.  
Viene inoltre mostrato, per ciascuna immagine, il titolo che ad essa è stato assegnato; affianco a questo attraverso il click del bottone “**VAI ALLA SCHEDA >**” si viene reindirizzati alla scheda in cui è contenuta l’immagine che si stava visualizzando.  

<div id="didascalia">
<img src="../imgcomp/preview/preview_img.png" align="right" alt="preview logo"/>
<br>
<br>
<br>
<div style="margin-right:-10px; margin-top:-10px">
[figura 1]	
</div>
</div>

## Comportamenti specifici  
Attraverso l’oggetto ```slickOptiond``` vengono definite le proprietà dell’immagine di anteprima. Per esempio, verrà mostrata una sola immagine alla volta (*slidesToShow: 1*) che sarà centrata nella schermata (*centerMode: true*); le immagini non avranno tutte la stessa grandezza (*variableWidth: true*) e saranno presenti, ai lati dell’immagine, due frecce per passare all’immagine precedente o successiva (*prevArrow e nextArrow*).  

```java
slickOptions: {
	infinite: false,
	edgeFriction: 0,
	centerMode: true,
	slidesToShow:1 ,
	variableWidth: true,
	waitForAnimate: false,
	prevArrow: '<span class ="slick-prev bg-transparent"><span class="fal fa-chevron-left fa-2x white"></span></span>',
	nextArrow: '<span class ="slick-next bg-transparent"><span class="fal fa-chevron-right fa-2x white"></span></span>',
	cssEase: 'cubic-bezier(.77,0,.175,1)'
},
```
##
##

```java
imagesLst: _.map(this.images, (e) => {
	var result = {
		href: e.url,
		title: e.title
	}

	result.type = /mp4$/.test(e.url) ? 'video/mp4' : ''

	if(/youtube\.com/.test(e.url)){
		result.type = 'text/html'
		result.youtube = _.split(e.url, '?v=')[1]
	}

	return result
})
```
<div id="elenco">
1. Per ogni immagine della preview, vengono assegnati il corrispondente <i>URL</i> e <i>titolo</i> alle rispettive proprietà (<i>href</i> e <i>title</i>) della variabile <code>result</code>; questa verrà restituita alla fine.
</div>
<div id="elenco">
2. Se il tipo della variabile <code>result</code> corrisponde ad un URL di un file <i>.mp4</i> (<code>.test function</code>) allora, verrà restituita la stringa <code>‘video/mp4’</code>, altrimenti restituirà una stringa vuota.
</div>
<div id="elenco">
3. Viene testato se l’URL in questione è un URL appartenente a YouTube, al tipo della variabile <code>result</code> viene detto che è un <code>‘text/html’</code> e per ogni <code>‘?v=’</code> all’interno dell’URL verrà sostituita una virgola. Alla fine verrà restituita la variabile <code>result</code>.
</div>
