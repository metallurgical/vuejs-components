## v-input
### Descriptions
| Props        | Type        | Default Value| Description|
|--------------|:------------|:-------------|:-----------|
|inputType     | String      | row          | Decide which pattern want to use. Available values are `row` and `column`|
|type          | String      | text         | Decide what input want to create. Can be `email`, `date`, `text`, `password`, etc|
|label         | String      | null         | **Required**. Input's label |
|name          | String      | null         | Required if using traditional form instead of ajax operation|
|inputValue    | String      | null         | Pass this prop to set default value of input|
|placeholder   | String      | null         | Input's placeholder|
|value         | String      | null         | Pass in v-model to receive reactive input value|

### Usage
```html
<v-input input-type="row" type="text" label="Email" name="email" input-value="norlihazmey.ghazali@gmail.com" placeholder="Enter Email" v-model="email"></v-input>
```

Will Render to following:

```html
<div class="form-group">
    <label>Email</label>
    <input type="text" placeholder="Enter Email" class="form-control" name="email" value="norlihazmey.ghazali@gmail.com"/>
</div>
```
 
