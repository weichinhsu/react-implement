# Redux 專案

## 專案結構

## 專案入口 Index.js
``` javascript
import React from 'react'
import ReactDOM from 'react-dom/client'
import { Provider } from 'react-redux'
import store from './store'
import './index.css'
import App from './pages/App'
import reportWebVitals from './reportWebVitals'

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(
  <Provider store={store}>
    <App />
  </Provider>
);
```
## Store
``` javascript
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import reducers from './reducers';
import * as api from './services/api';

const store = createStore(
    reducers,
    applyMiddleware(thunk.withExtraArgument({ api }))
);
  
export default store;
```
## Product List
### Get product list
``` javascript
export const get_products = () => {
    return (dispatch, getState, { api }) => {
        const products = api.get_products()
        dispatch({
            type: 'PRODUCTS', payload: products
        })
    };
};
```

### Reducer
``` javascript
export default (state =  null , action) => {
    switch (action.type) {
        case 'PRODUCTS':
            return action.payload;
        default:
            return state;
    }
};
```
``` javascript
import { combineReducers } from 'redux';
import products from './products';

const root_reducers = combineReducers({
    products
})

export default root_reducers;
```
### GUI
``` javascript
import React, { Component } from 'react'
import { connect } from 'react-redux'
import Grid from '@mui/material/Grid'
import Stack from '@mui/material/Stack'
import { get_products } from '../actions/products'
import { add_to_cart } from '../actions/cart'
import ProductCard from '../components/ProductCard'


class Product extends Component {
    componentDidMount() {
        this.props.getProducts()
    }

    addHandler = (data) => {
        this.props.addToCart(data)
    }

    render() {
        return (
            <Grid item xs={6}>
                <Stack direction="row" spacing={2} >
                    {
                        this.props.products.map(data =>
                            <ProductCard key={data.id} data={data} add={this.addHandler} />
                        )
                    }
                </Stack>
            </Grid>
        );
    }
}

const mapStateToProps = (state) => ({
    products: state.products ? state.products : []
})

const mapDispatchToProps = {
    getProducts: get_products,
    addToCart: add_to_cart
}

export default connect(mapStateToProps, mapDispatchToProps)(Product);
```

```javascript
import React, { Component } from 'react'
import Card from '@mui/material/Card'
import CardActions from '@mui/material/CardActions'
import CardContent from '@mui/material/CardContent'
import Button from '@mui/material/Button'
import Typography from '@mui/material/Typography'


class ProductCard extends Component {
    render() {
        return (
            <Card variant="outlined" style={{ width: '10vw' }}>
                <CardContent>
                    <Typography variant="h5" component="div">
                        {this.props.data.name}
                    </Typography>
                    <Typography sx={{ mb: 1.5 }} color="text.secondary">
                        $ {this.props.data.price}
                    </Typography>
                </CardContent>
                <CardActions>
                    <Button onClick={() => this.props.add(this.props.data)} size="small">Add</Button>
                </CardActions>
            </Card >
        )
    }
}

export default ProductCard
```

# Add to Cart

``` javascript
export const add_to_cart = (data) => {
    return (dispatch, getState, { api }) => {
        dispatch({
            type: 'ADD_PRODUCT', payload: data
        })
    }
}
```

``` javascript
export default (state = [], action) => {
    switch (action.type) {
        case 'ADD_PRODUCT':
            return [
                ...state,
                {
                    ...action.payload,
                    count: 1
                }
            ]
        default:
            return state;
    }
};
```

``` javascript
import { combineReducers } from 'redux';
import products from './products';
import cart from './cart';

const root_reducers = combineReducers({
    products,
    cart
})

export default root_reducers;
```

