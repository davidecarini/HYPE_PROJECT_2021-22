<!--
  Component: TheFooter
  Description: Footer of the website with company icon(linked to the homepage), social icons and links to other pages.
-->
<template>
  <!-- Footer -->
  <footer class="page-footer text-center text-lg-start text-muted">
    <!-- Section: Links  -->
    <section class="container10">
      <div class="container text-center text-md-start mt-5">
        <!-- Grid row -->
        <div class="row mt-3">

          <!-- Grid column -->
          <div class="col-md-3 col-lg-4 col-xl-3 mx-auto mb-4">
            <a href="/"><img class="logo" src="~/static/logoCompatto_bianco.png" alt="logo_compatto_bianco"></a>
          </div>
          <!-- Grid column -->

          <!-- Grid column -->
          <div class=" col-md-2 col-lg-2 col-xl-2 mx-auto mb-4">
            <p><a href="/contattaci" class="text">> Contattaci</a></p>
            <p><a href="/bolognainbreve" class="text">> Bologna in Breve</a></p>
          </div>

          <!-- Grid column -->
          <div class=" col-md-2 col-lg-2 col-xl-2 mx-auto mb-4">
            <p><a target="_blank" href="https://www.bolognatoday.it/meteo/" class="text">> Meteo</a></p>
            <p><a target="_blank" href="https://www.skylinewebcams.com/en/webcam/italia/emilia-romagna/bologna/bologna-torre-degli-asinelli.html" class="text">> Webcam</a></p>
          </div>

          <!-- Grid column -->
          <div class="col-md-3 col-lg-2 col-xl-2 mx-auto mb-4">
            <!-- Links -->
            <p><a title="areaLegale" href="/arealegale" class="text">> Area Legale</a></p>
            <p><a title="privacy" href="/privacy" class="text">> Informativa Privacy</a></p>
          </div>

        </div>

      </div>
    </section>

    <!-- Section: Social media -->
    <section
      class="container2 d-flex justify-content-center justify-content-lg-between p-4 border-bottom">
      <!-- Left -->
      <div class="me-5 d-none d-lg-block">© 2022 Tutti i diritti sono riservati.</div>

      <!-- Right -->
      <div>
        <span>Seguici su:</span>
        <a target="_blank" href="https://www.facebook.com" class="me-1 text-reset"> <i class="mdi mdi-facebook"></i>facebook</a>
        <a target="_blank" href="https://www.twitter.com" class="me-1 text-reset"><i class="mdi mdi-twitter"></i>twitter</a>
        <a target="_blank" href="https://www.instagram.com" class="me-1 text-reset"><i class="mdi mdi-instagram"></i>instagram</a>
      </div>
    </section>
  </footer>
</template>

<script>
  export default {
    name: 'TheFooter',
  }
</script>

<style scoped>
footer{
  bottom: 0;
}
.container10{
  background-color: #c13939;
  color: white;
  border-bottom: 1px solid #F2F2F2;
}
.container2{
  background-color: #c13939;
  color: white;
}
.logo{
  margin: auto;
}
img{
  float:inherit;
  width:130px;
}
.mdi{
  color:white
}
/* Color of social icons on mouse */
.mdi-facebook{
  font-size: 25px;
}
.mdi-twitter{
  font-size: 25px;
}
.mdi-instagram{
  font-size: 25px;
}
/* Color of social icons on mouse hover */
.mdi-twitter:hover {
  color: black;
}
.mdi-facebook:hover {
  color: black;
}
.mdi-instagram:hover {
  color: black;
}
/* Color of links on mouse hover */
.text:hover {
  color: black;
  font-weight: bold ;
}
/* text of the link */
.text{
  color:white;
  text-decoration: none; /* Eliminate the underline */
}
/* font size of the generic span (Seguici su:) */
span{
  font-size: 22px;
}
</style>
