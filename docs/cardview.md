# Card-view  

<hr>  

##

Il componente "**card-view**" sono gli elementi mostrati in formato "*card*".  

##

Importa il componente: [preview](preview.md).  

```java
import AuiPreview from '~/component/preview/preview.vue'
```
##

Prende in input alcune proprietà e ci restituirà un vettore di immagini.  

```java
props: [
	'title',
	'imgUrl',
	'category',
	'type',
	'link',
	'id',
	'table',
	'preview'
],
```
```java
data (){
	return {
		'images': []
	}
},
```

##

Prende in input la proprietà ```imgUrl``` e, facendo dei controlli, imposterà la grandezza dell’immagine della card: se l’url dell’immagine è una stringa (```_.isString```) e se non è vuoto (" "), allora l'immagine avrà la sua normale grandezza; se l’url dell’immagine e l’immagine medio-larga non sono null, indefinito o di lunghezza = 0, allora l’immagine avrà una grandezza medio-larga; altrimenti ancora, sarà un’icona.  

```java
computed: {
	backImg: function (){
		let img = {'thumb': '', 'medium': ''}
		if (_isString(this.imgUrl) && this.imgUrl !== ''){
			img = {'thumb': this.imgUrl, 'medium': this.imgUrl}
		}else if (!_.isEmpty(this.imgUrl) && !_.isEmpty(this.imgUrl.mediumlarge)){
			img = {'thumb': this.imgUrl.thumbnail, 'medium': this.imgUrl.mediumlarge}
			}else{
			let icon = util.getIcon(this.table, this.type)
			img = {'thumb': icon, 'medium': icon}
		}
		return img
	}
},
```

##

Restituisce l’immagine della card (**backImg.medium**) che avrà, grazie al codice *.html*, essa stessa come sfondo sfocato (**card_img_blurred_bg**), e che al click ci mostrerà la preview delle immagini (**@click.prevent=”getPreview”**).  


```html
<clazy-load :src="backImg.medium">
```
```html
<div class="card_img_blurred_bg" :style="{ backgroundImage: 'url(' + backImg.medium + ')' }"></div>
<img :src="backImg.medium" :alt="title" @click.prevent="getPreview">
```
##

### Il metodo ```getPreview()```:  
 prende in input la proprietà ```preview``` e controlla: se non è una preview, rimanda direttamente al link senza ricaricare tutta la pagina (```.push(this.link)```), altrimenti manda allo *store* le azioni del metodo ```getDetail()``` (dettaglio e identificativo) e restituisce alle immagini (```images```) un URL di media larghezza e un titolo.  

```java
async getPreview () {
	if (!this.preview) {
		this.$router.push(this.link)
	} else {
		let detail = await this.$store.dispatch('detail/getDetail', {table: this.table, id: this.id})
		if (detail.representations) {
			this.images = _.map(detail.representations, e => {
				return {
					'url': e.url.mediumlarge,
					'title'; e.title
				}
			})
		}
```

##

Infine controlla se i metadati sono quelli di un video, in quel caso mette l’URL del video nelle immagini (```images```).  

```java
if (!_.isEmpty(detail.metadati) && !_.isEmpty(detail.metadati.external_link)) {
	this.images.push({'url': detail.metadati.external_link.subelement.url_entry.value})
}
```

