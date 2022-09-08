<template>
  <header>
    <router-link to="/">
      <h1>Netflix</h1>
    </router-link>
  </header>
  <main>
    <router-view/>
    </main>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;

  &::selection {
    background: transparentize(#000000, 0.5);
  }
}

body {
  background-color: #0f0f0f; 
}

  a {
    text-decoration: none;
  }

header {
    display: flex;
    
    padding: 10px 16px;
    background-color:#050505;
    box-shadow: 0px 0px 6px rgba(255, 255, 255, 0.1);
}

h1 {
  color: #ff0000;
  font-size: 28px;
}

</style>
