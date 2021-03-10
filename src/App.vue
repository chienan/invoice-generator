<template>
  <div id="invoice-generator">
    <router-view />
  </div>
</template>

<script>
import "bootstrap";
import "bootstrap/dist/css/bootstrap.min.css";
export default {
  name: "App"
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Raleway:wght@100;400;800&display=swap");

/* CSS reset */
body {
  margin: 0;
  padding: 0;
}
* {
  box-sizing: border-box;
  font-family: "Raleway", sans-serif;
}
h1,
h2,
h3,
h4,
h5,
h6,
p {
  margin: 0px;
  padding: 0px;
}

ul,
ol,
li {
  list-style: none;
  margin: 0px;
  padding: 0px;
}
a,
a:hover,
a:focus {
  text-decoration: none;
}
img {
  display: block;
  object-fit: cover;
}
.btn,
button,
button:focus,
input:focus,
textarea:focus,
select,
select:focus,
a:focus {
  outline: 0px !important;
}
button {
  background-color: transparent;
  border: 0;
  cursor: pointer;
}
button[disabled] {
  pointer-events: none;
}

input {
  padding: 0;
  background: transparent;
  border-radius: 5px;
}
input:required {
  box-shadow: none;
}
input:invalid {
  box-shadow: none;
}

input:hover {
  border: 1px solid #4a4aff;
}

input:focus {
  border: 1px solid #9bd2ed;
}
</style>
