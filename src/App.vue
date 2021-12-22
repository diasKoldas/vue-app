<template>
  <div class="container">
    <div class="sidebar">
      <div v-if="filters.length">
        <div v-for="(filter, idx) in filters || []" v-bind:key="idx">
          <Filter
              ref="filterComponent"
              :title="filter.title"
              :options="filter.options"
              @select="setOptions"
          />
          <div class="delimiter"/>
        </div>
        <button class="btn" @click="clearOptions">Сбросить все фильтры</button>
        <div class="delimiter"/>
      </div>
    </div>
    <div class="delimiter"/>
    <div class="content">
      <div v-if="tickets.length">
        <div v-for="(ticket, idx) in filteredTickets" v-bind:key="idx">
          <Ticket
              :price="ticket.price"
              :companyName="ticket?.itineraries[0][0].carrier_name"
              :logoURL="`https://aviata.kz/static/airline-logos/80x80/${ticket.validating_carrier}.png`"
          />
          <div class="delimiter"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {Ticket, Filter} from './components';
import {airlines, flights} from '../data.json';

export default {
  name: 'App',
  components: {
    Ticket,
    Filter
  },
  data: () => ({
    selectedOptions: [],
    filters: [],
    tickets: [],
  }),
  methods: {
    setOptions(options) {
      this.selectedOptions = options;
    },
    clearOptions() {
      this.selectedOptions = [];
      this.$refs.filterComponent[0].clearAll()
    }
  },
  computed: {
    filteredTickets () {
      if (this.selectedOptions.length === 0) {
        return this.tickets;
      }
      return this.tickets?.filter(item => {
        return this.selectedOptions.map(option => {
          return option;
        }).indexOf(item.validating_carrier) >= 0
      });
    }
  },
  async mounted() {
    setTimeout(() => {
      this.filters = [{title: 'Авиакомпании', options: airlines}]
      this.tickets = [...flights]
    }, 1000)
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;0,800;1,300;1,400;1,500;1,600;1,700;1,800&family=Roboto:wght@100;300;400;500;700;900&display=swap');
body {
  font-family: 'Open Sans', sans-serif;
  background: #D7D7D7;
  margin: 0;
}
.delimiter {
  flex: 0 0 12px; width: 12px; height: 12px;
}
.container {
  display: flex;
  flex-direction: row;
  max-width: 1170px;
  padding: 50px 15px;
  margin: auto;
  box-sizing: border-box;
}
.sidebar {
  flex: 0 0 240px;
}
.content {
  flex: 0 1 100%;
}
.btn {
  background: transparent;
  font-family: 'Open Sans', sans-serif;
  font-size: 12px;
  line-height: 16px;
  color: #7284E4;
  border: none;
  border-bottom: 1px dashed #7284E4;
  padding: 0;
  cursor: pointer;
}
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
}
@media (max-width: 425px) {
  .container {
    padding: 15px;
  }
}
</style>
