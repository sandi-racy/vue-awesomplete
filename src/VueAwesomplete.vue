<template lang="jade">
    input(type='text', v-model="internalValue")
</template>

<script>
    import Awesomplete from 'awesomplete'

    export default {
        props: {
            ajax: {
                type: Object,
                default() {
                    return {
                        callback: function(){},
                        method: 'GET',
                        url: ''
                    }
                }
            },

            close: Function,

            highlight: Function,

            open: Function,

            select: Function,

            selectComplete: {
                type: Function,
                default: function(){}
            },

            setting: {
                type: Object,
                default() {
                    return {}
                }
            },

            value: String,
        },

        data() {
            return {
                internalValue: ''
            }
        },

        mounted() {
            let self = this
            let input = this.$el

            if (this.ajaxUrl == '') {
                new Awesomplete(input, this.setting)
            } else {
                let ajax = new XMLHttpRequest();
                ajax.open(this.ajax.method, this.ajax.url, true);
                ajax.onload = function() {
                    let response = JSON.parse(ajax.responseText)
                    let list = self.ajax.callback(response)
                    self.setting.list = list
                    new Awesomplete(input, self.setting)
                };
                ajax.send()
            }

            input.addEventListener('awesomplete-select', this.select)
            input.addEventListener('awesomplete-selectcomplete', () => {
                self.internalValue = input.value
                this.selectComplete()
            })
            input.addEventListener('awesomplete-open', this.open)
            input.addEventListener('awesomplete-close', this.close)
            input.addEventListener('awesomplete-highlight', this.highlight)
        },

        watch: {
            internalValue() {
                this.$emit('input', this.internalValue)
            }
        },

        created() {
            this.internalValue = this.value
        }
    }
</script>
