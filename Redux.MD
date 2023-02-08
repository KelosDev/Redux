# REDUX

## Cos'è:

Redux è un modello e una libreria per la gestione e l'aggiornamento dello stato dell'applicazione, utilizza eventi chiamati AZIONI. Funge da archivio centralizzato per lo stato che deve essere utilizzato nell'intera app, con regole che garantiscono che lo stato possa essere aggiornato solo in **modo prevedibile**

Modo prevedibile? -> In Redux, l'aggiornamento di uno stato in modo prevedibile significa che lo stato dell'applicazione viene gestito in modo deterministico e immutabile. Ciò significa che ogni azione che modifica lo stato viene gestita da una funzione denominata **REDUCER** che, dato lo stato corrente e l'azione da eseguire, restituisce un nuovo stato. In questo modo è possibile prevedere come cabierà lo stato dell'applicazione in seguito a un'azione specifica e garantire che lo sato non venga modificato direttamente, ma solo tramite ale azioni gestite dai reducer. Questo rende il processo di aggiornamento dello stato più prevedibile e facile da debuggare.

## Perchè usare Redux:

Redux consente di gestire lo stato 'globale', ovvero lo stato necessario in molte parti dell'applicazione. I modelli e gli strumenti forniti da Redux semplificano la comprensione di quando, dove, perchè e come viene aggiornato lo stato dell'applicazione e come si comporterà la logica dell'applicazione quando si verificano tali modifiche.

## Quando usare Redux: 

1) Ci sono molti stati dell'applicazione che servono in molte posizioni dell'app
2) Lo stato dell'app viene aggiornato frequentemente nel tempo
3) La logica per aggiornare tale sato può essere complessa
4) L'app ha una base di codice di medie o grandi dimensioni e potrebbe essere utilizzata da molte persone

---
## Store, Actions, Reducers

In Redux, i reducers, le actions e lo store sono tre componenti principali che lavorano inseme per gestire lo stato dell'applicazione.

1) **Reducer**: Un reducer è una funzione che modifica lo stato dell'applicazione. Riceve l'azione corrente e lo stato corrente dell'applicazione come input e restituisce un nuovo stato dell'applicazione. I reducers sono immutabili, il che significa che non modificano direttamente lo stato corrente, ma restituiscono un nuovo stato.
2) **Actions**: Le actions sono oggetti che descrivono le azioni che l'utente o l'applicazione possono intraprendere. Ogni azione ha un tipo che descrive il tupo di azione e, a volte, un payload che fornisce ulteriori dettagli sulle azioni da eseguire.
3) **Store**: Lo store è il contenitore centrale di Redux che contiene lo stato dell'applicazione. E' possibile accedere ai dati dello stato tramite la funzione 'getState' e modificare lo stato tramite la funzione 'dispatch' che accetta un'azione come input.

In sintesi, i reducers gesticono i cambiamenti dello stato dell'applicazione, le actions descrivono le azioni da intraprendere e lo store è il contenitore centrale che tiene traccia dello stato dell'applicazione. Questi tre componenti lavorano insieme per rendere l'applicazione reattiva ai cambiamenti di stato.

---

# REDUX TOOLKIT

## Scopo:

Il pacchetto Redux Toolkit è destinato ad essere il modo standard per scrivere la logia Redux.

## Installazione in un nuovo progetto React
```
 npx create-react-app my-app --template typescript //crea un nuovo progetto in React usando TypeScript

 npm i react-redux @types/react-redux @reduxjs/toolkit //installa le dipendenze redux e redux toolkit nella cartella del progetto
```

## Cos'è incluso: 

Redux Toolkit include le seguenti API:

- **configureStore()**
- **createReducer()** 
- **createAction()** 
- **createSlice()** 
- **createAsyncThunk()** 
- **createEntityAdapter()** 
- **createSelector()** 

---

## Nello specifico:

