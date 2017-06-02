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

You can even set it (or override it) later and it will just work
``` bash
<template>
  <vue-awesomplete :setting="{ list: ['Html', 'CSS', 'Javascript', 'PHP'] }" ref="skills"></vue-awesomplete>
  <button @click="changeSkills">Change Skills</button>
</template>

<script>
  import VueAwesomplete from 'vue-awesomplete'

  export default {
    methods: {
      changeSkills() {
        this.$refs.skills.list(['Angular', 'React', 'Vue'])
      }
    },
  
    components: {
      VueAwesomplete
    }
  }
</script>
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
| Name            | Type          | Description  |
| ----------------|:--------------|--------------|
| setting         | Object        | Setting of Awesomplete |
| ajax            | Object        | Setting of ajax request. There are three properties:<br>1. callback<br>Callback of ajax request. You must return array.<br>2. method<br>Set method of ajax request. Default using GET method.<br>3. url<br>Set url of ajax request

## Methods
| Name            | Description  |
| ----------------|:--------------|
| close()         |	Closes the popup. |
| destroy()       |	Clean up and remove the instance from the input. |
| evaluate()      |	Evaluates the current state of the widget and regenerates the list of suggestions or closes the popup if none are available. You need to call it if you dynamically set list while the popup is open. |
| goto(i)         |	Highlights the item with index i in the popup (-1 to deselect all). Avoid using this directly and try to use next() or previous() instead when possible. |
| next()          |	Highlights the next item in the popup. |
| open()          | Opens the popup. |
| previous()      |	Highlights the previous item in the popup. |
| select()        |	Selects the currently highlighted item, replaces the text field’s value with it and closes the popup. |

## Events
| Name            | Description  |
| ----------------|:--------------|
| close           | The popup just closed. |
| highlight       | The highlighted item just changed. |
| open            | The popup just appeared. |
| select          | The user has made a selection (either via pressing enter or clicking on an item), but it has not been applied yet. |
| selectcomplete  | The user has made a selection (either via pressing enter or clicking on an item), and it has been applied |

## License
vue-awesomplete is released under the MIT License.
