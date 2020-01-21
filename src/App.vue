<template>
  <div id="app">

    <DialogConfirm
      :dialogVis="dialogVis"
      @closeDialog="showDialog"
      @deleteItem="deleteIt"
    />
    <!-- <el-button type="text" @click="showDialog" >click to open the Dialog</el-button> -->

    <Form @submitForm="onFormSubmit" />
    <TotalBalance :list="list" />
    <BudgetList
      :list="list"
      @deleteItem="onDeleteItem"
    />

  </div>
</template>

<script>
import BudgetList from "@/components/BudgetList";
import TotalBalance from "@/components/TotalBalance";
import Form from "@/components/Form";
import DialogConfirm from "@/components/DialogConfirm";

export default {
  name: "app",
  components: {
    BudgetList,
    TotalBalance,
    Form,
    DialogConfirm
  },
  data: () => ({
    list: {
      1: {
        type: "INCOME",
        value: 100,
        comment: "Some comment",
        id: 1
      },
      2: {
        type: "OUTCOME",
        value: 50,
        comment: "Some outcome comment",
        id: 2
      }
    },
    dialogVis: { type: false, listItemDel: Number }
  }),
  computed: {},
  methods: {
    onDeleteItem(id) {
      this.showDialog();
      this.dialogVis.listItemDel = this.list[id];
    },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      this.$set(this.list, newObj.id, newObj);
    },
    showDialog() {
      this.dialogVis.type = !this.dialogVis.type;
    },
    deleteIt(id) {
      // console.log('delete', id)
      this.$delete(this.list, id.id);
      this.showDialog();
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
