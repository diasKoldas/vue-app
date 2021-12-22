<template>
  <div class="ticketWrapper">
    <div class="left">
      <div class="leftTop">
        <div class="logo">
          <img :src="logoURL" alt="">
          <span>{{ companyName }}</span>
        </div>
        <div class="from">
          <div>25 ноя, вс</div>
          <div>23:25</div>
        </div>
        <div class="time">
          <div class="top">
            <span>ALA</span>
            <span>4 ч 20 м</span>
            <span>TSE</span>
          </div>
          <div class="center">
            <div></div>
            <div></div>
            <div></div>
          </div>
          <div class="bottom">через Шымкент, 1 ч 50 м</div>
        </div>
        <div class="to">
          <div>26 ноя, сб <span>+1</span></div>
          <div>03:45</div>
        </div>
      </div>
      <div class="leftBottom">
        <button class="btn">Детали перелета</button>
        <button class="btn">Условия тарифа</button>
        <div class="status">
          <img :src="status" alt="">
          <span>невозвратный</span>
        </div>
      </div>
    </div>
    <div class="right">
      <div class="price">{{ price }} ₸</div>
      <button class="selectedBtn">Выбрать</button>
      <small>Цена за всех пассажиров</small>
      <div class="baggage">
        <span>Нет багажа</span>
        <button>+ Добавить багаж</button>
      </div>
    </div>
  </div>
</template>

<script>
import status from '../../assets/status-icon.png'
export default {
  name: 'Ticket',
  props: {
    price: String,
    companyName: String,
    logoURL: String,
  },
  data() {
    return {
      status
    }
  }
}
</script>

<style scoped>
@import "./Ticket.module.css";
</style>