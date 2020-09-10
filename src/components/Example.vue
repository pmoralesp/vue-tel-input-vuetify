<template>
  <v-container>
    <v-row justify="center">
      <v-col cols="6">
        <vue-tel-input-vuetify
          v-model="telefono"
          outlined
          :valid-characters-only="true"
          select-label="Code"
          @input="onInput"
          @country-changed="onChange"
          mode="significant"
          hideArrow
          :prefix="'+' + phone.prefix"
          :error="error"
          :errorMessages="errorMsg"
        />
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="6">
        <div v-if="phone.number" style="color: #e83e8c">
          <span>
            Number:
            <strong>{{ phone.number }}</strong
            >,&nbsp;
          </span>
          <span>
            Is valid:
            <strong>{{ phone.valid }}</strong
            >,&nbsp;
          </span>
          <span>
            Country:
            <strong>{{ phone.country }}</strong>
          </span>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import VueTelInputVuetify from '../lib/vue-tel-input-vuetify.vue';

export default {
  name: 'Example',
  components: {
    VueTelInputVuetify,
  },
  data() {
    return {
      phone: {
        number: '',
        valid: false,
        country: undefined,
        prefix: '',
      },
      error: false,
      errorMsg: '',
      telefono: '+56994162312',
      // telefono: '+5723304056',
    };
  },
  methods: {
    onInput(formattedNumber, { number, valid, country }) {
      this.phone.number = number.international;
      this.phone.valid = valid;
      this.phone.country = country && country.name;
      this.error = !this.phone.valid;
      if (this.error) {
        this.errorMsg = 'Número no válido';
      } else {
        this.errorMsg = '';
      }
      console.log('Teléfono: ', this.telefono);
    },
    onChange(e) {
      this.phone.prefix = e.dialCode;
    },
  },
};
</script>