- Con **configureStore()** è possibile creare e configurare uno store Redux. Per utilizzare questa funzione e necessario importarla dalla libreria: 
```js
import {configureStore} from '@reduxjs/toolkit'
```
Quindi è possibile utilizzarla per creare un nuovo store:
```js
const store = configureStore({
    reducer: rootReducer,
}) 
```
In questo esempio, 'configureStore' riceve un oggetto che descrive la configurazione dello store. In questo caso viene passato solo un singolo reducer ('rootReducer') che gestisce lo stato globale dell'app.

'configureStore' offre anche altre opzioni di configurazione avanzate, come la possibilità di passare middleware, preloaded state e enhancers. Queste opzioni possono essere passate come proprietà supplementari dell'oggetto di configurazione:
```js
const store = configureStore({
    reducer: rootReducer,
    middleware: [loggerMiddleware],
    preloadedState: { ... },
    enhancers: [applyMiddleware(thunkMiddleware)],
})
```
Spiegazione del codice sopra:

La funzione configureStore riceve un oggetto di configurazione che descrive come deve essere configurato lo store. L'oggetto di configurazione può avere le seguenti proprietà:

- 'reducer': è una funzione che gestisce lo stato globale dell'applicazione. Questa funzione viene passata a 'createStore' di Redux per creare lo store.
- 'middleware': è un array di middleware che gestiscono le azioni prima che raggiungano il reducer. I middleware possono essere utilizzati per eseguire azioni asincrone, loggare le azioni o midificarle prima che queste raggiungano il reducer.
- 'preloadedState': è un oggetto che rappresenta lo stato iniziale dell'applicazione. QUesto stato viene passato a 'createStore' di Redux come stato iniziale
- 'enhancers': è un array di enhancer che modificano la funzione di creazione dello store. Gli enhancer possono essere utilizzati per integrare middleware, estensioni o altri strumenti con lo store.

---

- Con 'createReducer()' è possibile creare un reducer per gestire lo stato dell'applicazione. Per utilizzarlo bisogna importarlo dalla libreria:
```js
import {createReducer} from '@reduxjs/toolkit'
```
Quindi, è possibile utilizzare createReducer per creare un nuovo reducer:
```js
const counterReducer = createReducer(0, {
  increment: state => state + 1,
  decrement: state => state - 1,
});
```
In questo esempio 'createReducer' riceve due argomenti:
1) Il valore iniziale dello stato, che in questo caso è 0
2) Un oggetto che descrive come gestire le azioni. Ogni proprietà dell'oggetto rappresenta un tipo di azione e il relativo valore è una funzione che descrive come il reducer deve gestire l'azione.

In questo esempio, vengono descritte due azioni: 'increment' e 'decrement'. Ogni volta che viene inviata un'azione di questo tipo, il reducer esegue la funzione corrispondente per modificare lo stato.

---

- Con 'createAction() è possibile creare azioni. Bisogna importarla dalla libreria:
```js
import { createAction } from '@reduxjs/toolkit';
```
Quindi, è possibile utilizzare createAction per creare una nuova azione:
```js
const increment = createAction('increment');
```
In questo esempio, 'createAction' riceve un solo argomento: il nome dell'azione. Il risultato è una funzione che può essere invocata per creare un'azione con il nome specificato.

La funzione 'increment' può essere utilizzate per creare un'azione di tipo 'increment':
```js
dispatch(increment())
```
In questo modo, viene inviata un'azione di tipo 'increment' al dispatcher di Redux, che la inoltra ai reducer per modificare lo stato dell'applicazione.

---

- Con 'createSlice()' è possibile creare uno 'slice' di stato, ovvero una porzione di stato che gestisce una specifica parte dell'applicazione. Per utilizzarlo bisogna importarlo:
```js
import { createSlice } from '@reduxjs/toolkit';
```
Quindi, è possibile utilizzare createSlice per creare un nuovo slice di stato:
```js
const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
  },
});
```
In questo esempio, 'createSlice' riceve un oggetto che descrive il nome dello slice di stato, lo stato inziale e i reducer. I reducer sono funzioni che gestiscono le azioni e modificano lo stato in modo prevedibile. Dopo aver creato uno slice di stato, è possibile accedere alle azioni e al reducer tramite l'oggetto restituito da 'createSlice':
```js
const { actions, reducer } = counterSlice
```
- 'action' è un oggetto che contiene tutte le azioni gestite dallo slice di stato come 'increment' e 'decrement'

