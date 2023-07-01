<template>
  <div class="p-4" style="max-width: 400px; margin: 50px auto; background: #313131; border-radius: 25px; border: 3px solid #E4A11B;">

    <div class="w-full rounded m-2 p-4 text-right lead font-weight-bold text-white bg-dark" style="font-size: 30px; line-height: 10px; overflow: hidden;">
      {{ calcVal || 0 }}
    </div>

    <div class="w-full text-right font-weight-bold text-xs mt-2" style="position: relative; left: 212px; top: 352px; font-family: monospace; font-size: 40px; display: inline-block; color: #E4A11B;">
      {{ name }}
    </div>

    <div class="row no-gutters">
      <div class="col-3" v-for="n in calcObjects" :key="n">
        <div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          @click="action(n)"
        >
          {{n}}
        </div>
      </div>
    </div>

    <!-- "Back" gomb -->
    <div
      class="back-button"
      @click="goBack"
      style="
        position: fixed;
        right: 20px;
        bottom: 20px;
        font-family: monospace;
        font-size: 14px;
        padding: 10px;
        background-color: #313131;
        border-radius: 5px;
        color: white;
        cursor: pointer;
        text-decoration: underline;
      "
    >
      Back
    </div>

  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'calc',
  props: {
    msg: String
  },
  data() {
    return {
      calcVal: '',
      calcObjects: ['C', '*', '/', '-', '7', '8', '9', '+', '4', '5', '6', '%', '1', '2', '3', '=', '0', '.'],
      operator: null,
      beforeCalcVal: '',
      name: 'saekq'
    }
  },
  computed: {
    result() {
      return this.calcVal || 0;
    }
  },
  methods: {
    action(n) {
      switch (n) {
        case 'C':
          this.calcVal = '';
          break;
        case '%':
          this.calcVal = Number(this.calcVal) / 100 + '';
          break;
        case '/':
        case '*':
        case '-':
        case '+':
          this.operator = n;
          this.beforeCalcVal = this.calcVal;
          this.calcVal = '';
          break;
        case '=':
          this.calcVal = eval(this.beforeCalcVal + this.operator + this.calcVal);
          this.beforeCalcVal = '';
          this.operator = null;
          break;
        default:
          if (!isNaN(n) || n === '.') {
            if (this.calcVal.length < 19) {
              this.calcVal += n + '';
            }
          }
          break;
      }
    },
    goBack() {
      window.history.back();
    }
  }
}
</script>

<style scoped>
  .bg-vue-dark {
    background: #363636;
    box-shadow: 0px 5px #2c2c2c;
  }
  .hover-class:hover {
    cursor: pointer;
    background-color: #E4A11B;
    box-shadow: 0px 5px #ca8e16;
  }
</style>
