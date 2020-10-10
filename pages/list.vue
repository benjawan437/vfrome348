<template>
  <div>
    <v-card color="#FFAB40">
      <v-card-title>
        <v-spacer></v-spacer>
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-line
          hide-details
        ></v-text-field>
      </v-card-title>
      <v-data-table
        :headers="headers"
        :items="desserts"
        :items-per-page="5"
        :search="search"
        class="elevation-3"
      ></v-data-table>
    </v-card>
    <v-card color="#69F0AE">
      <v-card-title>
        <v-spacer></v-spacer>
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-line
          hide-details
        ></v-text-field>
      </v-card-title>
      <v-data-table
        :subhead="subhead"
        :items="desserts"
        :items-per-page="5"
        :search="search"
        class="elevation-3"
      ></v-data-table>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: '',
      headers: [
        {
          text: 'ภาพยนตร์',
          value: 'nmovie',
        },
        {
          text: 'โรงภาพยนตร์',
          value: 'cinema',
        },
        {
          text: 'จองวันที่',
          value: 'day',
        },
        {
          text: 'จองเวลา',
          value: 'time',
        },
        {
          text: 'จำนวนคน',
          value: 'numpeo',
        },
        {
          text: 'เลขที่นั่ง',
          value: 'seat',
        },
        {
          text: 'ชื่อผู้จอง',
          value: 'name',
        },
        {
          text: 'E-mail',
          value: 'email',
        },
      ],
    }
  },
  computed: {
    desserts: {
      get() {
        return this.$nuxt.$store.state.list
      },
    },
    // listdata: {},
  },
}
</script>
