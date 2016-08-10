<template>
    <div id="root">
        <navbar></navbar>
        <login v-if="!login"></login>
        <div v-if="login" class="container">
            <alert :show.sync="alert.show" :duration="5000" :type="alert.type" width="400px" placement="top" dismissable>
                <span class="glyphicon glyphicon-info-sign"></span>
                <strong>Uh oh!</strong>
                <p>{{ alert.msg }}</p>
            </alert>
            <div class="page-header">
                <h1>Email Forwarder <small>Modify email forwards here</small></h1>
            </div>
            <div class="row">
                <div class="col-md-4">
                    <vueform></vueform>
                </div>
                <div class="col-md-8">
                    <vuetable :forwards="forwards"></vuetable>
                </div>
            </div>
            <div class="row">
                <div class="col-md-6">
                    <cmdinput :forwards.sync="forwards"></cmdinput>
                </div>
                <div class="col-md-6">
                    <cmdoutput :forwards="forwards"></cmdoutput>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import navbar from './navbar.vue'
    import login from './login.vue'
    import vueform from './form.vue'
    import vuetable from './table.vue'
    import {
        alert
    } from 'vue-strap'
    import cmdoutput from './cmdOutput.vue'
    import cmdinput from './cmdInput.vue'

    export default {
        components: {
            alert,
            navbar,
            login,
            vueform,
            vuetable,
            cmdoutput,
            cmdinput
        },
        data() {
            return {
                login: true,
                forwards: [{
                    incoming: 'ex@example.com',
                    outgoing: 'ex@gmail.com',
                    enabled: true,
                    editing: false
                }, {
                    incoming: 'ex2@anydomain.com',
                    outgoing: 'ex2@yahoo.com',
                    enabled: false,
                    editing: false
                }, {
                    incoming: 'bill@smith.com',
                    outgoing: 'bill.smith@gmail.com',
                    enabled: true,
                    editing: false
                }],
                alert: {
                    show: false,
                    type: 'danger',
                    msg: 'Your input was incorrect!'
                }
            }
        },
        events: {
            'new-forward': function(msg) {
                let forward = {
                    incoming: msg.in,
                    outgoing: msg.out,
                    enabled: true,
                    editing: false
                }
                this.forwards.push(forward)
            },
            'triggerAlert': function(msg) {
                this.alert.show = true,
                    this.alert.type = msg.type,
                    this.alert.msg = msg.message
            },
            'inputData': function(msg) {
                msg.forEach(item => {
                    let forward = {
                        incoming: item.in,
                        outgoing: item.out,
                        enabled: item.enabled,
                        editing: false
                    }
                    this.forwards.push(forward)
                    this.$broadcast('clear-input')
                })
            }
        }
    }
</script>
