<template>
  <div class="ticket-store-page">
    <div class="ticket-store-page__inner">
      <app-header></app-header>

      <div class="show">
        <div class="show__meta show-meta">

          <div class="show__time show-meta__item">
            <div class="show-meta__label">Vrijeme</div><!-- /.show-meta__label -->
            <div class="show-meta__value">
              {{currentTime | date('%H:%M') }}
              <div class="show-meta__value--subtitle">
                {{currentTime | date('%d. %B %Y')}}
              </div>
            </div><!-- /.show-meta__value -->
          </div><!-- /.show__time.show-meta__item -->

          <div class="show__location show-meta__item">
            <div class="show-meta__label">Dvorana</div><!-- /.show-meta__label -->
            <div class="show-meta__value">11</div><!-- /.show-meta__value -->
          </div><!-- /.show__time.show-meta__item -->

          <div class="show__ticket-type show-meta__item">
            <div class="show-meta__label">Tip karte</div><!-- /.show-meta__label -->
            <div class="show-meta__value">Regular</div><!-- /.show-meta__value -->
          </div><!-- /.show__time.show-meta__item -->

          <div class="show__price show-meta__item">
            <div class="show-meta__label">Cijena</div><!-- /.show-meta__label -->
            <div class="show-meta__value">{{totalPrice | round(2)}} kn</div><!-- /.show-meta__value -->
          </div><!-- /.show__time.show-meta__item -->

          <div class="show__time show-meta__item">
            <div class="show-meta__label">Ulaznice</div><!-- /.show-meta__label -->
            <div class="show-meta__value">
              <ticket-count :count="ticketCount" v-on:change="updatePrice"></ticket-count>
            </div><!-- /.show-meta__value -->
          </div><!-- /.show__time.show-meta__item -->

        </div><!-- /.show__meta -->

        <div class="show__heading">
          <h1 class="show__title">Interstellar</h1><!-- /.show__title -->

          <div class="show__purchase-type">
            <button class="show__purchase-button show__purchase-button--selected">Kupnja</button>
            <button class="show__purchase-button">Rezervacija</button>
          </div><!-- /.show__purchase-type -->
        </div><!-- /.show__heading -->

        <div class="show__subheading">Trajanje 2:15 <strong>Christofer Nolan</strong></div><!-- /.show__subheading -->

        <div class="show__blank-space"></div><!-- /.show__blank-space -->

        <div class="show__seat-selector">
          <seat-selector></seat-selector>
        </div><!-- /.show__seat-selector -->

        <div class="show__summary show-meta">
          <div class="show__location show-meta__item">
            <div class="show-meta__label">Red</div><!-- /.show-meta__label -->
            <div class="show-meta__value">N</div><!-- /.show-meta__value -->
          </div><!-- /.show__time.show-meta__item -->

          <div class="show__location show-meta__item">
            <div class="show-meta__label">Sjedalo</div><!-- /.show-meta__label -->
            <div class="show-meta__value">9-10</div><!-- /.show-meta__value -->
          </div><!-- /.show__time.show-meta__item -->

          <button class="show__submit-button show__submit-button--enabled"></button>
        </div><!-- /.show__summary -->

        <div class="show__footer">
          <div class="show__reserve-time">
            <span class="time">60<span class="time__unit">min</span></span>
          </div><!-- /.show__reserve-time -->

          <div class="show__footnotes">
            <div class="show__footnote show__footnote--time">Rezervirati se može najkasnije 60 minuta prije predstave.</div><!-- /.show__footnote -->

            <div class="show__footnote show__footnote--system">Ukoliko sustav ne dozvoljava rezervaciju, znači da je postotak već iskorišten ili već imate 2 otvorene rezervacije.<br/>Rezervacije za VIP i LoveBox sjedala nisu moguća, već samo kupovina.
            </div><!-- /.show__footnote -->
          </div><!-- /.show__footnotes -->
        </div><!-- /.show__footer -->
      </div><!-- /.show -->
    </div><!-- /.ticket-store-page__inner -->
  </div><!-- /.ticket-store-page -->
</template>

<script>
import AppHeader from '../components/header.vue'
import TicketCount from '../components/ticket-count.vue'
import SeatSelector from '../components/seat-selector.vue'

export default {
  name: 'ticket-store',

  data () {
    return {
      currentTime: null,
      ticketCount: 2
    }
  },

  created () {
    this.currentTime = new Date()
  },

  methods: {
    updatePrice (ticketCount) {
      this.ticketCount = ticketCount
    }
  },

  computed: {
    totalPrice () {
      return this.ticketCount * 20
    }
  },

  components: {
    AppHeader, TicketCount, SeatSelector
  }
}
</script>

