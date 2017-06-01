# vue-awesomplete
Vue wrapper for Awesomplete

## Install
``` bash
yarn add vue-awesomplete
```

## Basic Usage
``` bash
<template>
  <vue-awesomplete :setting="{ list: ['Html', 'CSS', 'Javascript', 'PHP'] }"></vue-awesomplete>
</template>

<script>
  import VueAwesomplete from 'vue-awesomplete'
  
  export default {
    components: {
      VueAwesomplete
    }
  }
</script>
```
Dont forget to include awesomplete.css
``` bash
<link rel="stylesheet" href="awesomplete.css" />
```
Or if you use style-loader and css-loader
``` bash
import AwesompleteCss from 'awesomplete/awesomplete.css'
```

## Props
| Prop            | Type          | Description  |
| ----------------|:--------------|--------------|
| ajax-method     | String        | Set method of ajax request |
| ajax-url        | String        | Set url of ajax request |
| close           | Function      | Callback when the popup just closed |
| highlight       | Function      | Callback when the highlighted item just changed |
| open            | Function      | Callback when the popup just opened |
| select          | Function      | Callback when the user has made a selection but it has not been applied yet |
| select-complete | Function      | Callback when the user has made a selection and it has been applied yet |
| setting         | Object        | Setting of Awesomplete |

## License
vue-awesomplete is released under the MIT License.
