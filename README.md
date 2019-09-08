# Redux Root Saga

## Configurable redux-saga execution management

Redux Root Saga provides an easy way to quickly run multiple sagas concurrently in a tested and widely used way.

This package is based on the root saga pattern from the [official documentation](https://redux-saga.js.org/docs/advanced/RootSaga.html) and therefore an easy way to get the described behavior without copy-pasting it into every new project.

Additionally the root saga behavior was extended by the following fully configurable and optional features (more to come):

* Strictly typed and fully Typescript compatible
* Maximum retry count for restarting child sagas
* Default error handling with a warning message including the saga name
* Custom error handling callback

## Example usage

``` typescript
import { createStore, applyMiddleware } from 'redux';
import createSagaMiddleware from '@redux-saga/core';
import { createRootSaga } from 'redux-root-saga';

function* saga1() { /*...*/ }
function* saga2() { /*...*/ }

const rootSaga = createRootSaga([saga1, saga2], {
    maxRetries: 3,
    errorHandler: (error, saga) => console.err(`Error in saga ${saga.name}: ${error}`);
});

const sagaMiddleware = createSagaMiddleware();
const store = createStore(reducer, applyMiddleware(sagaMiddleware));
sagaMiddleware.run(rootSaga);
```