<style lang="scss">
.ticket-store-page {
  background: transparent url(/static/images/movie-background.jpg) center center no-repeat;
  background-size: 102% auto;
  min-height: 100%;

  &__inner {
    /* Permalink - use to edit and share this gradient: http://colorzilla.com/gradient-editor/#000000+0,000000+30,000000+100 */
    background: #000000; /* Old browsers */
    background: -moz-linear-gradient(top,  rgba(0,0,0,0) 0%, rgba(0,0,0,0) 30%, rgba(0,0,0,1) 100%); /* FF3.6-15 */
    background: -webkit-linear-gradient(top,  rgba(0,0,0,0) 0%,rgba(0,0,0,0) 30%,rgba(0,0,0,1) 100%); /* Chrome10-25,Safari5.1-6 */
    background: linear-gradient(to bottom,  rgba(0,0,0,0) 0%,rgba(0,0,0,0) 30%,rgba(0,0,0,1) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
    filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='rgba(0,0,0,0)', endColorstr='rgba(0,0,0,0)',GradientType=0 ); /* IE6-9 */

    padding-left: 60px;

  }

  .show {
    padding-top: 110px;

    &__meta {
      border-bottom: 2px solid rgba(255,255,255,0.2);
      padding-bottom: 25px;
    }

    &__heading {
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      padding-right: 60px;
      padding-top: 80px;
      vertical-align: middle;
    }

    &__subheading {
      color: rgba(255,255,255,0.6);
      margin-top: 40px;
    }

    &__title {
      display: flex;
      align-self: flex-start;
      font-size: 72px;
      font-weight: 900;
      line-height: 72px;
    }

    &__purchase-type {
      align-self: flex-end;
      display: flex;
      width: 360px;
    }

    &__purchase-button {
      background-color: transparent;
      border: 1px solid rgba(255,255,255,0.2);
      color: #fff;
      font-size: 16px;
      font-weight: 700;
      height: 48px;
      outline: none;
      text-transform: uppercase;
      width: 50%;

      &:first-child {
        border-right: none;
        border-top-left-radius: 24px;
        border-bottom-left-radius: 24px;
      }

      &:last-child {
        border-left: none;
        border-top-right-radius: 24px;
        border-bottom-right-radius: 24px;
      }

      &--selected {
        background-color: #fb024e;
      }
    }

    &__blank-space {
      height: 640px;
    }

    &__seat-selector {
      padding-right: 60px;
    }

    &__summary {
      height: 180px;
      margin: 0 auto;
      padding: 25px 0px;
      padding-right: 60px;
      width: 1080px;
    }

    &__submit-button {
      background: url(/static/images/checkmark-icon.svg) center center no-repeat;
      background-color: transparent;
      background-size: 72px 72px;
      border: 1px solid rgba(255,255,255,0.3);
      border-radius: 50%;
      box-sizing: border-box;
      cursor: pointer;
      height: 128px;
      left: 50%;
      margin-left: -64px;
      outline: none;
      position: absolute;
      width: 128px;
      text-align: center;
      transition: all .25s;

      &:after {
        border-radius: 50%;
        bottom: 8px;
        content: '';
        display: block;
        left: 8px;
        position: absolute;
        right: 8px;
        top: 8px;
        transition: all .25s;
      }

      &--enabled {
        background: url(/static/images/checkmark-icon--selected.svg) center center no-repeat;
        background-size: 72px 72px;
        border: 1px solid #fb024e;

        &:after {
          border: 1px solid rgba(251, 2, 78, 0.3);
        }
      }
    }

    &__footer {
      margin: 0 auto;
      padding-right: 60px;
      width: 1080px;
    }

    &__reserve-time {
      .time {
        color: #fb024e;
        font-size: 36px;
        font-weight: 900;

        &__unit {
          font-size: 14px;
        }
      }
    }

    &__footnotes {
      display: flex;
      flex-direction: row;
      flex: 1 0 100%;
      padding-bottom: 40px;
    }

    &__footnote {
      color: rgba(255,255,255,0.6);
      font-size: 12px;
      display: flex;
      flex-direction: column;
      padding: 16px 0;

      &--time {
        width: 160px;
        margin-right: 60px;
      }
    }
  }

  .show-meta {
    display: flex;
    flex-direction: row;

    &__item {
      display: flex;
      flex-direction: column;
      margin-right: 40px;
    }

    &__label {
      color: rgba(255,255,255, 0.6);
      font-size: 12px;
      font-weight: 700;
      letter-spacing: 3px;
      margin-bottom: 16px;
      text-transform: uppercase;
    }

    &__value {
      font-size: 36px;
      font-weight: 900;

      &--subtitle {
        color: rgba(255,255,255, 0.6);
        font-size: 16px;
        font-weight: 400;
      }
    }
  }
}
</style>
