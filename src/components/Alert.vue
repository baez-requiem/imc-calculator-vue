<template>
  <div v-if="hasShow" class="overlay">
    <div class="alert" :class="classColor">
      <h2>{{ msg }}</h2>
      <div class="btn-content">
        <button @click="$emit('onClose')">Entendi</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .overlay {
    position: absolute;
    z-index: 999;
    top: 0;
    left: 0;
    
    display: flex;
    justify-content: center;
    align-items: center;

    height: 100vh;
    width: 100vw;

    background-color: #0007;
  }

  .alert {
    padding: 1rem;
    color: #f5f5f5;
    border-radius: 5px;
  }

  .btn-content {
    display: flex;
    justify-content: flex-end;
  }

  button {
    border: 2px solid #fff;
    border-radius: 5px;

    display: flex;
    justify-content: center;
    align-items: center;

    padding: .5rem 1rem;
    margin-top: 1rem;
    cursor: pointer;
    height: 36px;
    transition: all .2s;
    
    background-color: transparent;
    color: #fff;
    font-weight: bold;
  }

  button:hover {
    filter: brightness(.8);
  }
</style>

<script>
  export default {
    name: 'Alert',
    props: ['color', 'message', 'show'],
    emits: ['onClose'],
    data() {
      return {
        hasShow: this.show,
        classColor: this.color,
        msg: this.message
      }
    }
  }
</script>