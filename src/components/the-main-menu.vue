<template>
  <div class="nav-parent-wrapper">
    <a
      class="hidden-close"
      @click="setMenuClosed"
    ></a>
    <nav id="menu" >
      <a
        class="close-button"
        @click="setMenuClosed"
      >
        Close
      </a>
      <div class="nav-wrapper">
        <p class="nav-label">Menu</p>
        <ul>
          <router-link
            to="/"
            exact
            role="presentation"
            tag="li"
          >
            <a>Home</a>
          </router-link>
          <router-link
            :to="{
              name: 'page-detail',
              params: {
                slug: 'about-travel-adventures'
              }
            }"
            role="presentation"
            tag="li"
          >
            <a>About The Blog</a>
          </router-link>
          <router-link
            :to="{ name: 'activity-index' }"
            role="presentation"
            tag="li"
          >
            <a>Explore By Activity</a>
          </router-link>
          <router-link
            :to="{ name: 'author-index' }"
            role="presentation"
            tag="li"
          >
            <a>Our Authors</a>
          </router-link>
        </ul>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      isOpen: false
    }
  },
  methods: {
    setMenuClosed: function () {
      this.isOpen = false
    },
    setMenuOpen: function () {
      this.isOpen = true
    },
    toggleClassOnHtmlRoot () {
      const htmlTag = document.getElementsByTagName('html')[0]
      if (this.isOpen) {
        htmlTag.classList.add('menu-active')
      } else {
        htmlTag.classList.remove('menu-active')
      }
    }
  },
  created () {
    this.$eventBus.$on('menu-open', () => {
      this.setMenuOpen()
    })
  },
  watch: {
    isOpen: {
      handler: 'toggleClassOnHtmlRoot',
      immediate: true
    },
    '$route': {
      handler: 'setMenuClosed'
    }
  }
}
</script>
