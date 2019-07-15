## v-input
Create bootstrap 4 input element

### Descriptions

#### Props
| Props        | Type        | Default Value| Description|
|--------------|:------------|:-------------|:-----------|
|input-type     | String      | row          | Decide which pattern want to use. Available values are `row` and `column`|
|type          | String      | text         | Decide what input want to create. Can be `email`, `date`, `text`, `password`, etc|
|label         | String      | null         | **Required**. Input's label |
|name          | String      | null         | Required if using traditional form instead of ajax operation|
|input-value    | String      | null         | Pass this prop to set default value of input|
|placeholder   | String      | null         | Input's placeholder|
|value         | String      | null         | Pass in v-model to receive reactive input value|

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
| fetch        | Internally used for emitting remote call|

#### Event Listener
| Event Listener  | Description|
|-----------------|:------------|
|remote-call      | Pass in method's name from parent component. `v-paginate` will trigger provided function from inside `fetch`'s method

### Usage
```html
<v-pagination :paginate="paginate" v-on:remote-call="getDataFromRemote"></v-pagination>
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
 