- 'reducer' è la funzione che gestisce le azioni e modifica lo stato. Questa funzione può essere passata a 'useReducer' o a 'combineReducers' per essere integrata nel sistema di gestione dello stato globale.

---

- con 'createAsyncThunk()' è possibile gestire l'esecuzione di operazioni asincrone. Per utilizzarlo bisogna importarlo:
```js
import { createAsyncThunk } from '@reduxjs/toolkit';
```
Quindi, è possibile utilizzare createAsyncThunk per creare un nuovo thunk:
```js
const fetchData = createAsyncThunk('fetchData', async (arg1, arg2) => {
  // codice per effettuare una richiesta HTTP, ad esempio con axios
});
```
In questo esempio 'createSlice' riceve due argomenti: 

- il nome dell'azione, in questo caso è 'fetchData'
- una funzione che descrive l'operazione asincrone da eseguire. Questa funzione riceve eventuali argomenti passati al thunk e restituisce una promise che si risolve con i dati recuperati.

La funzione 'fetchData' effettua una richiesta HTTP con una libreria come AXIOS per recuperare i dati. La funzione restituisce una promise.

Per utilizzare il thunk 'fetchData' è possibile invocarlo con la funzione 'dispatch' di Redux:
```js
dispatch(fetchData(arg1, arg2).then(data => {
    //codice per gestire i dati recuperati
}))
```
In questo modo viene invocato il thunk 'fetchData' e viene effettuata una richiesta HTTP. Al completamento della richiesta, i dati recuperati vengono gestiti nel codice.

---

- 'createEntityAdapter()' fornisce un modo semplice per gestire un elenco di elementi (ad esempio un elenco di prodotti) in uno stato Redux. Per utilizzarlo bisogna importarlo:
```js
import { createEntityAdapter } from '@reduxjs/toolkit';
```
Quindi, è possibile utilizzare createEntityAdapter per creare un adapter per un elenco di elementi:
```js
const productAdapter = createEntityAdapter({
  selectId: product => product.id,
});
```
In questo esempio 'createEntityAdapter' riceve un oggetto di configurazione che descrive come gestire gli elementi nell'elenco. L'opzione 'selectId' specifica che l'ID univoco è presente nella proprietà 'id' dell'oggetto 'product'.

Dopo aver creato l'adapter è possibile utilizzarlo per gestire lo stato dell'elenco di elementi nello stato di Redux. Ad esempio è possibile creare uno stato iniziale per l'elenco di prodotti:
```js
const initialState = productAdapter.getInitialState();
```
Successivamente è possibile creare un reducer per gestire le azioni che modificano l'elenco di prodotti:
```js
const productReducer = productAdapter.createSlice({
  name: 'products',
  initialState,
  reducers: {
    addProduct: (state, action) => {
      productAdapter.addOne(state, action.payload);
    },
    updateProduct: (state, action) => {
      productAdapter.updateOne(state, action.payload);
    },
    removeProduct: (state, action) => {
      productAdapter.removeOne(state, action.payload);
    },
  },
});
```
In questo esempio il reducer 'productReducer' utilizza le funzioni 'addOne', 'updateOne' e 'removeOne' fornite dall'adapter per gestire le azioni 'addProduct', 'updateProduct' e 'removeProduct' rispettivamente.

'addOne', 'updateOne' e 'removeOne' sono funzioni fornite da 'createEntityAdapter' di Redux Toolkit. Queste funzioni sono utilizzate per gestire le operazioni di inserimento, aggiornamento e rimozione di un singolo elemento in un elenco di elementi gestito da uno stato di Redux.

- 'addOne' viene utilizzato per aggiungere un nuovo elemento all'elenco. Riceve come argomenti lo stato corrente dell'elenco e un payload che rappresenta il nuovo elemento da aggiungere.

