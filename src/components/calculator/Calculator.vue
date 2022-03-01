<template>
  <div class="calculator">
    <h2>Расчет выхода по стадии таблетирования</h2>

    <form class="form">
      <p class="form-group">
        <label for="A">Загружено смеси для таблетирования A, кг</label>
        <input
          class="A"
          type="number"
          placeholder="указать значение"
          v-model.number="A"
        />
      </p>

      <p class="form-group">
        <label for="B1">Получено таблеток B1, кг</label>
        <input
          class="B1"
          type="number"
          placeholder="указать значение"
          v-model.number="B1"
        />
      </p>

      <p class="form-group">
        <label for="B2">Получено таблеток B2, кг</label>
        <input
          class="B2"
          type="number"
          placeholder="указать значение"
          v-model.number="B2"
        />
      </p>

      <p class="form-group">
        <label for="C">Брак C, кг</label>
        <input
          class="C"
          type="number"
          placeholder="указать значение"
          v-model.number="C"
        />
      </p>

      <p class="form-group">
        <label for="D">Отбор проб D, кг</label>
        <input
          class="D"
          type="number"
          placeholder="указать значение"
          v-model.number="D"
        />
      </p>

      <p class="form-group">
        <label for="F1">Средняя масса таблетки F1, мг</label>
        <input
          class="F1"
          type="number"
          placeholder="указать значение"
          v-model.number="F1"
        />
      </p>

      <p class="form-group">
        <label for="F2">Средняя масса таблетки F2, мг</label>
        <input
          class="F2"
          type="number"
          placeholder="указать значение"
          v-model.number="F2"
        />
      </p>

      <p class="form-group">
        <label for="G1">Стандартное отклонение StdDev G1, мг</label>
        <input
          class="G1"
          type="number"
          placeholder="указать значение"
          v-model.number="G1"
        />
      </p>

      <p class="form-group">
        <label for="G2">Стандартное отклонение StdDev G2, мг</label>
        <input
          class="G2"
          type="number"
          placeholder="указать значение"
          v-model.number="G2"
        />
      </p>
    </form>

    <div class="result">
      <p>Получено таблеток общее B = {{B}} кг</p>
      <p>Потери E = {{E}} кг</p>
      <p>Колличество таблеток после стадии таблетирования K1 = {{K1}} шт</p>
      <p>Колличество таблеток после стадии таблетирования K2 = {{K2}} шт</p>
      <p>Колличество таблеток после стадии таблетирования общее K = {{K}} шт</p>
      <p>Выход = {{sum}} %</p>
      <p>Min масса таблетки H1 = {{H1}} мг</p>
      <p>Min масса таблетки H2 = {{H2}} мг</p>
      <p>Max масса таблетки I1 = {{I1}} мг</p>
      <p>Max масса таблетки I2 = {{I2}} мг</p>
      <p>Колличество таблеток с Min массой Y1 = {{Y1}} шт</p>
      <p>Колличество таблеток с Min массой Y2 = {{Y2}} шт</p>
      <p>Колличество таблеток с Max массой Z1 = {{Z1}} шт</p>
      <p>Колличество таблеток с Max массой Z2 = {{Z2}} шт</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      A: null,
      B1: null,
      B2: null,
      C: null,
      D: null,
      F1: null,
      F2: null,
      G1: null,
      G2: null
    };
  },
  computed: {
    B() {
      return this.B1 + this.B2;
    },
    E() {
      return this.A - (this.B1 + this.B2) - this.D;
    },
    K1() {
      return (this.B1 * 1000000) / this.F1;
    },
    K2() {
      return (this.B1 * 1000000) / this.F2;
    },
    K() {
      return this.K1 + this.K2;
    },
    sum() {
      return (this.B / this.A) * 100;
    },
    H1() {
      return this.F1 - this.G1;
    },
    H2() {
      return this.F2 - this.G2;
    },
    I1() {
      return this.F1 + this.G1;
    },
    I2() {
      return this.F2 + this.G2;
    },
    Y1() {
      return (this.B1 * 1000000) / this.H1;
    },
    Y2() {
      return (this.B2 * 1000000) / this.H2;
    },
    Z1() {
      return (this.B1 * 1000000) / this.I1;
    },
    Z2() {
      return (this.B2 * 1000000) / this.I2;
    },
  },
};
</script>

<style scoped>
h2 {
  color: rgb(255, 255, 255);
  text-align: left;
}
.calculator {
  min-width: 200px;
  max-width: 600px;
  margin: 0 auto;
  /* position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%); */
  padding: 10px;
}
.form {
  text-align: left;
  background-color: rgb(223, 226, 214);
  padding: 10px;
  margin-bottom: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}

.result {
  text-align: left;
  background-color: rgb(223, 226, 214);
  padding: 10px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}
</style>