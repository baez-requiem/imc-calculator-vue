<script>
  import FormVue from './components/Form.vue'
  import InfoVue from './components/Info.vue'

  export default {
    components: {
      FormVue,
      InfoVue
    },
    data() {
      return {
        resultImc: '',
        backTime: 0
      }
    },
    methods: {
      setResult: function(value) {
        this.resultImc = value

        console.log('this.resultImc', this.resultImc)
      },
      back: function() {
        this.resultImc = ''

        this.backTime = new Date().getTime()
      }
    }
  }
</script>

<template>
  <main>
    <div class="container">
      <span class="badge">IMC</span>
      <div class="d-flex d-flex-column-md">
        <FormVue :key="'form-'+backTime" @setResult="setResult" />
        <InfoVue :key="'info-'+resultImc" :resultImc="resultImc" @back="back" />
      </div>
    </div>


  </main>
</template>

<style>
  @media (max-width: 768px) {
    main {
      display: flex;
      flex-direction: column;
    }
  }
  .badge {
    display: inline-block;
    padding: .5rem 1rem;
    background-color: #146ebe;
    color: #fff;
    font-weight: bold;
    border-radius: 5px;
    margin: 1rem 0;
  }
</style>