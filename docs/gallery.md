# Gallery  

<hr>  

## Descrizione generale  
Il componente “**gallery**” è una galleria di immagini contenuta in un elemento dell’archivio.     
Se selezionata, l’immagine essa può, attraverso dei pulsanti mostrati sotto di essa, essere: ingrandita, rimpicciolita, mostrata in scala 1:1, mostrata full-screen, capovolta sia a dx-sx che dall’alto verso il basso e viceversa, ripristinata alla stato iniziale, spostarla dove si vuole e, inoltre, si può passare all’immagine precedente o successiva.  

## Comportamenti specifici  
La gallery acquisisce come input (```prop``` → properties) delle immagini che verranno passate al ```Viewer``` e visualizzate in slides.  

```java
components: {
	Viewer
},
props: ['images'],
```
##

L’immagine mostrata sarà quella precedentemente selezionata dalla galleria di immagini; questa però apparirà più grande dell’immagine originale.  

```html
<img v-for="item in scope.images" :src="item.url.mediumlarge" :data-source="item.url.original" :key="item.id">
```
##

L’immagine selezionata dalla gallery verrà mostrata secondo la disposizione di alcune opzioni (```slickOptions``` → es. *centerMode*, *slideToShow*, *variableWidth*...).  

```java
slickOptions: {
	infinite: false,
	edgeFriction: 0,
	centerMode: true,
	slidesToShow: 1,
	variableWidth: true,
	waitForAnimate: false,
	prevArrow: '<span class="slick-prev bg-transparent"><span class="fal fa-chevron-left fa-2x white"></span></span>',
	nextArrow: '<span class="slick-next bg-transparent"><span class="fal fa-chevron-right fa-2x white"></span></span>',
	cssEase: 'cubic-bezier(.77,0,.175,1)'
},
```
##

Le immagini della gallery potranno essere modificate secondo la scelta di alcune opzioni (```options``` → es. *zoomable*, *fullscreen*...), mostrate come bottoni appartenenti ad una toolbar.  
La funzione ```$emit```, partendo dal componente, comunica esternamente a tutti gli ascoltatori che se vorranno potranno bloccare l’evento; inoltre ritornerà come valore “*hidden*”.  

```java
options: {
	'button': false,
	'navbar': true,
	'toolbar': true,
	'zoomable': true,
	'transition': false,
	'fullscreen': false,
	'keyboard': true,
	'movable': true,
	'rotatable': false,
	'scalable': true,
	'inline': false,
	'tooltip': true,
	'title': true,
	'flipHorizontal': false,
	'flipVertical': false,
	'url': 'data-source',
	'hidden': () => {
		this.$emit('hidden')
	}
}
```