## Redux Toolkit Tutorial

Redux Toolkit provides global state management. Unlike Redux, it has a simpler structure. To use the Redux Toolkit, download the `react-redux` and `@reduxjs/toolkit` packages in your project:

`npm install react-redux @reduxjs/toolkit`

Classic file structure is `store` and `features`. The "store.js" file is in the "store" folder. In the "features" folder, slices are written. You can write the information you want to keep as a global state as a slice component.

![1](https://github.com/user-attachments/assets/f083cd8a-362b-47b3-9dc7-64bb7990a660)

---

## API

### 1. `configureStore()`

It allows to make reducer definitions. Generally, the `store.js` file is created and written inside this file. The store variable uses the configureStore() function and the reducer is defined in the object.

```
import {configureStore} from "@reduxjs/toolkit";

const store = configureStore({
      reducer: ()=> {}
});

export default store;
```

![2](https://github.com/user-attachments/assets/9c6ca6d9-e71b-43b8-8807-4ff36a9d58e7)

### 2. `combineReducers()`

Used to combine reducers. If you have more than one reducer, you can use it.

```
import {configureStore} from "@reduxjs/toolkit";

const rootReducers = combineReducers({
      userReducer,
      postReducer,
      commentReducer,
});

const store = configureStore({
      reducer: rootReducers;
})
```

![3](https://github.com/user-attachments/assets/a5994762-8159-4d2e-ab3d-1e67588f64df)

### 3. `createSlice()`

Allows creating slice components. The information to be kept as a global state is kept as a slice part. `name`, `initialState` and `reducers` definitions should be made in createSlice().

```
import {createSlice} from "@reduxjs/toolkit";

const initialState = {
      currentUser: null
};

export const UserSlice = createSlice({
      name: "user",
      initialState,
      reducers: {
        loginStart: (state)=> {
            state.currentUser = null;
        },
        loginSuccess: (state, action) => {
            state.currentUser = action.payload;
        },
        logout: (state) => {
            state.currentUser = null;
        }
     }
});

export const UserReducer = UserSlice.reducer; // export reducers
export const {loginStart, loginSuccess, logout} = UserSlice.actions; // export actions
```

![4](https://github.com/user-attachments/assets/d0e85e2c-d2fb-41e5-a511-cdd8875277f1)

### 4. `useDispatch()` ve `useSelector()`:

+ `useDispatch()`: Enables the use of defined actions. 

```
import {useDispatch} from "react-redux";
import {loginStart} from "../features/UserSlice.js";

function Home(){

const dispatch = useDispatch();

<button onClick={(event)=> {
          dispatch(loginSuccess({name: username}))
       }}
>Login</button>

}
```

+ `useReducer()`: It is used to access the state information defined in the reducer and to be aware of the changes.

```
import {useDispatch, useSelector} from "react-redux";

function Home(){
   const {currentUser} = useSelector(state => state.user)

   <h2>{currentUser ? `You are logged in, ${currentUser.name}.` : "No auth. Please login."}</h2>
}
```

![5](https://github.com/user-attachments/assets/dfa495b2-58f0-487d-a4fd-08da47e13541)


### 5. Global Provider

![6](https://github.com/user-attachments/assets/25dc5fb6-a796-4a14-ac8c-b120087512e0)