- 'updateOne' viene utilizzato per aggiornare un elemento esistente nell'elenco. Riceve come argomenti lo stato corrente dell'elenco e un payload che rappresenta l'elemento da aggiornare e i nuovi valori per le sue proprietà.

- 'removeOne' viene utilizzato per rimuovere un elemento esistente dall'elenco. Riceve come argomenti lo stato corrente dell'elenco e un payload che rappresenta l'elemento da rimuovere.

---

- Con 'createSelector()' è possibile creare selettori memoizzati che calcolano il valore dello stato di Redux basato su uno o più selettori di stato. 

La funzione 'createSelector' prende come argomenti uno o più selettori di stato e una funzione che calcola il valore basato sui valori restituiti dai selettori di stato. La funzione restituita dalla 'createSelector' è un selettore memoizzato che tiene traccia delle dipendenze dei selettori di stato e calcola il valore solo quando i valori dei selettori di stato cambiano.

Ecco un esempio:

```js
import { createSelector } from 'reselect';

const selectUsers = state => state.users;
const selectUserId = (state, props) => props.userId;

const selectUser = createSelector(
  [selectUsers, selectUserId],
  (users, userId) => users[userId]
);
```
In questo esempio 'selectUsers' è un selettore di stato che restituisce la porzione dello stato che contiene gli utenti, mentre 'selectUserId' è un selettore di stato che restituisce l'ID utente dalle proprietà passate. La funzione 'selectUser' calcola l'utente specifico restituendo l'elemento con l'ID specificato dall'elenco degli utenti.

L'utilizzo di 'createSelector' migliora le prestazioni dell'applicazione riducendo il numero di ricomputazioni effettuate quando lo stato cambia, poichè il selettore memoizzato tiene traccia delle dipendenze e calcola il valore solo quando i valori dei selettori di stato cambiano.

Excursus: significato di memoizzare: significa memorizzare il valore restituito da una funzione per un dato insieme di input, in modo che quando viene chiamata di nuovo con gli stessi input, il valore memorizzato venga restituito senza eseguire di nuovo la funzione. Questo è utile per le funzioni costose in termini di tempo di calcolo, poichè riduce il tempo di esecuzione totale dell'applicazione evitando di ricalcolare il risultato per gli stessi input. Non esiste una differenza tra "memorizzare" e "memoizzare". "Memoizzare" è una parola che deriva da "memorizzare", ed è un termine tecnico utilizzato in programmazione per descrivere la tecnica di memorizzazione dei risultati delle funzioni.
In pratica, "memorizzare" significa semplicemente archiviare o memorizzare un valore o un risultato, mentre "memoizzare" significa utilizzare questa tecnica per migliorare le prestazioni di un'applicazione.
In sintesi, "memorizzare" è un verbo generale che significa archiviare informazioni, mentre "memoizzare" è un termine più specifico che si riferisce alla memorizzazione dei risultati delle funzioni per migliorare le prestazioni dell'applicazione.

---

## Redux Thunk (x rtk)

Redux Thunk è un middleware che consente di scrivere azioni asincrone in un'applicazione Redux. Ecco i passaggi per utilizzarlo:

1) Installare Redux Thunk tramite npm: 'npm install redux-thunk'
2) Importare il middleware nell'applicazione Redux e configurarlo nella funzione 'configureStore' fornita da redux toolkit:
```js
import { configureStore, getDefaultMiddleware } from '@reduxjs/toolkit';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

const store = configureStore({
  reducer: rootReducer,
  middleware: [...getDefaultMiddleware(), thunk],
});
```
3) Scrivere azioni asincrone che ritornano funzioni anzichè oggetti. Queste funzioni possono quindi dispatchare altre azioni e chiamare API asincrone:
```js
export const fetchData = () => {
  return (dispatch) => {
    fetch('https://my-api.com/data')
      .then((response) => response.json())
      .then((data) => {
        dispatch({ type: 'FETCH_SUCCESS', payload: data });
      });
  };
};
```
4) Dispatchare queste azioni nei componenti React o nei reducer:
```js
import { fetchData } from './actions';

...

dispatch(fetchData());
```


