<template lang="jade">
    div
        vue-awesomplete(ajax-url='https://restcountries.eu/rest/v1/lang/fr', :ajax-callback='callback')
</template>

<script>
    import VueAwesomplete from './VueAwesomplete.vue'

    export default {
        data() {
            return {
                callback: function (response) {
                    return response.map(function(i) {
                        return i.name
                    })
                },
                editor: {
                    select: function () {
                        alert('xy')
                    }
                },
                setting: {
                    editor: {
                        list: ['Atom', 'Sublime', 'Bracket', 'Notepad++'],
                        minChars: 0
                    },
                    programmingLanguage: {
                        list: ['Ada', 'Java', 'JavaScript', 'Brainfuck', 'LOLCODE', 'Node.js', 'Ruby on Rails'],
                        minChars: 0
                    }
                }
            }
        },

		components: {
			VueAwesomplete
		}
	}
</script>
