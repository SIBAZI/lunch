<template>
  <div>
    <v-container>
      <v-row
        class="blue lighten-4"
        justify="center"
        align-content="center"
        v-for="(userFee, index) in userFees"
        :key="index"
      >
        <v-col cols="3">
          <v-text-field label="名前" variant="outlined"></v-text-field>
        </v-col>
        <v-col cols="3">
          <v-text-field
            type="number"
            label="料金"
            variant="outlined"
            @input="change(index)"
            v-model="userFee.price"
          ></v-text-field>
        </v-col>
        <v-col cols="3">
          <v-text-field
            type="number"
            label="預り金"
            variant="outlined"
            @input="change(index)"
            v-model="userFee.deposit"
          ></v-text-field>
        </v-col>
        <v-col cols="3">
          <v-text-field
            type="number"
            label="お釣り"
            variant="outlined"
            :bg-color="userFee.change < 0 ? 'error' : ''"
            v-model="userFee.change"
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row class="blue lighten-4" justify="center" align-content="center">
        <v-col cols="3">
          <v-btn variant="outlined" @click="addUserFee"> 追加 </v-btn>
        </v-col>
        <v-col cols="3">合計:{{ totalPrice }}</v-col>
        <v-col cols="3">合計:{{ totalDeposit }}</v-col>
        <v-col cols="3">合計:{{ totalChange }}</v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userFees: [{ name: "", price: "", deposit: "", change: "" }],
    };
  },
  computed: {
    totalPrice() {
      return this.userFees
        .map((userFee) => userFee.price)
        .reduce((a, b) => {
          return Number(a) + Number(b);
        });
    },

    totalDeposit() {
      return this.userFees
        .map((userFee) => userFee.deposit)
        .reduce((a, b) => {
          return Number(a) + Number(b);
        });
    },

    totalChange() {
      return this.userFees
        .map((userFee) => userFee.change)
        .reduce((a, b) => {
          return Number(a) + Number(b);
        });
    },
  },
  methods: {
    addUserFee() {
      this.userFees.push({ name: "", price: "", deposit: "", change: "" });
    },
    /**
     *
     * @param {Number} index userFeesのindex
     */
    change(index) {
      this.userFees[index]["change"] =
        this.userFees[index]["deposit"] - this.userFees[index]["price"];
    },
  },
};
</script>

<style>
.greeting {
  color: red;
  font-weight: bold;
}
</style>