---

## Esempio pratico di utilizzo - Gestione carrello della spesa

In un file 'cartSlice.ts'

```ts
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';
import { AppThunk } from '../store';
import axios from 'axios';

interface CartItem {
  id: string;
  name: string;
  price: number;
  quantity: number;
}

interface CartState {
  items: CartItem[];
  loading: boolean;
  error: string | null;
}

const initialState: CartState = {
  items: [],
  loading: false,
  error: null,
};

export const fetchCart = createAsyncThunk(
  'cart/fetchCart',
  async (): Promise<CartItem[]> => {
    try {
      const response = await axios.get('/api/cart');
      return response.data;
    } catch (error) {
      throw error;
    }
  }
);

const cartSlice = createSlice({
  name: 'cart',
  initialState,
  reducers: {
    addToCart(state, action) {
      const { id, name, price } = action.payload;
      state.items.push({ id, name, price, quantity: 1 });
    },
    removeFromCart(state, action) {
      const { id } = action.payload;
      state.items = state.items.filter((item) => item.id !== id);
    },
    updateCartItem(state, action) {
      const { id, quantity } = action.payload;
      const itemIndex = state.items.findIndex((item) => item.id === id);
      state.items[itemIndex].quantity = quantity;
    },
  },
  extraReducers: (builder) => {
    builder.addCase(fetchCart.pending, (state) => {
      state.loading = true;
      state.error = null;
    });
    builder.addCase(fetchCart.fulfilled, (state, action) => {
      state.loading = false;
      state.items = action.payload;
    });
    builder.addCase(fetchCart.rejected, (state, action) => {
      state.loading = false;
      state.error = action.error.message;
    });
  },
});

export const { addToCart, removeFromCart, updateCartItem } = cartSlice.actions;

export default cartSlice.reducer;

export const fetchCartItems = (): AppThunk => (dispatch) => {
  dispatch(fetchCart());
};
```

1) Importazioni:
```ts
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';
import { AppThunk } from '../store';
import axios from 'axios';
```
Queste sono le importazioni dei moduli di Redux Toolkit e di axios. 'createSlice' e 'createAsyncThunk' sono funzioni fornite da Redux Toolkit per creare rispettivamente uno slice e un thunk. 'AppThunk' è un tipo che definisce il tipo di un'azione asincrona. Infine 'axios' per effettuare chiamate HTTP.

2) Interfacce:
```ts
interface CartItem {
  id: string;
  name: string;
  price: number;
  quantity: number;
}

interface CartState {
  items: CartItem[];
  loading: boolean;
  error: string | null;
}
```
Queste sono due interfacce che descrivono rispettivamente un elemento del carrello e lo stato del carrello.

3) Stato iniziale:
```ts
const initialState: CartState = {
  items: [],
  loading: false,
  error: null,
};
```

Questa è la definizione dello stato iniziale del carrello. Viene inizializzato con un array vuoto di elementi del carrello, un flag 'loading' impostato su 'false' e una stringa 'error' impostata su 'null'.

4) Thunk asincorno 'fetchCart':
```ts
export const fetchCart = createAsyncThunk(
  'cart/fetchCart',
  async (): Promise<CartItem[]> => {
    try {
      const response = await axios.get('/api/cart');
      return response.data;
    } catch (error) {
      throw error;
    }
  }
);
```
Questo è il codice per creare un thunk asincrono 'fetchCart' che recupera i dati del carrello dall'API. La funzione 'createAsyncThunk' accetta due argomenti: il primo è una stringa che identifica il tipo dell'azione, il secondo è una funzione asincrona che esegue l'effettiva chiamata API. Se la chiamata ha successo, viene restituito il corpo della risposta come array di elementi del carrello. In caso contrario viene lanciata un'eccezione.

