# Redux 專案

## 專案結構

## 專案入口 Index.js
``` javascript
import React from 'react';
import { createRoot } from 'react-dom/client';
import { Provider } from 'react-redux';
import { store } from './app/store';
import App from './App';
import './index.css';

const container = document.getElementById('root');
const root = createRoot(container);

root.render(
    <Provider store={store}>
      <App />
    </Provider>
);
```

## Store
``` javascript
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from '../features/counter/counterSlice';
import productReducer from '../features/products/productSlice';
import cartReducer from '../features/cart/cartSlice';

export const store = configureStore({
  reducer: {
    counter: counterReducer,
    products: productReducer,
    cart: cartReducer
  },
});
```

## Product List
### Get product list
``` javascript
import { createAsyncThunk, createSlice } from '@reduxjs/toolkit';
import { fetchProducts } from './productAPI';

export const getProducts = createAsyncThunk(
  'products/fetchProducts',
  async () => {
    const response = await fetchProducts()
    return response.data
  }
)
```

### Reducer
``` javascript
import { createAsyncThunk, createSlice } from '@reduxjs/toolkit';

const initialState = {
  items: []
}

export const productSlice = createSlice({
  name: 'products',
  initialState,
  reducers: {
  },
  extraReducers: (builder) => {
    builder
      .addCase(getProducts.fulfilled, (state, action) => {
        state.items = action.payload;
      });
  },
});

export const selectProducts = (state) => state.products.items;

export default productSlice.reducer;
```
``` javascript
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from '../features/counter'
import productReducer from '../features/products/productSlice';

export const store = configureStore({
  reducer: {
    products: productReducer
  },
});
```
### GUI
``` javascript
import React, { useEffect } from 'react'
import { useSelector, useDispatch } from 'react-redux'
import Grid from '@mui/material/Grid'
import Stack from '@mui/material/Stack'
import { selectProducts, getProducts } from './productSlice'
import { addToCart } from '../cart/cartSlice'
import ProductCard from '../../components/ProductCard'

export function Products() {
    const products = useSelector(selectProducts)
    const dispatch = useDispatch()

    useEffect(() => {
        dispatch(getProducts())
    }, [])

    const addHandler = (data) => {
        dispatch(addToCart(data))
    }

    return (
        <Grid item xs={6}>
            <Stack direction="row" spacing={2} >
                {
                    products.map(data =>
                        <ProductCard key={data.id} data={data} add={addHandler} />
                    )
                }
            </Stack>
        </Grid>
    );
}
```

``` javascript
import React from 'react'
import Card from '@mui/material/Card'
import CardActions from '@mui/material/CardActions'
import CardContent from '@mui/material/CardContent'
import Button from '@mui/material/Button'
import Typography from '@mui/material/Typography'

export default function ProductCard({data, add}) {
    return (
        <Card variant="outlined" style={{ width: '10vw' }}>
            <div key={data.id}>
                <CardContent>
                    <Typography variant="h5" component="div">
                        {data.name}
                    </Typography>
                    <Typography sx={{ mb: 1.5 }} color="text.secondary">
                        $ {data.price}
                    </Typography>
                </CardContent>
                <CardActions>
                    <Button onClick={() => add(data)} size="small">Add</Button>
                </CardActions>
            </div>
        </Card >
    );
}
```

# Add to Cart

``` javascript
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
    productInCart: []
}

export const cartSlice = createSlice({
    name: 'cart',
    initialState,
    reducers: {
        addToCart: (state, action) => {
            state.productInCart.push({ ...action.payload, count: 1 })
        }
    }
});

export const selectProductInCart = (state) => state.cart.productInCart;

export const { addToCart } = cartSlice.actions;

export default cartSlice.reducer;
```


``` javascript
import { configureStore } from '@reduxjs/toolkit';
import productReducer from '../features/products/productSlice';
import cartReducer from '../features/cart/cartSlice';

export const store = configureStore({
  reducer: {
    products: productReducer,
    cart: cartReducer
  },
});
```

