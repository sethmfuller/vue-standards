# Vue Standards - Vuex
Formal standards for how Vuex should be constructed and used

## Instantiation

- Install vuex with `npm install vuex`
- Import vuex with `import Vuex from 'vuex'` in main.js
- Inject vuex into all the components of the vue project by using `Vue.use(Vuex);` in main.js
- Create Vuex store object via `const store = new Vuex.Store({/* config parameters */});` in main.js
    - Parameters include
        - state
        - getters
        - mutations
        - actions
    - **State**: a single object that contains all application level state and serves as the "single source of truth". Usually you will have only one store for each application. A single state tree makes it straightforward to locate a specific piece of state, and allows us to easily take snapshots of the current app state for debugging purposes.
    - **Getters**: computed properties for stores. Like computed properties, a getter's result is cached based on its dependencies, and will only re-evaluate when some of its dependencies have changed.
    - **Mutations**: very similar to events: each mutation has a string type and a handler. The handler function is where we perform actual state modifications, and it will receive the state as the first argument. 
        - You cannot directly call a mutation handler. Think of it more like event registration: "When a mutation with type increment is triggered, call this handler." To invoke a mutation handler, you need to call `store.commit({type: 'mutation-name'});` with its type.
    - **Actions**: Instead of mutating the state, actions commit mutations. Actions can contain arbitrary asynchronous operations. 
        - Actions are triggered with `store.dispatch('mutation-name');`
        - This may look dumb at first sight: if we want to increment the count, why don't we just call store.commit('increment') directly? Remember that mutations have to be synchronous? Actions don't. We can perform asynchronous operations inside an action.
- Add the `store` object into the Vue object instantiated in the main.js file.

## Vuex Store Operations in Single-File Components

- Since the Vuex is injected into ever single-file component from the main.js, we are able to access the vue store by `this.$store`
- To access state `this.$store.state.youStateVar`
- To trigger a getter `this.$store.getters.getterName`
- To commit a mutation `this.$store.commit('mutation-name');`
- To trigger an action `this.$store.dispatch('mutation-name);`
- To integrate the store's state into the computed section of a single-file component use the mapState helper
    - First import the help by putting `import { mapState } from 'vuex'` in your single-file component
    - Then use the spread operator and the helper in the computed section like
        ```javascript
        computed: { 
            localComputedProperty() { 
                return blah;
            }, 
            
            ...mapState({ 
                stateVar: state => state.stateVar
            }) 
        }
        ```
- To integrate the store's getters into the computed section of a single-file component use the mapGetters helper
    - First import the help by putting `import { mapGetters } from 'vuex'` in your single-file component
    - Then use the spread operator and the helper in the computed section like 
        ```javascript
        computed: { 
            localComputedProperty() { 
                return blah;
            }, 
            
            ...mapGetters([
                'getterName', 
                'anotherGetterName'
            ]) 
        }
        ```
