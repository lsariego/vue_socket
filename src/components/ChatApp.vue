<template>
    <h1>Chat</h1>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-12 col-md-8">
                <button @click="sendMessage()">Enviar código</button>
            </div>
        </div>
    </div>
</template>

<script>
import io from 'socket.io-client';

export default {
  name: 'ChatApp',
  data: function() {
    return {
        active: 0,
    }
  },
  methods: {
    sendMessage() {
        this.socketInstance.emit('message', 2022);
        this.active = 1;
    },
    respondMessage() {
        if (this.active === 0 ) {
            this.socketInstance.emit('message', 'ok');
            this.active = 1;
        }
        return;
    }
  },
  created: function() {
    this.socketInstance = io('http://localhost:3000');

    this.socketInstance.on(
        'message:received', (data) => {
            console.log(data);
            this.respondMessage();
        }
    )
  },
}
</script>