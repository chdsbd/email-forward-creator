<template lang="html">
    <nav class="navbar navbar-default">
        <div class="container-fluid">
            <div class="navbar-header">
                <a class="navbar-brand" href="/">
                    emails.dignam.xyz
                </a>
            </div>
            <p v-show="login" class="navbar-text">Signed in as <a href="#" class="navbar-link">{{ username }}</a></p>
            <button v-show="login" type="button" class="btn btn-default navbar-btn">Sign out</button>
        </div>
    </nav>
</template>

<script>
export default {
  data: function () {
    return {
        login: false,
        username: 'Christopher Dignam'
    }
  },
  computed: {},
  ready: function () {},
  attached: function () {},
  methods: {},
  components: {}
}
</script>

<style lang="css">
</style>
