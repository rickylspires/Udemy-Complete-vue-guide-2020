<template>
  <div>
    <h3>Some User Details</h3>
    <p>User has id: {{ $route.params.id }}</p>
    <router-link
      tag="button"
      :to="{ name: 'userEdit', params: { id: $route.params.id } }"
      class="btn btn-primary"
    >Edit User</router-link>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        link: {
          name: 'userEdit',
          params: {
            id: this.$route.params.id
          },
          query: {
            locale: 'en',
            q: 100
          },
          hash: '#data'
        }
      }
    },
    beforeRouteEnter: (to, from, next) => {
      console.log('route UserDetail beforeRouteEnter')
      //object not init here, yet
      if (true) {
        next()
      }else{
        next(false)
      }
    }
  }
</script>