## Cart List
``` javascript
import React, { Component } from 'react'
import { connect } from 'react-redux'
import Grid from '@mui/material/Grid'
import { increase_quality, decrease_quality, remove_product } from '../actions/cart'
import CartTable from '../components/CartTable'


class Cart extends Component {
    render() {
        return (
            <Grid item xs={6}>
                <CartTable
                    cart={this.props.cart}
                    increaseQuality={this.props.increaseQuality}
                    decreaseQuality={this.props.decreaseQuality}
                    removeProduct={this.props.removeProduct} />
            </Grid>
        );
    }
}

const mapStateToProps = (state) => ({
    cart: state.cart ? state.cart : []
})

const mapDispatchToProps = {
    increaseQuality: increase_quality,
    decreaseQuality: decrease_quality,
    removeProduct: remove_product
}

export default connect(mapStateToProps, mapDispatchToProps)(Cart);
```

``` javascript
import React, { Component } from 'react'
import Button from '@mui/material/Button'
import Table from '@mui/material/Table'
import TableBody from '@mui/material/TableBody'
import TableCell from '@mui/material/TableCell'
import TableContainer from '@mui/material/TableContainer'
import TableHead from '@mui/material/TableHead'
import TableRow from '@mui/material/TableRow'
import Paper from '@mui/material/Paper'


class CartTable extends Component {

    caculateTotal = () => {
        return this.props.cart.map(data => data.price * data.count)
            .reduce((tempSum, current) => current + tempSum, 0)
    }

    render() {
        return (
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
                        {this.props.cart.map((row) => (
                            <TableRow key={row.id}>
                                <TableCell align="center">
                                    <Button onClick={() => this.props.removeProduct(row.id)}>X</Button>
                                </TableCell>
                                <TableCell component="th" scope="row">{row.name}</TableCell>
                                <TableCell align="center">{row.price}</TableCell>
                                <TableCell align="center">
                                    <Button onClick={() => this.props.decreaseQuality(row.id)} size="small">-</Button>
                                    {row.count}
                                    <Button onClick={() => this.props.increaseQuality(row.id)} size="small">+</Button>
                                </TableCell>
                                <TableCell align="center">{row.count * row.price}</TableCell>
                            </TableRow>
                        ))}
                        <TableRow>
                            <TableCell colSpan={3} />
                            <TableCell colSpan={1} align="center">Subtotal</TableCell>
                            <TableCell align="center">{this.caculateTotal()}</TableCell>
                        </TableRow>
                    </TableBody>
                </Table>
            </TableContainer>
        )
    }
}

export default CartTable

```

## increase / decrease
``` javascript
export const increase_quality = (id) => {
    return (dispatch, getState, { api }) => {
        dispatch({
            type: 'INCREASE_QUANTITY', payload: id
        })
    }
}
```

``` javascript
export const decrease_quality = (id) => {
    return (dispatch, getState, { api }) => {
        const product = getState().cart.find(prod => prod.id === id)
        if (product.count === 1) {
            dispatch({
                type: 'DELETE_PRODUCT', payload: id
            })
        } else {
            dispatch({
                type: 'DECREASE_QUANTITY', payload: id
            })
        }
    }
}
```

``` javascript
export default (state = [], action) => {
    switch (action.type) {
        case 'ADD_PRODUCT':
            ...
        case 'INCREASE_QUANTITY':
            // let addedItem = state.find(item=> item.id === action.payload)
            // addedItem.count += addedItem.count
            state.map(prod =>
                prod.id === action.payload ? { ...prod, count: prod.count++ } : prod
            )
            return [
                ...state
            ]
        case 'DECREASE_QUANTITY':
            state.map(prod =>
                prod.id === action.payload ? { ...prod, count: prod.count-- } : prod
            )
            return [
                ...state
            ]
        default:
            return state;
    }
};

```
## Remove item
``` javascript
export const remove_product = (id) => {
    return (dispatch, getState, { api }) => {
        dispatch({
            type: 'DELETE_PRODUCT', payload: id
        })
    }
}
```

``` javascript
export default (state = [], action) => {
    switch (action.type) {
        case 'ADD_PRODUCT':
            ...
        case 'INCREASE_QUANTITY':
            ...
        case 'DECREASE_QUANTITY':
            ...
        case 'DELETE_PRODUCT':
            return state.filter(prod =>
                prod.id !== action.payload
            )
        default:
            return state;
    }
};

```

``` javascript

```