<script setup>
import { ref } from 'vue';
import HelloWorld from './components/HelloWorld.vue'
import {
  HttpTransportType,
  HubConnectionBuilder,
  HubConnectionState,
  LogLevel,
} from '@microsoft/signalr'

// A conexão com SignalR deve ser alterada aqui ...
const webSocketUrl = 'https://chatweb-api.development.omnyve.com.br/chatwebMessageHub'

const connectionStatus = ref({ message: 'Connectando ao WebSocket...', error: null })

const connection = new HubConnectionBuilder()
  .withUrl(webSocketUrl + '?userIdentity=f43MNAwLeZmdcDPvbdH6&channelKey=123456'    )
  .withAutomaticReconnect()
  .configureLogging(LogLevel.Information)
  .build()

  connection.start().then(() => {
    if (connection.state === HubConnectionState.Connected) {
      connectionStatus.value.message = 'Deu muito bom!!!'
    }

    if (connection.state === HubConnectionState.Disconnected) {
      connectionStatus.value.message = 'Você está desconectado'
    }

  }).catch((error) => {
    connectionStatus.value.message = 'Deum ruim heim...'
    connectionStatus.value.error = error
    console.log(error)
  })

</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld :msg="connectionStatus.message" :url="webSocketUrl" :error="connectionStatus.error" />
    </div>
  </header>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
