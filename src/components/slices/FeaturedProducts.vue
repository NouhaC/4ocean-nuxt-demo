<template>
  <section class='featured-products content-section'>
    <div class="gallery">
      <div v-for="item in slice.items" :key="item.id" class="gallery-item">
        <img :src="item.catalog.image_url" class="gallery-item-img"/>
        <h3>{{ item.catalog.title }}</h3>
        <p>{{ item.catalog.description}}</p>
        <p>
          <prismic-link :field="item.button_link" class="gallery-link">{{ $prismic.richTextAsPlain(item.button_label) }}</prismic-link>
        </p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: ['slice'],
  name: 'featured-products'
}
</script>

<style scoped>
.gallery {
    display: -webkit-box;  /* OLD - iOS 6-, Safari 3.1-6, BB7 */
    display: -ms-flexbox;  /* TWEENER - IE 10 */
    display: -webkit-flex; /* NEW - Safari 6.1+. iOS 7.1+, BB10 */
    display: flex;
    -webkit-flex-wrap: wrap;
    flex-wrap: wrap;
    -webkit-justify-content: space-between; 
    justify-content: space-between; 
    /*display: -webkit-box; /* OLD - iOS 6-, Safari 3.1-6, BB7 */
    /* display: -ms-flexbox; /* TWEENER - IE 10 */ 
    /* display: -webkit-flex; /* NEW - Safari 6.1+. iOS 7.1+, BB10 */
    /* display: flex;
    -webkit-flex-wrap: wrap;
    flex-wrap: wrap;
    -webkit-justify-content: space-between;
    justify-content: space-between */
}

.gallery-item {
  -webkit-box-flex: 0 1 48%;
  -moz-box-flex:  0 1 48%;
  -webkit-flex:  0 1 48%;
  -ms-flex:  0 1 48%;
  flex: 0 1 20%;
  /* -webkit-box-flex: 0 1 48%;
  -moz-box-flex: 0 1 48%;
  -webkit-flex: 0 1 48%;
  -ms-flex: 0 1 48%;
  flex: 0 1 48% */
}

.gallery-item-img {
    max-width: 100%;
    height: 100px;
    display: block;
    margin-left: auto;
    margin-right: auto;
}

.gallery-link {
  margin-top: -20px;
  text-transform: uppercase;
/*  margin-top: -20px;
  text-transform: uppercase; */
}

@media (max-width: 767px) {
  .gallery {
    margin-bottom: 2rem
  }
  .gallery-item {
    -webkit-box-flex: 100%;
    -moz-box-flex:  100%;
    -webkit-flex:  100%;
    -ms-flex:  100%;
    flex: 100%;
    /* -webkit-box-flex: 100%;
    -moz-box-flex: 100%;
    -webkit-flex: 100%;
    -ms-flex: 100%;
    flex: 100%; */
  }
}
</style>