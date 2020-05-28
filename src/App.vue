<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  font-size: 16px;
  min-height: 100vh;
}

html,
body,
div,
header,
main,
ul,
li,
ol,
p,
span,
h1,
h2,
h3,
h4,
h5,
h6,
button,
input,
textarea {
  margin: 0;
  padding: 0;
  list-style: none;
  box-sizing: border-box;
  outline: none;
}
h1 {
  font-size: 5.378em;
  font-weight: lighter;
  color: #222;
}
h2 {
  font-size: 3.842em;
  color: #222;
}
h3 {
  font-size: 2.744em;
  color: #222;
}
h4 {
  font-size: 1.96em;
  color: #222;
}
h5 {
  font-size: 1.4em;
  color: #222;
}
input, textarea {
  border: 1px solid #dddddd;
  border-radius: 2px;
  padding: 8px 12px;
}
button, .button {
  border: 1px solid #ccc;
  border-radius: 2px;
  padding: 8px 12px;
  background-color: white;
  cursor: pointer;
  color: #222;
  &_primary {
    background-color: #999;
    border-color: #999;
    color: white;
  }
}
</style>