5) Slice 'cart'
```ts
const cartSlice = createSlice({
  name: 'cart',
  initialState,
  reducers: {
    addToCart(state, action) {
      const { id, name, price } = action.payload;
      state.items.push({ id, name, price, quantity: 1 });
    },
    removeFromCart(state, action) {
      state.items = state.items.filter(item => item.id !== action.payload);
    },
    incrementQuantity(state, action) {
      const item = state.items.find(item => item.id === action.payload);
      if (item) {
        item.quantity++;
      }
    },
    decrementQuantity(state, action) {
      const item = state.items.find(item => item.id === action.payload);
      if (item && item.quantity > 1) {
        item.quantity--;
      }
    },
  },
  extraReducers: {
    [fetchCart.pending.type]: (state) => {
      state.loading = true;
      state.error = null;
    },
    [fetchCart.fulfilled.type]: (state, action) => {
      state.loading = false;
      state.items = action.payload;
    },
    [fetchCart.rejected.type]: (state, action) => {
      state.loading = false;
      state.error = action.error.message;
    },
  },
});
```
Questo slice di Redux definisce le azioni per gestire il carrello, come 'addToCart', 'removeFromCart', 'incrementQuantity' e 'decrementQuantity'. Inoltre 'extraReducers' viene utilizzato per gestire le azioni di stato del thunk asincrono 'fetchCart' come 'pending', 'fulfilled' e 'rejected'. QUesti gestori di stato impostano i valori di 'loading', 'error' e 'items' in base ai risultati della richiesta HTTP.

6) Esportazinoe delle azioni e dello sato dallo slice:
```ts
export const { addToCart, removeFromCart, incrementQuantity, decrementQuantity } = cartSlice.actions;

export default cartSlice.reducer;

export const selectCartItems = (state: RootState) => state.cart.items;
export const selectCartLoading = (state: RootState) => state.cart.loading;
export const selectCartError = (state: RootState) => state.cart.error;
```
Queste righe esportano le azioni e il reducer dallo slice di Redux. Inoltre vengono definite tre selezioni per accedere allo sato del carrello, 'selectCartItems', 'selectCartLoading' e 'selectCartError'. Queste selezioni possono essere utilizzate in componenti React per accedere allo stato del carrello.

7) Utilizzo delle azioni e dello stato nel componente React: (in un file 'Cart.tsx')
```ts
const Cart: React.FC = () => {
  const dispatch = useDispatch();
  const items = useSelector(selectCartItems);
  const loading = useSelector(selectCartLoading);
  const error = useSelector(selectCartError);

  const handleAddToCart = (id: string, name: string, price: number) => {
    dispatch(addToCart({ id, name, price }));
  };

  const handleRemoveFromCart = (id: string) => {
    dispatch(removeFromCart(id));
  };

  const handleIncrementQuantity = (id: string) => {
    dispatch(incrementQuantity(id));
  };

  const handleDecrementQuantity = (id: string) => {
    dispatch(decrementQuantity(id));
  };

  if (loading) {
    return <div>Loading...</div>;
  }

  if (error) {
    return <div>{error}</div>;
  }

  return (
    <div>
      {items.map(item => (
        <CartItem
          key={item.id}
          id={item.id}
          name={item.name}
          price={item.price}
          quantity={item.quantity}
          onRemove={handleRemoveFromCart}
          onIncrement={handleIncrementQuantity}
          onDecrement={handleDecrementQuantity}
        />
      ))}
      <AddToCartForm onAdd={handleAddToCart} />
    </div>
  );
};
```
In questo componente 'Cart', viene utilizzato 'useDispatch' per accedere alla funzione di dispatch di Redux e 'useSelector' per accedere allo stato del carrello tramite i selectors definiti in precedenza. Viene anche definita una serie di gestori di eventi per gestire le azioni relative al carrello, come 'handleAddToCart', 'handleRemoveFromCart', 'handleIncrementQuantity' e 'hnaldeDecrementQuantity'. QUesti gestori di eventi dispatchano le relative azioni di Redux usando la funzione di dispatch. 

Infine viene visualizzato lo stato del carrello con un messaggio di 'Loading...' se il carrello sta ancora caricando, un messaggio di errore se si è verificato un errore durante il caricamento del carrello o una lista di elementi nel carrello se il carrello è stato caricato con successo.