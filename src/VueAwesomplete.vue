<template lang="jade">
    input(type='text')
</template>

<script>
    import Awesomplete from 'awesomplete'

    export default {
        props: {
            ajaxCallback: {
                type: Function
            },

            ajaxMethod: {
                type: String,
                default: 'GET'
            },

            ajaxUrl: {
                type: String,
                default: ''
            },

            close: {
                type: Function
            },

            highlight: {
                type: Function
            },

            open: {
                type: Function
            },

            select: {
                type: Function
            },

            selectComplete: {
                type: Function
            },

            setting: {
                type: Object,
                default: {}
            }
        },

        mounted() {
            let self = this
            let input = this.$el

            if (this.ajaxUrl == '') {
                new Awesomplete(input, this.setting)
            } else {
                let ajax = new XMLHttpRequest();
                ajax.open(this.ajaxMethod, this.ajaxUrl, true);
                ajax.onload = function() {
                    let response = JSON.parse(ajax.responseText)
                    let list = self.ajaxCallback(response)
                    self.setting.list = list
                    new Awesomplete(input, self.setting)
                };
                ajax.send()
            }

            input.addEventListener('awesomplete-select', this.select)
            input.addEventListener('awesomplete-selectcomplete', this.selectComplete)
            input.addEventListener('awesomplete-open', this.open)
            input.addEventListener('awesomplete-close', this.close)
            input.addEventListener('awesomplete-highlight', this.highlight)
        }
    }
</script>
