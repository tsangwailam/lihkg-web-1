<template>
  <div id="offcanvas-categories" class="uk-offcanvas">
    <div class="uk-offcanvas-bar">
      <ul class="uk-nav uk-nav-offcanvas">
        <li>
          <div class="uk-grid uk-grid-collapse offcanvas-header">
            <div class="uk-width-1-2" @click="closeOffcanvas">
              <router-link to="/category/1">
                LIHKG 討論區
              </router-link>
            </div>
            <div class="uk-width-1-2">
              <a href="#modal-setting" data-uk-modal>
                <span class="uk-icon-cog"></span> 設定
              </a>
            </div>
          </div>
        </li>
        <li
          v-for="category in allCategories"
          :key="category.cat_id"
          :class="{'uk-active': activeCategory ? category.cat_id === activeCategory.cat_id : false}"
          @click="closeOffcanvas">
          <router-link :to="'/category/' + category.cat_id">
            {{ category.name }}
          </router-link>
        </li>
        <li>
          <a href="#modal-about" data-uk-modal>關於本站</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
/* global UIkit */
import { mapActions } from 'vuex'

export default {
  name: 'offcanvas',
  computed: {
    activeCategory () {
      return this.$store.getters.activeCategory
    },
    allCategories () {
      return this.$store.state.categories.categories
    }
  },
  methods: {
    ...mapActions([
      'fetchCategories'
    ]),
    closeOffcanvas () {
      UIkit.offcanvas.hide()
      document.body.scrollTop = document.documentElement.scrollTop = 0
    }
  }
}
</script>

<style lang="stylus">
.uk-offcanvas-bar {
  box-shadow: 1px 1px 4px 1px #000;

  &:after {
    display: none;
  }

  .is-safari & {
    background: rgba(#222, 0.7);
    backdrop-filter: blur(10px);
  }
}

.offcanvas-header {
  a {
    display: block;
    padding: 10px 15px;
    text-align: center;
  }
}
</style>
