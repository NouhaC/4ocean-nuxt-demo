<template>
  <header class="site-header">
    <router-link to="/" class="logo" >
      <img class="logo" src="https://wesaidgotravel.com/wp-content/uploads/2017/06/4Ocean.png" alt="4Ocean Logo">
    </router-link>
    <nav>
      <ul>
        <li v-for="menuLink in menuLinks" :key="menuLink.id">
          <prismic-link :field="menuLink.link">{{ $prismic.richTextAsPlain(menuLink.label) }}</prismic-link>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'HeaderPrismic',
  data () {
    return {
      menuContent: [],
      menuLinks: []
    }
  },
  methods: {
    getMenu () {
      //Query to get menu content
      this.$prismic.client.getSingle('menu')
        .then((menuContent) => {
          this.menuContent = menuContent
          this.menuLinks = menuContent.data.menu_links
        })
    },
  },
  created () {
    this.getMenu()
  }
}
</script>

<style>
/* Site header */
.site-header {
  height: 40px;
  padding: 20px 0;
  background-position: center center;
  background-size: cover;
  color: #0057B8;
  line-height: 2;
  text-align: center;
}
.site-header,
.site-header a {
  color: #484d52;
  font-weight: 700;
  left: 2px;
}
.site-header nav a:hover {
  color: #72767B;
}
.homepage .site-header,
.homepage .site-header a {
  color: #0057B8;
}
.homepage .site-header nav a:hover {
  color: #c8c9cb;
}
.site-header .logo {
  position: absolute;
  left: 5%;
  display: inline-block;
  width: 100px;
}
.site-header nav {
  float: right;
}
.site-header nav ul {
  margin: 0;
}
.site-header nav li {
  display: inline-block;
  margin-left: 40px;
}

/* Media Queries */
@media (max-width: 1060px) {
  .site-header {
    padding-left: 20px;
    padding-right: 20px;
  }
}
@media (max-width: 767px) {
  .site-header {
    height: auto;
  }
  .homepage .site-header {
    position: absolute;
    left: 0;
    right: 0;
  }
  .site-header .logo {
    display: block;
    text-align: center;
  }
  .site-header nav {
    float: none;
    text-align: center;
  }
  .site-header nav li {
    display: inline-block;
    margin-left: 10px;
    margin-right: 10px;
  }
}
</style>

