<template>
  <div>
    <b-navbar type="is-black">
      <template slot="brand">
        <b-navbar-item tag="router-link" :to="{ path: '/' }">
          <h1>E2 Tools</h1>
        </b-navbar-item>
      </template>
      <template slot="start">
        <!-- <b-navbar-item tag="router-link" :to="{ path: '/' }">Home</b-navbar-item> -->
        <template v-for="(item, key) of items">
          <b-navbar-item :key="key" :href="item.to">
            {{ item.title }}
            <b-icon :icon="item.icon" />
          </b-navbar-item>
        </template>
      </template>

      <!-- <template slot="end">
        <b-navbar-item tag="div">
          <div class="buttons">
            <a class="button is-primary">
              <strong>Sign up</strong>
            </a>
            <a class="button is-light">Log in</a>
          </div>
        </b-navbar-item>
      </template>-->
    </b-navbar>

    <section class="main-content columns">
      <aside class="column is-2 section"></aside>
      <!-- <aside class="column is-2 section">
        <p class="menu-label is-hidden-touch">General</p>
        <ul class="menu-list">
          <li v-for="(item, key) of items" :key="key">
            <nuxt-link :to="item.to" exact-active-class="is-active">
              <b-icon :icon="item.icon" />
              {{ item.title }}
            </nuxt-link>
          </li>
        </ul>
      </aside>-->

      <div class="container column is-8">
        <nuxt />
      </div>

      <aside class="column is-2 section"></aside>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          title: 'Email',
          icon: 'email',
          to: '/email-templates'
        },
        {
          title: 'Behaviours',
          icon: 'beaker',
          to: '/behaviours'
        },
        {
          title: 'Case Change',
          icon: 'android-studio',
          to: '/case-change'
        },
        {
          title: 'Convert JSON',
          icon: 'autorenew',
          to: '/convert-json'
        },
        {
          title: 'Copy',
          icon: 'copy',
          to: '/copy-text'
        },
        {
          title: 'Collection Build',
          icon: 'beaker',
          to: '/masscollection'
        }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
span.icon {
  padding-left: 15px;
}
</style>
