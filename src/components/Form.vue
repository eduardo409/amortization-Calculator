<template>
  <div class="form">
    <v-form>
      <v-container>
        <v-row>
          <v-col
            v-for="(entry,index) in entries"
            v-bind:key="index"
            cols="12"
            lg="12"
            sm="12"
            md="12"
          >
            <v-text-field
              v-bind:label="entry.rep"
              v-model="entry.value"
              outlined
              type="number"
              pattern="[0-9]*"
              inputmode="numeric"
              hide-details
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" lg="12" sm="12" md="12">
            <v-btn
              block
              class="indigo lighten-1 white--text text-center"
              v-on:click="submitForm()"
              :loading="loading"
            >Calculate</v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-form>
  </div>
</template>

<script>
export default {
  name: "Form",
  props: {
    entries: Object
  },
  data: () => ({
    // entries:{bal:{rep:"Balance",value:8500}, apr:{rep:"APR",value:12.74}, monthPayment:{rep:"Monthly Payment",value:1200}},
    tableData: null,
    loading: false
  }),
  methods: {
    wait(ms) {
      var start = new Date().getTime();
      var end = start;
      while (end < start + ms) {
        end = new Date().getTime();
      }
    },
    submitForm() {
      this.$parent.updateComponents(
        this.entries.bal.value,
        this.entries.apr.value,
        this.entries.monthPayment.value
      );
    }
  }
};
</script>
<style >
.loading {
  background: red;
}
.form {
  background: white;
}
</style>
