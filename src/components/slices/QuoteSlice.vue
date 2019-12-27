<template>
  <section class='content-section quote'>
    <blockquote class="block-quotation">{{ $prismic.richTextAsPlain(slice.primary.quote_text) }}</blockquote>
  </section>
</template>

<script>
export default {
  props: ['slice'],
  name: 'quote-slice'
}
</script>

<style scoped>
.quote blockquote {
  display: block;
  font-family: 'SlatePro-Medium'; 
  font-size: 20px;
  font-style:normal;
  font-weight: normal; 
  color: navy; 
  background-color:white;
  letter-spacing : 1.14;
  line-height: 1.5em;
  text-align: center;
}
.quote blockquote:before,
.quote blockquote:after {
  color:white;
  content: open-quote;
  font-family: 'SlatePro-Medium';
  font-size: 2.5em;
  font-weight: 900;
  line-height: 0.1em;
  margin-left: 10px;
  margin-right: 10px;
  vertical-align: -0.3em;
}
.quote blockquote:after {
  content: close-quote;
}
/* Media Queries */
@media (max-width: 767px) {
  .quote {
    font-size: 20px;
  }
}
</style>
