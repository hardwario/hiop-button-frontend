<template>
  <section>
    <form form v-on:submit.prevent="register">
      <b-field label="Device ID">
        <b-input v-model="id"></b-input>
      </b-field>

      <b-field label="SMS text">
        <b-input maxlength="200" type="textarea" v-model="text"></b-input>
      </b-field>

      <b-field label="Telefon 1">
        <b-input maxlength="30" v-model="phone1"></b-input>
      </b-field>

      <b-field label="Telefon 2">
        <b-input maxlength="30" v-model="phone2"></b-input>
      </b-field>

      <b-button type="is-success" expanded native-type="submit" :loading="loading">Registrovat</b-button>
    </form>
  </section>
</template>

<script>
export default {
  data() {
    return {
      id: 'nb@vf:901288001062015',
      text: 'Ducha plny text',
      phone1: '+420',
      phone2: '+420',
      loading: false,
    };
  },
  methods: {
    async register() {
      const data = {
        id: this.id,
        text: this.text,
        phone: [],
      };

      if (this.phone1.length > 4) {
        data.phone.push(this.phone1);
      }

      if (this.phone2.length > 4) {
        data.phone.push(this.phone2);
      }

      if (data.phone.length === 0) {
        return;
      }

      this.loading = true;

      const resp = await this.$http.post(
        'https://us-central1-hardwario-button.cloudfunctions.net/config',
        data
      );

      this.loading = false;

      console.log(resp);
    },
  },
};
</script>

