## v-input
Create bootstrap 4 input element

### Descriptions

#### Props
| Props        | Type        | Default Value| Description|
|--------------|:------------|:-------------|:-----------|
|input-type    | String      | row          | Decide which pattern want to use. Available values are `row` and `column`|
|type          | String      | text         | Decide what input want to create. Can be `email`, `date`, `text`, `password`, etc|
|label         | String      | Empty        | **Required**. Input's label |
|name          | String      | Empty        | Required if using traditional form instead of ajax operation|
|input-value   | String      | Empty        | Pass this prop to set default value of input|
|placeholder   | String      | Empty        | Input's placeholder|
|value         | String      | Empty        | Pass in v-model to receive reactive input value|

### Usage

```html
<v-input input-type="row" type="text" label="Email" name="email" input-value="norlihazmey.ghazali@gmail.com" placeholder="Enter Email" v-model="email"></v-input>
```

Will render to following:

```html
<div class="form-group">
    <label>Email</label>
    <input type="text" placeholder="Enter Email" class="form-control" name="email" value="norlihazmey.ghazali@gmail.com"/>
</div>
```

## v-paginate
Create bootstrap 4 laravel's pagination

### Descriptions
#### Props
| Props        | Type        | Default Value| Description|
|--------------|:------------|:-------------|:-----------|
|prev-text     |String       |Previous      | Change previous text's button|
|next-text     |String       |Next          | Change next text's button|
|paginate      |Object       |{}            | Just pass in laravel's pagination javascript object receiving from backend|

#### Methods
| Method Name  | Description|
|--------------|:------------|
| fetch        | Internally used for emitting remote call. Emit along with `url` parameter to parent's method |

#### Event Listener
| Event Listener  | Description|
|-----------------|:------------|
|remote-call      | Pass in method's name from parent component. `v-paginate` will trigger provided function from inside `fetch`'s method

### Usage
```html
<v-pagination :paginate="paginate" v-on:remote-call="getDataFromRemote"></v-pagination>
```

From Javascript
```javascript
// Inside parent component
export default {
    methods: {
        getDataFromRemote(url) {
            // axios.get(url)
        }
    }
}
```

Will render to following:

```html
<nav aria-label="">
    <ul class="pagination">
        <li class="page-item"><a class="page-link">Previous</a></li>
        <li class="page-item active">
            <a href="javascript:void(0);" class="page-link">1 <span class="sr-only">(current)</span></a>
        </li>
        <li class="page-item"><a class="page-link">2</a></li>
        <li class="page-item"><a class="page-link">Next</a></li>
    </ul>
</nav>
```

## v-search
Create search functionality. This component require input to be slot in by using available inputs `v-input`, `v-select`, `v-checkbox`, `v-radio`

### Descriptions
#### Props
| Props          | Type        | Default Value| Description|
|----------------|:------------|:-------------|:-----------|
|btn-search-text |String       |Search        |Change default search's button|
|action          |String       |Empty         |Url to redirect if click search button. Only for traditional form|
|method          |String       |POST          |Available values are `POST`, `PUT`, `DELETE`, `PATCH`, `GET`. Only for traditional form|
|type            |String       |traditional   |Available values are `traditional`, `ajax`|
|form-data       |Object       |{}            |**Required**. `v-search` will look for this formData's object to populate input's values to form a query string parameter 

#### Methods
| Method Name  | Description|
|--------------|:------------|
| search       | Internally used for emitting remote call. Emit along with `queryString` parameter to parent's method|

#### Event Listener
| Event Listener  | Description|
|-----------------|:------------|
|remote-call      | Pass in method's name from parent component. `v-search` will trigger provided function from inside `search`'s method

### Usage
```html
<search v-on:remote-call="getDataFromRemote" :form-data="formData" type="ajax">
    <v-input label="Email" placeholder="Enter Email" v-model="formData.email"></v-input>
</search>
```
From Javascript
```javascript
// Inside parent component
export default {
    data() {
        return {
            formData: {
                email: ''
            }
        }
    },
    methods: {
        getDataFromRemote(queryString) {
            // 
        }
    }
}
```
