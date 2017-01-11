<template>
  <div class="seat-selector">
    <div class="seat-row" v-for="(seatRow, rowIndex) in seats" v-bind:class="{'seat-row--selected': (selected.row === rowIndex)}">
      <span class="seat-row__name">{{seatRow.name}}</span>

      <span class="seat" v-for="(seat, seatIndex) in seatRow.seats" v-bind:class="{'seat--double': (seat === 2), 'seat--empty': (seat === 0), 'seat--selected': isSeatSelected(rowIndex, seatIndex), 'seat--reserved': isSeatReserved(seatRow, seatIndex)}" @click="selectSeat(rowIndex, seatIndex)"></span>
    </div><!-- /.seat-row -->
  </div><!-- /.seat-selector -->

  {{selected}}
</template>

<script>
const seats = [
  {name: 'A', seats: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]},
  {},
  {name: 'B', seats: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]},
  {name: 'C', seats: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]},
  {name: 'D', seats: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]},
  {name: 'E', seats: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]},
  {name: 'F', seats: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]},
  {name: 'G', seats: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]},
  {},
  {name: 'H', seats: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]},
  {name: 'I', seats: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]},
  {name: 'J', seats: [1, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1]},
  {name: 'K', seats: [1, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1]},
  {name: 'L', seats: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]},
  {name: 'M', seats: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]},
  {name: 'N', seats: [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]},
  {name: 'O', seats: [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]}
]

export default {
  name: 'seat-selector',

  data () {
    return {
      seats: seats.reverse(),
      selected: { row: 1, seat: 4 },
      reservedSeats: [
        {row: 'C', seat: 12},
        {row: 'C', seat: 13},
        {row: 'C', seat: 14},
        {row: 'C', seat: 15},
        {row: 'C', seat: 16},
        {row: 'C', seat: 17},
        {row: 'C', seat: 18},
        {row: 'C', seat: 19},
        {row: 'C', seat: 20},
        {row: 'C', seat: 21},
        {row: 'C', seat: 22},
        {row: 'C', seat: 23},
        {row: 'D', seat: 10},
        {row: 'D', seat: 11},
        {row: 'D', seat: 12},
        {row: 'D', seat: 23},
        {row: 'D', seat: 24},
        {row: 'D', seat: 25},
        {row: 'E', seat: 8},
        {row: 'E', seat: 9},
        {row: 'E', seat: 10},
        {row: 'E', seat: 11},
        {row: 'E', seat: 24},
        {row: 'E', seat: 25},
        {row: 'E', seat: 26},
        {row: 'E', seat: 27},
        {row: 'N', seat: 7},
        {row: 'N', seat: 8},
        {row: 'N', seat: 9},
        {row: 'N', seat: 10},
        {row: 'M', seat: 5},
        {row: 'M', seat: 6},
        {row: 'M', seat: 7},
        {row: 'M', seat: 8},
        {row: 'M', seat: 19},
        {row: 'M', seat: 20},
        {row: 'M', seat: 21},
        {row: 'M', seat: 22},
        {row: 'O', seat: 0},
        {row: 'O', seat: 1},
        {row: 'O', seat: 2},
        {row: 'O', seat: 3},
        {row: 'O', seat: 4},
        {row: 'O', seat: 5},
        {row: 'O', seat: 6},
        {row: 'O', seat: 7},
        {row: 'O', seat: 8},
        {row: 'O', seat: 9},
        {row: 'O', seat: 10},
        {row: 'O', seat: 11},
        {row: 'O', seat: 12},
        {row: 'O', seat: 13},
        {row: 'O', seat: 14},
        {row: 'O', seat: 15},
        {row: 'O', seat: 16},
        {row: 'O', seat: 17}
      ]
    }
  },

  methods: {
    isSeatSelected (rowIndex, seatIndex) {
      if (this.selected.row !== null && this.selected.seat !== null) {
        if (this.selected.row === rowIndex && this.selected.seat === seatIndex) {
          return true
        }
      }
      return false
    },

    isSeatReserved (seatRow, seatIndex) {
      let reservedSeat = this.reservedSeats.filter(function (seat) {
        return (seat.row === seatRow.name && seat.seat === seatIndex)
      })

      if (reservedSeat && reservedSeat.length) return true
      return false
    },

    selectSeat (rowIndex, seatIndex) {
      let seatRow = this.seats[rowIndex]
      if (this.isSeatReserved(seatRow, seatIndex)) return false

      this.selected.row = rowIndex
      this.selected.seat = seatIndex
    }
  }
}
</script>

<style lang="scss">
  .seat-selector {
    margin: 0 auto;
    padding-bottom: 40px;
    position: relative;
    width: 1080px;
  }

  .seat-row {
    height: 30px;

    &__name {
      border: 1px solid transparent;
      border-radius: 50%;
      color: rgba(255,255,255,0.5);
      display: inline-block;
      font-size: 12px;
      font-weight: 900;
      line-height: 25px;
      height: 25px;
      margin-right: 10px;
      position: absolute;
      right: 100%;
      text-align: center;
      width: 25px;
    }

    &--selected {
      .seat-row__name {
        border: 1px solid #fb024e;
        color: #fb024e;
      }
    }
  }

  .seat {
    background-color: rgba(255,255,255,0.4);
    border-top-left-radius: 8px;
    border-top-right-radius: 8px;
    box-sizing: border-box;
    cursor: pointer;
    display: inline-block;
    height: 25px;
    margin-right: 5px;
    transition: all .25s;
    width: 25px;

    &--double {
      width: 55px;
    }

    &--selected {
      background-color: #fb024e;
      box-shadow: 0 0 5px #fb024e;
    }

    &--reserved {
      background-color: rgba(255,255,255,0.15);
    }

    &--empty {
      background-color: transparent;
      box-shadow: none;
    }
  }
</style>
