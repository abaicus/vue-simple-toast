<span>
  <img src="https://badge.fury.io/js/vue-js-simple-toast.svg">
</span> <span>
  <img src="https://img.shields.io/npm/dm/vue-js-simple-toast.svg">
</span> 

# Vue.js simple toast.

### Install

```bash
npm install vue-simple-toast --save
```

### Import

Import plugin:

```javascript
import simpleToast from 'vue-simple-toast'

Vue.use(simpleToast)
```
**OR**

Import component:

```javascript
import { simpleToast } from 'vue-simple-toast'

Vue.component('simpleToast', simpleToast)
```

### Use

```xml
<simple-toast  
    :class="type"
    :type="type"
    :dismissible="true"
    :auto-dismiss="false"
    iconClass="dashicons dashicons-yes"
    message="Options saved."
    >
</simple-toast>
```

### Properties

| Name            | Type              | Default     | Description                        |
| ---             | ---               | ---         | ---                                |
| autoDismiss           | Boolean           | false       | Should the toast auto-dismiss after 1.7s  |
| color     | [String, Object]  | undefined  | If `String` - background color of the toast. <br>If `Object` - background color for the toast in multiple types <br>Example: `{error: 'red', warning: 'yellow', success : 'green'}`   |
| dismissible           | Boolean            | true        | If the toast should be dismissible - adds a dismiss button.   |
| iconClass           | String            | undefined        | Icon class that will be added on the left of the notice   |
| message        | String           | undefined      | **Required** - the toast message |
| type           | String  | `success`  | Can be `['success', 'error', 'warning']`|
