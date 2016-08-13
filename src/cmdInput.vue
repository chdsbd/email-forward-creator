<template lang="html">
    <div>
        <h3>Data from server <small><code>/etc/postfix/virtual</code></small></h3>
        <textarea class="form-control" v-model="inputText" placeholder="Paste config file from server here" rows="3"></textarea>
        <br>
        <button class="btn btn-primary" @click="updateList" type="button" name="button">Update list</button>
    </div>
</template>

<script>
    export default {
        data: function() {
            return {
                inputText: ''
            }
        },
        computed: {
            parsed: function() {
                let inputLines = this.inputText.trim().split('\n').map(line => line.trim())
                let forwards = inputLines.map(line => {
                    let forward = { in: '',
                        out: '',
                        enabled: true
                    }
                    let forwardProperties = line.split(' ').map(property => property.trim())
                    forwardProperties.forEach(prop => {
                        if (prop === '#') {
                            return forward.enabled = false;
                        }
                        if (forward.in === '') {
                            return forward.in = prop;
                        }
                        if (forward.out === '') {
                            return forward.out = prop;
                        } else {
                            console.error('Too many arguments')
                        }
                    })

                    return forward
                })
                return forwards
            }
        },
        ready: function() {},
        attached: function() {},
        methods: {
            updateList: function() {
                this.$dispatch('inputData', this.parsed)
                this.inputText = ''
            }
        },
        components: {}
    }
</script>

<style lang="css">

</style>
