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

input, textarea {
  border: 1px solid #dddddd;
  border-radius: 2px;
  padding: 8px 12px;
  font-size: 14px;
}
button {
  border: 1px solid #ccc;
  border-radius: 2px;
  padding: 8px 12px;
  background-color: white;
  cursor: pointer;
  font-size: 14px;
}
</style>
