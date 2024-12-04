<template>
    <div class="container">
      <h1 class="mt-4 text-center">Invoices</h1>
      <form>
        <div class="form-group">
          <label for="score">Invoice number</label>
          <input
            type="number"
            placeholder="Ex: 53453"
            v-model="score"
            class="form-control"
          />
        </div>
        <br>
        <div class="form-group">
          <label for="amount">Total amount</label>
          <input
            type="number"
            placeholder="Ex: 53453"
            v-model="amount"
            class="form-control"
          />
        </div>
        <br>
        <div class="form-group">
            <label for="selected">Select a client</label>
            <select v-model="selected">
                <option>Client1</option>
                <option>Client2</option>
                <option>Client3</option>
            </select>
        </div>
        <br>
        <div class="form-group">
          <label for="items">Items</label><br>
          <input
            type="text"
            placeholder="Item Name"
            v-model="itemName"
            class="form-control"
          />
          <input
            type="number"
            placeholder="Quantity"
            v-model="itemQuan"
            class="form-control"
          />
          <input
            type="number"
            placeholder="Ammount"
            v-model="itemAmm"
            class="form-control"
          />
        </div>
        <br>
        <div>
            <datepicker v-model="date" :format=" 'yyyy-MM-dd'" />
        </div>
        <button type="button" @click="onSubmit" class="btn btn-dark">
          Submit
        </button>
      </form>
      <table class="table mt-5">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Invoice number</th>
            <th scope="col">Amount</th>
            <th scope="col">Client</th>
            <th scope="col">Due date</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(entry, i) in sortedList" :key="i">
            <th scope="row">{{ ++i }}</th>
            <td>{{ entry.score }}</td>
            <td>{{ entry.amount }}</td>
            <td>{{ entry.selected }}</td>
            <button @click="deleteTask(i)">Delete</button>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  //import { Datetime } from 'vue-datetime';
  export default {
    name: "Leaderboard",
    data: () => ({ score: "", allScores: [], amount: "", 
    options: [{ id: 1, text: 'Client 1' },
              { id: 2, text: 'Client 2' },
              { id: 3, text: 'Client 3' }], sortedList: [] }),
    computed: {
      sortedList: function() {
        return this.allScores.slice().sort(function(a, b) {
          return b.score - a.score;
        });
      },
    },
    methods: {
      onSubmit() {
        this.allScores.push({ score: this.score, amount: this.amount, selected: this.selected });
        this.clearForm();
      },
      clearForm() {
        this.name = "";
        this.score = "";
        this.amount = "";
      },
      deleteTask (index) {
        this.sortedList.splice(index, 1);
      }
    },
    
    
    

  };
  </script>