## Cart List
``` javascript
import React from 'react'
import { useSelector, useDispatch } from 'react-redux'
import Grid from '@mui/material/Grid';
import Table from '@mui/material/Table';
import TableBody from '@mui/material/TableBody';
import TableCell from '@mui/material/TableCell';
import TableContainer from '@mui/material/TableContainer';
import TableHead from '@mui/material/TableHead';
import TableRow from '@mui/material/TableRow';
import Paper from '@mui/material/Paper';
import { selectProductInCart, increment, decrement, removeFromCart } from './cartSlice'
import CartTable from '../../components//CartTable'

export function Cart() {
    const productInCart = useSelector(selectProductInCart)
    console.log()
    const dispatch = useDispatch()
    const caculateTotal = () => {
        return productInCart.map(data => data.price * data.count)
            .reduce((tempSum, current) => current + tempSum, 0)
    }
    return (
        <Grid item xs={6}>
            <TableContainer component={Paper}>
                <Table aria-label="simple table">
                    <TableHead>
                        <TableRow>
                            <TableCell align="center"></TableCell>
                            <TableCell>Product</TableCell>
                            <TableCell align="center">Price</TableCell>
                            <TableCell align="center">Count</TableCell>
                            <TableCell align="center">Price</TableCell>
                        </TableRow>
                    </TableHead>
                    <TableBody>
                        {productInCart.map((row) => (
                            <CartTable
                                key={row.id}
                                data={row}
                                decrement={() => dispatch(decrement(row.id))}
                                increment={() => dispatch(increment(row.id))}
                                removeFromCart={() => dispatch(removeFromCart(row.id))}
                            />
                        ))}
                        <TableRow>
                            <TableCell colSpan={3} />
                            <TableCell colSpan={1} align="center">Subtotal</TableCell>
                            <TableCell align="center">{caculateTotal()}</TableCell>
                        </TableRow>
                    </TableBody>
                </Table>
            </TableContainer>
        </Grid>
    );
}
```

``` javascript
import React from 'react'
import Button from '@mui/material/Button'
import TableCell from '@mui/material/TableCell'
import TableRow from '@mui/material/TableRow'

export default function CartTable({data, decrement, increment, removeFromCart}) {
    return (
        <TableRow key={data.id}>
            <TableCell align="center">
                <Button onClick={() => removeFromCart(data.id)}>X</Button>
            </TableCell>
            <TableCell component="th" scope="row">{data.name}</TableCell>
            <TableCell align="center">{data.price}</TableCell>
            <TableCell align="center">
                <Button onClick={() => decrement(data.id)} size="small">-</Button>
                {data.count}
                <Button onClick={() => increment(data.id)} size="small">+</Button>
            </TableCell>
            <TableCell align="center">{data.count * data.price}</TableCell>
        </TableRow>
    );
}
```

## increase / decrease
``` javascript
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
    productInCart: []
}

export const cartSlice = createSlice({
    name: 'cart',
    initialState,
    reducers: {
        addToCart: (state, action) => {
            state.productInCart.push({ ...action.payload, count: 1 })
        },
        increment: (state, { payload }) => {
            const itemIndex = state.productInCart.findIndex(item => item.id === payload);
            state.productInCart[itemIndex].count += 1;
        },
        decrement: (state, { payload }) => {
            const itemIndex = state.productInCart.findIndex(item => item.id === payload);
            if (state.productInCart[itemIndex].count === 1) {
                state.productInCart = state.productInCart.filter(prod => prod.id !== payload)
            } else {
                state.productInCart[itemIndex].count -= 1;
            }
        },
    }
});

export const selectProductInCart = (state) => state.cart.productInCart;

export const { addToCart, increment, decrement } = cartSlice.actions;

export default cartSlice.reducer;
```

## Remove item
``` javascript
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
    productInCart: []
}

export const cartSlice = createSlice({
    name: 'cart',
    initialState,
    reducers: {
        addToCart: (state, action) => {...},
        increment: (state, { payload }) => {...},
        decrement: (state, { payload }) => {...},
        removeFromCart: (state, { payload }) => {
            state.productInCart = state.productInCart.filter(prod =>
                prod.id !== payload
            )
        },
    }
});

export const selectProductInCart = (state) => state.cart.productInCart;

export const { addToCart, increment, decrement, removeFromCart } = cartSlice.actions;

export default cartSlice.reducer;
```

``` javascript

```