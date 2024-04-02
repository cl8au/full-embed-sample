<template>
  <div class="App">
    <AppHeader/>
    <div class="App__content">
      <router-view/>
    </div>
    <div class="App__footer"></div>
  </div>
</template>

<script>
  import AppHeader from "@/components/AppHeader";

  export default {
    components: {
      AppHeader
    },
    mounted() {
      window.addEventListener('message', this.handleMessage);
    },
    beforeDestroy() {
      window.removeEventListener('message', this.handleMessage);
    },
    methods: {
      handleMessage(event) {
        if (typeof event.data === 'string' || event.data instanceof String) {
          const data = JSON.parse(event.data);
          console.log(`IVE-38: receive message ${JSON.stringify(data)}`)
          switch (data.type) {
            case 'navigated':
              console.log('IVE-38: navigated event is received, we can add custom logic here...');
              if (data.payload.url === '/dashboard/audit') {
                window.location.href = "/activities";
              }
              break;
            case 'heightChange':
              console.log('IVE-38: heightChange event is received, we can add custom logic here...');
              break;
            case 'connectionStatusChange':
              console.log('IVE-38: connectionStatusChange event is received, we can add custom logic here...');
              break;
            case 'error':
              console.log('IVE-38: error event is received, we can add custom logic here...');
              console.log(`IVE-38: error event: ${data.payload.message}`);
              break;
          }
        }
      },
    },
  }
</script>

<style lang="scss">
  .App {
    height: 100%;
    display: flex;
    flex-direction: column;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;

    &__content {
      flex: 1 1 auto;
      display: flex;
      align-items: stretch;
    }

    &__footer {
      flex: 0 0 auto;
      height: 50px;
      background: #33373e;
    }
  }
</style>

<style lang="scss">
  // Global styles

  @font-face {
    font-family: "Source Sans Pro";
    font-style: normal;
    font-weight: 300;
    src: local("Source Sans Pro Light"), local("SourceSansPro-Light"),
    url("/webfonts/Source_Sans_Pro/Light.woff2") format("woff2"),
    url("/webfonts/Source_Sans_Pro/Light.woff") format("woff");
  }

  @font-face {
    font-family: "Source Sans Pro";
    font-style: normal;
    font-weight: 400;
    src: local("Source Sans Pro Regular"), local("SourceSansPro-Regular"),
    url("/webfonts/Source_Sans_Pro/Regular.woff2") format("woff2"),
    url("/webfonts/Source_Sans_Pro/Regular.woff") format("woff");

  }

  @font-face {
    font-family: "Source Sans Pro";
    font-style: normal;
    font-weight: 700;
    src: local("Source Sans Pro SemiBold"), local("SourceSansPro-SemiBold"),
    url("/webfonts/Source_Sans_Pro/SemiBold.woff2") format("woff2"),
    url("/webfonts/Source_Sans_Pro/SemiBold.woff") format("woff");
  }

  @font-face {
    font-family: "Source Sans Pro";
    font-style: normal;
    font-weight: 900;
    src: local("Source Sans Pro Bold"), local("SourceSansPro-Bold"),
    url("/webfonts/Source_Sans_Pro/Bold.woff2") format("woff2"),
    url("/webfonts/Source_Sans_Pro/Bold.woff") format("woff");
  }

  * {
    box-sizing: border-box;
  }

  body {
    margin: 0;
    background: #f9f9f9;
  }

  body,
  button {
    font-family: "Source Sans Pro", Helvetica, Arial, sans-serif;
  }

  body, html {
    height: 100%;
  }

  .button {
    cursor: pointer;
    background: #34373E;
    color: #fff;
    font-size: 14px;
    font-weight: bold;
    border: none;
    padding: 10px 12px;
    border-radius: 2px;

    &_link {
      &:link,
      &:visited,
      &:hover,
      &:active {
        text-decoration: none;
      }
    }

    &_block {
      display: block;
      width: 100%;
      text-align: left;
    }

    .fas {
      margin-right: 5px;
    }
  }
</style>
