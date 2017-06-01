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

## Ajax Example
``` bash
<template>
  <vue-awesomplete :ajax="ajax"></vue-awesomplete>
</template>

<script>
  import VueAwesomplete from 'vue-awesomplete'

  export default {
    data() {
      return {
        ajax: {
          callback: function (response) {
            return response.map(function(i) {
              return i.name
            })
          },
          url: 'https://restcountries.eu/rest/v1/lang/fr'
        }
      }
    },

    components: {
      VueAwesomplete
    }
  }
</script>
```

## Props
| Prop            | Type          | Description  |
| ----------------|:--------------|--------------|
| close           | Function      | Callback when the popup just closed |
| highlight       | Function      | Callback when the highlighted item just changed |
| open            | Function      | Callback when the popup just opened |
| select          | Function      | Callback when the user has made a selection but it has not been applied yet |
| select-complete | Function      | Callback when the user has made a selection and it has been applied yet |
| setting         | Object        | Setting of Awesomplete |
| ajax            | Object        | Setting of ajax request. There are three properties:<br>1. callback<br>Callback of ajax request. You must return array.<br>2. method<br>Set method of ajax request. Default using GET method.<br>3. url<br>Set url of ajax request

## License
vue-awesomplete is released under the MIT License.
