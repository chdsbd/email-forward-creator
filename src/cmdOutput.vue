<template lang="html">
    <div>
        <h3>Code for server <small>Paste into terminal</small></h3>
        <pre><button @click="selectText('output')" type="button" class="btn btn-sm btn-default pull-right" name="button">Select text</button><code id='output'>{{ output }}</code></pre>
    </div>
</template>

<script>
    String.prototype.format = function() {
        var formatted = this;
        for (var i = 0; i < arguments.length; i++) {
            var regexp = new RegExp('\\{' + i + '\\}', 'gi');
            formatted = formatted.replace(regexp, arguments[i]);
        }
        return formatted;
    };

    export default {
        data: function() {
            return {}
        },
        props: ['forwards'],
        computed: {
            output: function() {
                let data = ''
                for (let forward of this.forwards) {
                    let row = '\n';
                    if (!forward.enabled) {
                        row += '# ';
                    }
                    row += forward.incoming + ' ' + forward.outgoing;
                    data += row;
                }
                let openFile = 'echo "{0}" > /etc/postfix/virtual && sudo postmap /etc/postfix/virtual'.format(data)
                return openFile
            }
        },
        watch: {
            'output': function(oldVal, newVal) {
                this.selectText('output');
            }
        },
        ready: function() {
            this.selectText('output');
        },
        attached: function() {},
        methods: {
            selectText: function(element) {
                var elem = document.getElementById(element);
                var selection = window.getSelection();
                var range = document.createRange();
                selection.removeAllRanges();
                range.selectNodeContents(elem);
                selection.addRange(range);
            }
        },
        components: {}
    }
</script>

<style lang="css">

</style>
