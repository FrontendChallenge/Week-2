<template>
  <div class="ticket-count">
    <button @click.prevent="decrement()" class="ticket-count__decrement">-</button>
    <span class="ticket-count__value">{{ticketCount}}</span>
    <button @click.prevent="increment()" class="ticket-count__increment">+</button>
  </div><!-- /.ticket-count -->
</template>

<script>
export default {
  name: 'app-header',

  props: ['count'],

  data () {
    return {
      ticketCount: this.count
    }
  },

  methods: {
    decrement () {
      if (this.ticketCount > 0) {
        this.ticketCount = this.ticketCount - 1
        this.$emit('change', this.ticketCount)
      }
    },

    increment () {
      this.ticketCount = this.ticketCount + 1
      this.$emit('change', this.ticketCount)
    }
  }
}
</script>

<style lang="scss">
.ticket-count {
  &__decrement,
  &__increment {
    background-color: #fb024e;
    border: none;
    border-radius: 50%;
    color: #fff;
    cursor: pointer;
    font-size: 20px;
    font-weight: 700;
    height: 24px;
    line-height: 24px;
    outline: none;
    vertical-align: middle;
    width: 24px;
  }

  &__value {
    pointer-events: none;
  }
}
</style>
