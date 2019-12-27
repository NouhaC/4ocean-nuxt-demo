<template>
  <section class="homepage">
    <!-- Vue tag to add header component -->
    <header-prismic />
    <!-- Button to edit document in dashboard -->
    <prismic-edit-button :documentId="documentId" />
    <section class="homepage-banner">
      <video class="banner-video" poster="https://cdn11.bigcommerce.com/s-amir6jyttl/product_images/uploaded_images/screen-shot-2019-11-01-at-10.53.11-am.jpg?t=1572620181" playsInline autoPlay muted="muted" loop >
        <source src= "https://firebasestorage.googleapis.com/v0/b/trash-tracker-49de1.appspot.com/o/4oceanSiteVideos%2Fheader%20video.mp4?alt=media&token=0d860e97-b2e7-4657-b933-2d4cdeed1246" type='video/mp4' />
      </video>
      <div class="banner-content container">
        <!-- Template for page title. -->
        <h2 class="banner-title">
          {{ $prismic.richTextAsPlain(fields.title) }}
        </h2>
        <!-- Template for page tagline -->
        <p class="banner-description">{{ $prismic.richTextAsPlain(fields.tagline) }}</p>
        <prismic-link class="banner-button" :field="fields.button_link">
          {{ $prismic.richTextAsPlain(fields.button_label) }}</prismic-link>
      </div>
    </section>
    <div class="container">
      <!-- Slices block component -->
      <slices-block :slices="slices" />
    </div>
  </section>
</template>

<script>
// imports for all components
import HeaderPrismic from "../components/HeaderPrismic.vue";
import SlicesBlock from "../components/SlicesBlock.vue";

export default {
  name: "home-page",
  components: {
    HeaderPrismic,
    SlicesBlock
  },
  data() {
    return {
      documentId: "",
      fields: {
        title: null,
        tagline: null,
        image: null,
        video: null,
        button_link: null,
        button_label: null
      },
      slices: []
    };
  },
  methods: {
    getContent() {
      //Query to get home content
      this.$prismic.client.getSingle("homepage").then(document => {
        if (document) {
          this.documentId = document.id;
          const banner = document.data.homepage_banner[0];
          this.fields.image = banner.image.url;
          this.fields.title = banner.title;
          this.fields.video = banner.video.url;
          this.fields.tagline = banner.tagline;
          this.fields.button_link = banner.button_link;
          this.fields.button_label = banner.button_label;

          //Set slices as variable
          this.slices = document.data.page_content;
        } else {
          //returns error page
          this.$router.push({ name: "not-found" });
        }
      });
    }
  },
  created() {
    this.getContent();
  }
};
</script>

<style>
.homepage-banner {
  margin: -70px 0 0px;
  padding: 10px 0 10px 0;
  background-position: center center;
  background-size: cover;
  color: #ffffff;
  line-height: 1.75;
  text-align: center;
}
.banner-video {
  padding: 10px 0 10px 0;
  position: static;
  width: 100%;
  height: 100%;
}
.banner-content {
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.banner-title,
.banner-description {
  width: 100%;
  max-width: 490px;
  margin-left: auto;
  margin-right: auto;
}
.banner-title {
  color: #ffffff;
  font-size: 70px;
  font-weight: 900;
  line-height: 70px;
}
.banner-button {
  background: #ffffff;
  border-radius: 7px;
  color: #484d52;
  font-size: 14px;
  font-weight: 700;
  padding: 15px 40px;
}
.banner-button:hover {
  background: #c8c9cb;
}
/* Media Queries */
@media (max-width: 767px) {
  .homepage-banner {
    margin: 0 0 40px;
    padding: 10em 0 6em;
  }
  .banner-title {
    font-size: 50px;
    line-height: 50px;
  }
  .text-section-2col {
    -webkit-column-count: 1; /* Chrome, Safari, Opera */
    -moz-column-count: 1; /* Firefox */
    column-count: 1;
    -webkit-column-gap: 40px; /* Chrome, Safari, Opera */
    -moz-column-gap: 40px; /* Firefox */
    column-gap: 40px;
  }
  .quote {
    font-size: 20px;
  }
  .gallery-item {
    -webkit-box-flex: 100%;
    -moz-box-flex: 100%;
    -webkit-flex: 100%;
    -ms-flex: 100%;
    flex: 100%;
  }
  .highlight-left,
  .highlight-right {
    width: 100%;
    float: none;
  }
}
</style>
