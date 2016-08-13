<template lang="html">
    <table class="table">
        <th>#</th>
        <th>Incoming</th>
        <th>Outgoing</th>
        <th>Enabled</th>
        <th>
            <button type="button" title="Click to edit forward" class="btn btn-xs btn-default" disabled><span class="glyphicon glyphicon-edit"></span></button>
            <button type="button" title="Double click to delete forward" class="btn btn-xs btn-danger" disabled><span class="glyphicon glyphicon-trash"></span></button>
        </th>
        <tr v-for="(index, forward) in forwards" :class="{'text-muted':!forward.enabled}">
            <td>{{ index + 1 }}</td>
            <td>{{ forward.incoming }}</td>
            <td>{{ forward.outgoing }}</td>
            <td>
                <div class="btn-group" role="group">
                    <button type="button" @click="toggleEnabled(forward)" class="btn btn-default" :class="{'active btn-info':forward.enabled}"><span class="glyphicon glyphicon-ok"></span></button>
                    <button type="button" @click="toggleEnabled(forward)" class="btn btn-default" :class="{'active btn-warning':!forward.enabled}"><span class="glyphicon glyphicon-remove"></span></button>
                </div>
            </td>
            <td>
                <button type="button" title="Click to edit forward" @click="toggleEditing(forward)" class="btn btn-xs btn-default"><span class="glyphicon glyphicon-edit"></span></button>
                <button type="button" title="Double click to delete forward" @click="deleteItem(forward)" class="btn btn-xs btn-danger"><span class="glyphicon glyphicon-trash"></span></button>
            </td>
        </tr>
    </table>
</template>

<script>
    export default {
        data: function() {
            return {}
        },
        props: ['forwards'],
        computed: {},
        ready: function() {},
        attached: function() {},
        methods: {
            toggleEnabled: function(item) {
                item.enabled = !item.enabled;
            },
            toggleEditing: function(item) {
                item.editing = !item.editing
            },
            deleteItem: function(item) {
                this.forwards.$remove(item)
            }
        },
        components: {}
    }
</script>

<style lang="css">

</style>
