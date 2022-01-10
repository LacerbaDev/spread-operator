# Spread Operator

Consente ad un oggetto iterabile (Array, Oggetto o Stringa) di estrapolare i singoli valori laddove ce ne sia almeno più di uno e ci consente di ottenere una lista di valori da un'array.
Come sintassi è simile al parametro "rest" `...` ma si comporta nella maniera opposta.
Quali sono gli utilizzi pratici dello __spread operator__?

## Array

__Concatenare array__

E' possibile usarlo per concatenare rapidamente due array o inserire un valore all'inizio o alla fine di un array.
Usando il metodo `concat()` proprio degli array la sintassi è la seguente:
```
// Usando metodo concat()
let arr = [1,2,3];
let arr2 = [4,5];
  
arr = arr.concat(arr2);
  
console.log(arr); // [ 1, 2, 3, 4, 5 ]
```
Usando invece lo spread operator è possibile fare:
```
// usando Spread operator
let arr = [1,2,3];
let arr2 = [4,5];
  
arr = [...arr,...arr2];
console.log(arr); // [ 1, 2, 3, 4, 5 ]
```

__Nota:__ Anche se è possibile utilizzare lo spread operator per ottenre lo stesso risultato è sconsigliato il suo utilizzo quando si ha a che fare con una grande mole di dati. In quel caso è meglio utilizzare il metodo nativo degli array `concat()` che è più efficiente in termini di performance.

---

__Copiare contenuto di un array in un altro (clonare un array)__

Se usassimo una sintassi del genere per copiare un array:
```
let arr = ['a','b','c'];
let arr2 = arr;
  
console.log(arr2); // [ 'a', 'b', 'c' ]
```
siamo in grado di ottenere una copia dell'array all'interno della variabile `arr2` __MA__ se provassimo ad esempio ad aggiungere un elemento al secondo array copiato in questo modo:
```
arr2.push('d');
  
console.log(arr2);
console.log(arr); 
```
all'interno del primo array avremmo lo stesso elemento poiché con la sintassi precedente non abbiamo "copiato" un oggetto in una nuova variabile bensì abbiamo copiato la "reference" dell'oggetto ovvero __la sua zona di memoria__ ed ogni cambiamento all'oggetto andrebbe a ripercuotersi in tutti quelle variabile che puntano a quella "reference".

Per risolvere questo problema ci viene in soccorso lo spread operator che ci consente letteralmente di __clonare__ l'oggetto andando a creare un altro oggetto separato in una nuova zona di memoria.

```
// spread operator per clonare array
let arr = ['a','b','c'];
let arr2 = [...arr];
// con ...arr stiamo estrapolando i singoli valori
// con [...arr] stiamo creando un array con al suo interno i singoli valori estrapolati ed equivale a clonare l'array
  
console.log(arr); // [ 'a', 'b', 'c' ]
  
arr2.push('d'); // se provo ad inserire un elemento nel secondo array andrò soltanto ad apportare modifiche a quell'oggetto in quanto occupa una zona di memoria diversa da quello di partenza
  
console.log(arr2); // [ 'a', 'b', 'c', 'd' ]
console.log(arr); // [ 'a', 'b', 'c' ]
```

---
## Oggetti

__Clonare oggetti__
Allo stesso modo con cui si clonano gli array per evitare il problema di passare la reference ed effettuare modifiche non all'oggetto che pensiamo di aver copiato ma all'oggetto padre.
La sintassi è la medesima ma anziché le parentesi quadre andremo ad usare le parentesi graffe poiché stiamo generando oggetti e non array.

```
const user = {
    name: 'Marco',
    age: 31
};
  
const user2 = { ...user };
user.lastname = 'Bologna'
console.log(user2); // user2 non avrà la proprietà lastname
console.log(user);
```

E' possibile unire la clonazione all'aggiunta o modifica di nuove proprietà partendo da oggetti esistenti. Supponiamo di voler copiare un oggetto `user` mantenendo il suo nome e cognome ed aggiungendo contemporaneamente una proprietà relativa all'indirizzo:

```
const user = {
    name: 'Marco',
    lastname: 'Bologna',
    age: 31,
    gender: 'male'
};
  
const user2 = { ...user, address: 'Via Gian Giacomo Mora 26, Milano' };
console.log(user2);
```

---

__Merge di oggetti__
E' possibile usare lo spread operatore per unire oggetti:

```
const user = {
    name: 'Marco',
    age: 31
};
const user2 = {
    lastname: 'Bologna',
    phoneNumber: '+394234234223'
};
  
const mergedUser = { ...user, ...user2 };
console.log(mergedUser); // avrà tutte e 4 le proprietà nello stesso oggetto
```

__Nota:__ Fate attenzione che nel caso in cui ci siano proprietà con lo stesso nome negli oggetti che si vanno ad unire ci sarà una sovrascrittura della proprietà in base all'ordine con cui vengono mergiati gli oggetti

```
const user = {
    name: 'Marco',
    age: 31
};
const user2 = {
    name: 'Luigi',
    phoneNumber: '+394234234223'
};
  
const mergedUser = { ...user, ...user2 };
console.log(mergedUser); // il nome del nuovo oggetto sarà Luigi
```

---
## Stringhe

__Estrapolare i singoli valori da una stringa__
Essendo stringhe degli oggetti iterabili ovvero che hanno una property `length` è possibile usare lo spread operator per ottenere i singoli valori

```
const stringa = 'stringa di prova'

console.log(...stringa); // otteniamo i singoli caratteri della stringa

console.log([...stringa]) // inseriamo i valori estrapolati in un array
// equivalente di fare stringa.split("") ovvero splittare in un array ogni singolo carattere della stringa
```

---

