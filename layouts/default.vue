<template>
  <div>
    <nuxt/>
  </div>
</template>

<style>
  html {
    font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
    font-size: 16px;
    word-spacing: 1px;
    -ms-text-size-adjust: 100%;
    -webkit-text-size-adjust: 100%;
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
    box-sizing: border-box;
  }

  *,
  *:before,
  *:after {
    box-sizing: border-box;
    margin: 0;
  }

  body {
    margin-top: 20px;
  }

  .container {
    padding: 15px;

    box-shadow: 0 0 5px 0 #e4e4e4;
    border: 1px solid #e4e4e4;
  }

  @media print {
    .container {
      box-shadow: none;
      border: none;
    }
  }
</style>
