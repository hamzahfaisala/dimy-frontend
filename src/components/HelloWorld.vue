<template>
  <br><br>
  <div class="mx-5">
    <v-btn class="mr-16 mt-2" color="green" size="x-large" @click="addData()">
      <Icon class="text--white" icon="mdi:plus" style="font-size: 36px;"/>
    </v-btn>
    <br><br><br>
    <v-row v-for="(data, index) in datas" :key="index">
      <v-col cols="3">
        <v-text-field
          variant="solo"
          class="mr-16 mt-2"
          label="Product Name"
          v-model="data.productName"
        >
        </v-text-field>
      </v-col>
      <v-col cols="3">
        <v-text-field
          variant="solo"
          class="mr-16 mt-2"
          label="Product Price"
          v-model="data.productPrice"
          type="number"
          @input="calculateTotal(index)"
        >
        </v-text-field>
      </v-col>
      <v-col cols="2">
        <v-text-field
          variant="solo"
          class="mr-16 mt-2"
          label="Quantity"
          v-model="data.quantity"
          type="number"
          @input="calculateTotal(index)"
        >
        </v-text-field>
      </v-col>
      <v-col cols="3">
        <v-text-field
          variant="solo"
          class="mr-16 mt-2"
          label="Total"
          readonly
          v-model="data.total"
        >
        </v-text-field>
      </v-col>
      <v-col cols="1">
        <v-btn class="mr-16 mt-2" color="red" size="x-large" @click="deleteData(index)">
          <Icon class="text--white" icon="mdi:delete" style="font-size: 36px;"/>
        </v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="8"></v-col>
      <v-col cols="3">
        <v-text-field
          variant="solo"
          class="mr-16 mt-2"
          label="Grand Total"
          v-model="grandTotal"
          readonly
        >
        </v-text-field>
      </v-col>
    </v-row>

  </div>
</template>
<script>
  import { Icon } from '@iconify/vue';
  export default {
    components: {
      Icon
    },
    data() {
      return {
        grandTotal : 0,
        datas: [
          {
            productName: '',
            productPrice: '',
            quantity: 1,
            total: '',
          }
        ]
      }
    },
    methods: {
      addData(){
        const newData = {
          productName: '',
          productPrice: '',
          quantity: 1,
          total: '',
        }
        this.datas.push(newData)
        this.calculateGrandTotal()
      },
      deleteData(index){
        this.datas.splice(index, 1);
        this.calculateGrandTotal()
      },
      calculateTotal(index){
        if(this.datas[index].quantity < 1){
          this.datas[index].quantity = 1
          alert("quantity tidak bisa kurang dari 1")
        }
        this.datas[index].total = this.datas[index].productPrice * this.datas[index].quantity 
        this.calculateGrandTotal()
      },
      calculateGrandTotal(){
        this.grandTotal = 0
        for (let i = 0; i < this.datas.length; i++) {
          this.grandTotal = this.grandTotal + this.datas[i].total
        }
      }
    },
  };
</script>

<script setup>
  
</script>
