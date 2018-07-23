# MetadataService

<hr>

##

- Il componente "**metadataService**" è una classe che consente di gestire, attraverso diversi metodi, i metadati che verrano poi restituiti al componente [metadati](metadati.md).

##

###La classe MetadataService { }:
contiene tutti i metodi che verranno utilizzati dal componente [metadati](metadati.md).

```java
export default class MetadataService {...}
```

##

### Il metodo constructor():
è il costruttore che, riceve come parametro i metadati e li assegna ad una variabile della classe col medesimo nome.

```java
constructor (metadati) {
	this.metadati = metadati
}
```

##

### Il metodo value():
ritorna i metadati passati al costruttore.

```java
value() {
	return this.metadati
}
```

##

### Il metodo clearEmptyMetadata():
controlla se l'oggertto metadati è vuoto (```_recursiveCheckEmpty```), copia i valori presenti in metadati (```Object.assign```) e li assegna alla variabile costante ```clearMetadata```.  
Ritorna una nuova ```MetadataService``` con in nuovo oggetto senza metadati vuoti (```clearMetadata```).

```java
clearEmptyMetadata() {
	const clearMetadata = Object.assign({}, this._recursiveCheckEmpty(this.metadati))
	return new MetadataService(clearMetadata)
}
```

##

### Il metodo formatMetadati():
permette, se richiamato, di *formattare* i metadati. Restituisce alla variabile ```result``` il risultato, ```item```, della funzione_____
Per ogni item verrà assegnato ```*true*``` alla proprietà ```visible``` e ```code``` alla proprietà ```fieldCode```.  
Aggiunge a ```item.plainsubElement``` Crea una catena di sotto metadati 

Aggiunge a ```item.plainsubElement``` una catena di sottometadati, mettendoli dentro un array contenente il loro 'valore' primario, viene compattato e ogni 'submetadato' viene diviso dalla stringa (' - '), infine, viene riportato il valore finale ```.value()```.
Inoltre, con la funzione ```.replace()``` rimpiazzerà, appunto, tutti i caratteri con cui viene apportato 'il riporto a capo' dei vari sistemi operativi, con il tag ```<br/>```.
infine, ritorna l'oggetto ```item```

```java
formatMetadati() {
	const result = _.map(this.metadati, (item, code) => {
		item.visible = true
		item.fieldCode = code
		item.plainSubElement = _.chain(item.subelement).map('value').compact().join(' - ').value()
		if (_.isEmpty(item.plainSubElement)) {
			item.plainSubElement = item.value
		}
		item.plainSubElement = item.plainSubElement.replace(/(?:\r\n|\r|\n)/g, '<br/>')
		return item
	})
	return new MetadataService(result)
}
```

##

### Il metodo reduceForSummary():
Adatta il metadato al formato del *summary*, per esserci poi inserito 
La funzione reduce aggiunge all'array vuoto summary

Riempie un array, inizialmente vuoto, con i valori ridotti dell'oggetto ```summary``` con il codice (```code```) ricercato tramite ```.find()```,  troveremo quindi, l'array con i valori di ```label```, ```metadati```, e ```visible```, viene poi restituito tutto il metadato addattato con la funzione```.value()```.



```java
reduceForSummary(summary) {
	return _.chain(summary)
	.reduce((memo, code) => {
		const item = this.find(code)
		if (item) {
			memo.push(item)
		}
		return memo
	}, [])
	.map((value, key) => {
		return {
			label: value.label,
			metadati: value,
			visible: _.some(value, 'visible')
		}
	})
	.value()
}
```

##

### Il metodo reduceForSchedaBreve():
Adatta il metadato al formato della *scheda breve*, per esserci poi inserito 

Riempie un array, inizialmente vuoto, con i valori ridotti dell'oggetto ```schedabreve``` con il codice (```code```) ricercato tramite ```.find()```, avremmo infine, il vettore con i vecchi contenuti di ```schedabreve``` *ridotti* con la funzione ```.reduce()```.


```java
 reduceForSchedaBreve (schedabreve) {
 	return schedabreve.reduce((old, code) => {
 		old[code] = this.find(code)
 		return old
 	}, {})
 }
```

##

### Il metodo find():
Ricerca un metadato specifico all'interno della lista di metadati.

```java
find (elementCode) {
	return this.metadati[elementCode] ? this.metadati[elementCode] : this.metadati.find(item => item.fieldCode === elementCode)
}
```