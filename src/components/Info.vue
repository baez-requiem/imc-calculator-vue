<template>
  <section class="w-full-md py-5-md">
    <div class="row mb-20">
      <div class="card bg-gray">
        <div class="icon-content">
          <i class="fa-solid fa-thumbs-up invert-icon"></i>
        </div>
        <h3>Magreza</h3>
        <p>IMC está entre 0 e 18.5</p>
      </div>
      <div class="card bg-green">
        <div class="icon-content">
          <i class="fa-solid fa-thumbs-up"></i>
        </div>
        <h3>Normal</h3>
        <p>IMC está entre 18.6 e 24.9</p>
      </div>
    </div>
    <div class="row">
      <div class="card bg-yellow">
        <div class="icon-content">
          <i class="fa-solid fa-thumbs-up invert-icon"></i>
        </div>
        <h3>Sobrepeso</h3>
        <p>IMC está entre 25 e 30</p>
      </div>
      <div class="card bg-red">
        <div class="icon-content">
          <i class="fa-solid fa-thumbs-up invert-icon"></i>
        </div>
        <h3>Obesidade</h3>
        <p>IMC está entre 30.1 e 60</p>
      </div>
    </div>

    <div
      class="result-container"
      :class="infos?.bgClass, {'show-container': !!result}"
    >
      <div>
        <div class="icon-content">
          <i :class="infos.iconClass"></i>
        </div>
 
        <h3>{{infos.name}}</h3>
 
        <p>Seu IMC é {{ result }} kg/m²</p>
      </div>

      <p>IMC está entre {{infos.imcBetween}}</p>

      <button class="btn-back" @click="$emit('back')">
        <i class="fa-solid fa-arrow-left"></i>
      </button>
    </div>
  </section>
</template>

<style scoped>
  section {
    display: flex;
    flex-direction: column;
    position: relative;

    padding-right: 1.5rem;
    padding-left: 1.5rem;
  }

  .row {
    width: 100%;
    display: flex;
    gap: 20px;
    justify-content: center;
  }
  
  .mb-20 {
    margin-bottom: 20px;
  }

  .card {
    display: flex;
    justify-content: space-evenly;
    flex-direction: column;
    align-items: center;

    width: 190px;
    height: 190px;

    color: #fff;
    border-radius: 10px;
  }

  .card p, .result-container p {
    font-size: 0.9rem;
    text-align: center;
  }

  .icon-content {
    border-radius: 50%;
    height: 60px;
    width: 60px;
    
    display: flex;
    align-items: center;
    justify-content: center;

    font-size: 2rem;
    background-color: #0009;
  }

  .icon-content .invert-icon {
    transform: scaleY(-1) scaleX(-1);
  }

  .btn-back {
    position: absolute;
    left: -25px;

    height: 50px;
    width: 50px;
    
    border: 2px solid #f5f5f5;
    border-radius: 50%;

    background-color: #0d6efd;
    color: #fff;

    transition: all .2s;
    cursor: pointer;
  }

  .btn-back:hover {
    background-color: #084298;
  }

  @keyframes showAnim {
    from {
      opacity: 0;
    }

    to {
      opacity: 1;
    }
  }

  .result-container {
    visibility: hidden;

    position: absolute;
    color: #fff;

    display: flex;
    justify-content: space-evenly;
    flex-direction: column;
    align-items: center;

    height: 100%;
    width: calc(100% - 3rem);

    border-radius: 10px;
  }

  .result-container :first-child {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 10px;
  }
  .result-container :first-child p {
    font-size: 1rem;
  }
  
  .show-container {
    visibility: visible;
    animation: showAnim .5s forwards;
  }

  @media (max-width: 768px) {
    section {
      padding-left: 0;
      padding-right: 0;
    }
    .btn-back {
      left: unset;
      top: -25px;
      transform: rotate(90deg);
    }

    .row {
      gap: 0;
    }
    
    .mb-20 {
      margin-bottom: 0;
    }

    .card {
      border-radius: 0;
      width: 100%;
    }

    .result-container {
      width: 100%;
      height: 100%;
    }
  }
</style>


<script>
  const infos = {
    magreza: {
      iconClass: "fa-solid fa-thumbs-up invert-icon",
      bgClass: "bg-gray",
      name: "Magreza",
      imcBetween: "0 e 18.5"
    },
    normal: {
      iconClass: "fa-solid fa-thumbs-up",
      bgClass: "bg-green",
      name: "Normal",
      imcBetween: "18.6 e 24.9"
    },
    sobrepeso: {
      iconClass: "fa-solid fa-thumbs-up invert-icon",
      bgClass: "bg-yellow",
      name: "Sobrepeso",
      imcBetween: "25 e 30"
    },
    obesidade: {
      iconClass: "fa-solid fa-thumbs-up invert-icon",
      bgClass: "bg-red",
      name: "Obesidade",
      imcBetween: "30.1 e 60"
    },
  }

  export default {
    name: 'Info',
    props: {
      resultImc: String,
      back: { type: Function }
    },
    data() {
      return {
        result: this.resultImc,
        goBack: this.back,
        infos: {}
      }
    },
    created: function() {
      let type = ''

      const result = parseFloat(this.result)

      if (result < 18.5) {
        type = 'magreza'
      } else if (result >= 18.5 && result < 25) {
        type = 'normal'
      } else if (result >= 25 && result < 30) {
        type = 'sobrepeso'
      } else {
        type = 'obesidade'
      }

      this.infos = infos[type]
    }
  }
</script>