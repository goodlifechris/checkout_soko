<template>
  <v-row no-gutters class="py-10">
    <v-col cols="11" class="mx-auto">
      <v-form ref="form" @submit.prevent="submit">
        <v-row no-gutters>
          <v-col>
            <div class="w-75 mx-auto">
              <h1 class="__color__ font-weight-medium text-h4">
                Larry's Carpentry Store
              </h1>
              <v-breadcrumbs class="pl-0 text-body-2" :items="['Products', 'View Cart', 'Checkout']"></v-breadcrumbs>
              <h4 class="text-h5 font-weight-bold text-black mb-5">
                Customer information
              </h4>
              <div class="d-flex flex-column ga-2">
                <div>
                  <p class="font-weight-medium text-grey-lighten-2">Full name</p>
                  <v-text-field v-model="fullname" variant="outlined" density="compact" :rules="textRule" />
                </div>
                <div>
                  <p class="font-weight-medium text-grey-lighten-2">Email</p>
                  <v-text-field v-model="email" variant="outlined" density="compact" :rules="emailRule" />
                </div>
                <div>
                  <p class="font-weight-medium text-grey-lighten-2">Phone Number</p>
                  <v-text-field v-model="phone" variant="outlined" density="compact" :rules="phoneRule" />
                </div>
                <div>
                  <p class="font-weight-medium text-grey-lighten-2">City</p>
                  <v-text-field v-model="city" variant="outlined" density="compact" :rules="textRule" />
                </div>
                <div>
                  <p class="font-weight-medium text-grey-lighten-2">Zone</p>
                  <v-text-field v-model="zone" variant="outlined" density="compact" :rules="textRule" />
                </div>
                <v-checkbox v-model="save" color="#63C1EC" label="Save this information for faster check-out next time"
                  :rules="requiredRule"></v-checkbox>
              </div>
            </div>
          </v-col>
          <v-col class="d-flex align-center __bg_blueish_">
            <div class="w-75 mx-auto d-flex flex-column ga-3">
              <v-row no-gutters justify="space-between">
                <p class="font-weight-bold __font_18__">
                  Cart information
                </p>
                <p class="font-weight-bold __font_18__">2 Items</p>
              </v-row>
              <v-row v-for="i in 3" :key="i" no-gutters justify="space-between">
                <div class="d-flex ga-2">
                  <v-img src="/item.png" width="20px" height="20px" />
                  <p>
                    LCD Monitor
                  </p>
                </div>
                <p>100</p>
              </v-row>
              <v-divider></v-divider>
              <v-row no-gutters justify="space-between">
                <p>
                  Total
                </p>
                <p>kes 300</p>
              </v-row>
              <v-radio-group v-model="transfer" class="gy-3">
                <v-row no-gutters justify="space-between">
                  <v-radio label="Money" value="money" color="#63C1EC"></v-radio>
                  <div class="d-flex ga-2">
                    <v-img src="/safaricom.png" width="40px" />
                    <v-img src="/airtel.png" width="40px" />
                    <v-img src="/telkom.png" width="40px" />
                  </div>
                </v-row>
                <v-row no-gutters justify="space-between">
                  <div>
                    <v-radio label="Card" value="card" color="#63C1EC"></v-radio>
                  </div>
                  <div>
                    <v-img src="/equitel.png" width="60px" />
                  </div>
                </v-row>
              </v-radio-group>
              <div v-if="transfer === 'money'">
                <p>Phone Number</p>
                <v-text-field v-model="phoneNumber" variant="outlined" density="compact" :rules="phoneRule" />
              </div>
              <div v-else class="d-flex flex-column gy-3">
                <div>
                  <p class="font-weight-medium text-grey-lighten-2">Card holder name</p>
                  <v-text-field v-model="email" variant="outlined" type="text" density="compact" :rules="textRule" />
                </div>
                <div>
                  <p class="font-weight-medium text-grey-lighten-2">Card number</p>
                  <v-text-field v-model="email" type="number" variant="outlined" density="compact" :rules="requiredRule" />
                </div>
                <v-row no-gutters justify="space-between">
                  <div class="__w-45__">
                    <p class="font-weight-medium text-grey-lighten-2">Expiry (MM/YY)</p>
                    <v-text-field v-model="email" type="date" variant="outlined" density="compact" :rules="requiredRule" />
                  </div>
                  <div class="__w-45__">
                    <p class="font-weight-medium text-grey-lighten-2">CVC</p>
                    <v-text-field v-model="email" type="number" variant="outlined" density="compact"
                      :rules="requiredRule" />
                  </div>
                </v-row>
              </div>
              <v-btn class="text-capitalize py-6 text-white" color="#63C1EC" block type="submit">
                Place order
              </v-btn>
            </div>
          </v-col>
        </v-row>
      </v-form>
    </v-col>
  </v-row>
</template>

<script>
import { useText, useEmail, usePhone, useRequired } from '../composables/rules'
export default {
  name: 'HomePage',
  data: () => ({
    fullname: '',
    email: '',
    phone: '',
    city: '',
    zone: '',
    save: false,
    transfer: 'money',
    phoneNumber: '',
    textRule: useText(0, 50),
    emailRule: useEmail(),
    phoneRule: usePhone(),
    requiredRule: useRequired()
  }),
  methods: {
    async submit() {
      const state = await this.$refs.form.validate()
      if (state.valid) {
        //
      }
    }
  }
}
</script>
<style>
.__color__ {
  color: #63C1EC;
}

.__font_18__ {
  font-size: 18px;
}

.__bg_blueish_ {
  background-color: #FBFEFF;
}
.__w-45__{
  width: 48%;
}
</style>
