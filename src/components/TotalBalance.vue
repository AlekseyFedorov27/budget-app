<template>
  <div
    class="total-value"
    :style="{ color: totalBalanceColor }"
  >Balance: {{ totalBalance }}</div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    list: {
      type: Object,
      default: null
    }
  },
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce(
        (acc, item) => acc + this.plusMinus(item.type) * item.value,
        0
      );
    },
    totalBalanceColor() {
      // 3. TotalBalance должен менять цвет текста в зависимости от значения total,
      // если значение больше нуля то цвет  зеленый, если ноль то черный и если
      // меньше нуля то красный.
      // console.log( comp )
      if (this.totalBalance > 0) {
        return "green";
      }
      if (this.totalBalance == 0) {
        return "black";
      }
      return "red";
    }
  },
  methods: {
    // 2. Сейчас есть бага, если мы выберем в форме тип outcome но
    // цифру введем без минуса то это значение приплюсуется с общему балансу,
    //  нужно это исправить.
    plusMinus(type) {
      return type === "INCOME" ? 1 : -1;
    }
  }
};
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
}
</style>