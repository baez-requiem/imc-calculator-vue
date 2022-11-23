<style scoped>
  section {
    display: flex;
    flex-direction: column;
  }

  h2 {
    font-size: 2.2rem;
    color: #222;
    margin-bottom: 1rem;
  }

  p {
    color: #555;
    margin-bottom: 2rem;
  }

  .d-grid {
    display: grid;
  }

  input {
    border: none;
    border-bottom: 2px solid #c5c5c5;

    display: flex;
    justify-content: center;

    height: 28px;
    margin-bottom: 1rem;
    padding: 0 .25rem;
    background-color: transparent;
  }

  button {
    border: none;
    border-radius: 5px;

    display: flex;
    justify-content: center;
    align-items: center;

    margin-top: 2rem;
    cursor: pointer;
    height: 36px;
    transition: all .2s;
    
    background-color: #0d6efd;
    color: #fff;
  }

  button:disabled {
    transition: none;
    background-color: #555 !important;
    pointer-events: none;
  }

  button:hover {
    background-color: #084298;
  }

</style>

<template>
  <section class="w-full-md px-3">
    <h2>Calcule o seu IMC</h2>

    <p>
      IMC é a sigla para Índice de Massa Corpórea, parâmetro adotado pela Organização Mundial de Saúde para calcular o peso ideal de cada pessoa.
    </p>

    <div class="d-grid">
      <input
        type="number"
        step="0.1"
        min="0"
        placeholder="Digite a sua altura. Ex: 1.5 (em metros)"
        :disabled="disabled"
        :value="form.height"
        @input="e => form.height = e.target.value"
      >
      <input
        type="number"
        step="1"
        min="0"
        placeholder="Digite o seu peso. Ex: 75.45 (em kg)"
        :disabled="disabled"
        :value="form.wheight"
        @input="e => form.wheight = e.target.value"
      >
      <button
        @click="calculateResult"
        :disabled="disabled"
      >Calcular</button>
    </div>
  </section>
  <AlertVue
    :show="showAlert"
    :key="'alert-'+showAlert"
    :message="alertProps.message"
    :color="alertProps.color"
    @onClose="closeAlert"
  />
</template>

<script>
  import AlertVue from './Alert.vue'

  export default {
    name: "Form",
    components: { AlertVue },
    emits: ['setResult'],
    data() {
      return {
        form: {
          height: '',
          wheight: ''
        },
        disabled: false,
        showAlert: false,
        alertProps: {
          color: 'bg-red',
          message: 'Preencha os campos corretamente.'
        }
      }
    },
    methods: {
      calculateResult: function() {
        const { height, wheight} = this.form

        if (!height || !wheight) {
          this.showAlert = true
          return
        }

        this.disabled = true

        const result = (wheight / (height * height))?.toFixed(2) || 0

        this.$emit('setResult', result)
      },
      closeAlert: function() {
        this.showAlert = false
      }
    }
  }
</script>