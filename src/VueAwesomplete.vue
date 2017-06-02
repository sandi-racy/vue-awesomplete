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
                        url: null
                    }
                }
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
                awesomplete: null,
                internalValue: null
            }
        },

        methods: {
            close() {
                this.awesomplete.close()
            },

            destroy() {
                this.awesomplete.destroy()
            },

            evaluate() {
                this.awesomplete.evaluate()
            },

            goto(index) {
                this.awesomplete.goto(index)
            },

            list(list) {
                this.awesomplete.list = list
            },

            next() {
                this.awesomplete.next()
            },

            open() {
                this.awesomplete.open()
            },

            previous() {
                this.awesomplete.previous()
            },

            select() {
                this.awesomplete.select()
            }
        },

        mounted() {
            let self = this
            let input = this.$el

            if (this.ajax.url) {
                if (typeof this.ajax.method == 'undefined') {
                    this.ajax.method = 'GET'
                }

                let ajax = new XMLHttpRequest();
                ajax.open(this.ajax.method, this.ajax.url, true);
                ajax.onload = function() {
                    let response = JSON.parse(ajax.responseText)
                    let list = self.ajax.callback(response)
                    self.setting.list = list
                    self.awesomplete = new Awesomplete(input, self.setting)
                };
                ajax.send()
            } else {
                this.awesomplete = new Awesomplete(input, this.setting)
            }

            input.addEventListener('awesomplete-select', () => {
                this.$emit('select')
            })

            input.addEventListener('awesomplete-selectcomplete', () => {
                self.internalValue = input.value
                this.$emit('selectcomplete')
            })

            input.addEventListener('awesomplete-open', () => {
                this.$emit('open')
            })

            input.addEventListener('awesomplete-close', () => {
                this.$emit('close')
            })

            input.addEventListener('awesomplete-highlight', () => {
                this.$emit('highlight')
            })
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
