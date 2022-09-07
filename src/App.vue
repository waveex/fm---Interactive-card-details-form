<script setup>
  import Datepicker from '@vuepic/vue-datepicker';
    import '@vuepic/vue-datepicker/dist/main.css'
    import { createApp } from 'vue'

    createApp({

        data() {
            return {
                cardNumber: '',
                details: '',
                dateMonth: '',
                dateYear: '',
                cvc: ''

            }

        },
        components: { Datepicker },
        computed: {
            formatCardNumber() {
                return this.cardNumber ? this.cardNumber.match(/.{1,4}/g).join(' ') : '';
            }
        },
        methods: {
            updateValue(e) {
                this.cardNumber = e.target.value.replace(/ /g, '');
            },
            isNumber(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
                    evt.preventDefault();
                } else {
                    return true;
                }

            }
        }
    })
</script>

<template>

<body>
  <main id="app">
      <aside class="cards">
          <div class="card card--front">
              <span class="card__dot card__ot--bigger"></span>
              <span class="card__dot card__dot--small"></span>
              <p class="card__number">
                  {{ cardNumber }}
              </p>
              <p class="card__onwer">
                  {{ details }}
              </p>
              <p class="date">
                  <span class="date__month">{{dateMonth}}</span> /
                  <span class="date__year"> {{dateYear}} </span>
              </p>
          </div>
          <div class="card card--back">
              <span class="card__magnet"></span>
              <div class="card__sing">
                  {{ cvc}}
              </div>

          </div>
      </aside>
      <section class="form">
          <div class="form__field">
              <label for="name" class="form__label">cardholder name</label>
              <input type="text" id="name" />
          </div>
          <div class="form__field">
              <label for="cardNumber" class="form__label">cardholder name</label>
              <input type="text" maxlength="19" :value="formatCardNumber" @input="updateValue" @keypress="isNumber"
                  placeholder="0000 0000 0000 0000" id="cardNumber" />
          </div>
          <div class="inline-form">
              <div class="form__field">
                  <label for="exp-date">exp. date (mm/yy)</label>
              <input type="month" />
              <Datepicker v-model="month"></Datepicker>
              </div>
          </div>
      </section>
//       0000 0000 0000 0000 Jane Appleseed 00/00 000 Cardholder Name e.g. Jane Appleseed Card Number e.g. 1234 5678 9123
//       0000 Exp. Date (MM/YY) MM YY CVC e.g. 123 Confirm

//  Completed state start

//       Thank you! We've added your card details Continue

//       <div>{{ message }}</div>
//       <div>

//       </div>
  </main>

</body>
</template>

<style scoped>

</style>
