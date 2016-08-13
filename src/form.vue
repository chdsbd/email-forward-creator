<template lang="html">
    <form>
        <h3>Manual input</h3>
        <div class="form-group">
            <label for="incoming">Incoming Email</label>
            <input type="email" v-model="incoming" class="form-control" id="incoming" placeholder="Incoming Email">
        </div>
        <div class="form-group">
            <label for="outgoing">Outgoing Email</label>
            <input type="email" v-model="outgoing" class="form-control" id="outgoing" placeholder="Incoming Email" @keyup.enter="addUser">
        </div>
        <button type="button" @click="addUser" class="btn btn-block btn-primary btn-large" name="button">Add Forward</button>
    </form>
</template>

<script>
    export default {
        data: function() {
            return {
                incoming: '',
                outgoing: ''
            }
        },
        computed: {
            formFilled: function() {
                return (this.incoming != '' && this.outgoing !== '')
            }
        },
        ready: function() {},
        attached: function() {},
        methods: {
            addUser: function() {
                if (!this.formFilled) {
                    let data = {
                        type: 'danger',
                        message: 'The form wasn\'t fully filled.'
                    }
                    this.$dispatch('triggerAlert', data)
                    return;
                }
                let re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
                if (!re.test(this.incoming) || !re.test(this.outgoing)){
                    let data = {
                        type: 'danger',
                        message: 'Invalid email'
                    }
                    this.$dispatch('triggerAlert', data)
                    return;
                }
                if (this.incoming === this.outgoing){
                    let data = {
                        type: 'danger',
                        message: 'Duplicate Emails, they must be different'
                    }
                    this.$dispatch('triggerAlert', data)
                    return;
                }

                let data = { in: this.incoming,
                    out: this.outgoing
                }
                this.$dispatch('new-forward', data)
                this.incoming = '',
                    this.outgoing = ''
            }
        }
    }
</script>

<style lang="css">

</style>
