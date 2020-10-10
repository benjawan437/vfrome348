<template>
  <div>
    <h2>ชำระเงิน</h2>
    <v-card class="mx-auto pa-6" color="#69F0AE" max-width="900" elevation="15">
      <h3>รายละเอียดบัตรเครดิต</h3>
      <v-form ref="form" v-model="valid" lazy-validation>
        <v-row>
          <v-col cols="7">
            <v-text-field
              v-model="Pname"
              :rules="nameRules"
              label="ชื่อ-นามสกุล"
              required
            ></v-text-field>
          </v-col>
          <v-col cols="5">
            <v-text-field
              v-model="Pemail"
              :rules="emailRules"
              label="E-mail"
              prepend-icon="mdi-email"
              required
            >
              icon="mdi-cellphone"
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="6">
            <v-text-field
              v-model="Pncard"
              :rules="nameRules"
              name="input-7-1"
              label="ชื่อบนบัตร"
              required
            ></v-text-field>
          </v-col>
          <v-col cols="6">
            <v-text-field
              v-model="Pnumcard"
              :rules="nameRules"
              name="input-7-1"
              label="หมายเลขบัตร"
              required
            ></v-text-field> </v-col
        ></v-row>

        <v-row>
          <v-col cols="6" sm="6">
            <v-menu
              ref="menu"
              v-model="menu"
              :close-on-content-click="false"
              :return-value.sync="date"
              transition="scale-transition"
              offset-y
              max-width="290px"
              min-width="290px"
            >
              <template v-slot:activator="{ on, attrs }">
                <v-text-field
                  v-model="date"
                  label="วันหมดอายุ"
                  prepend-icon="mdi-calendar"
                  readonly
                  v-bind="attrs"
                  v-on="on"
                ></v-text-field>
              </template>
              <v-date-picker v-model="date" type="month" no-title scrollable>
                <v-spacer></v-spacer>
                <v-btn text color="primary" @click="menu = false">
                  Cancel
                </v-btn>
                <v-btn text color="primary" @click="$refs.menu.save(date)">
                  OK
                </v-btn>
              </v-date-picker>
            </v-menu>
          </v-col>

          <v-col cols="6" sm="6">
            <v-text-field
              v-model="Pscode"
              :rules="nameRules"
              name="input-7-1"
              label="รหัสรักษาความปลอดภัย"
              prepend-icon="mdi-key"
              required
            ></v-text-field>
          </v-col>
        </v-row>

        <v-row>
          <v-col cols="10"> </v-col>
          <v-col cols="2">
            <div class="text-center">
              <v-dialog v-model="dialog" width="800">
                <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    depressed
                    color="#558B2F"
                    :disabled="!valid"
                    v-bind="attrs"
                    v-on="on"
                    @click="validate"
                  >
                    SUMMIT
                  </v-btn>
                </template>

                <v-card class="pa-4" elevation="11">
                  <v-row>
                    <v-col cols="12"> ยืนยันข้อมูล </v-col>
                  </v-row>

                  <v-divider></v-divider>
                  <v-card-text
                    ><h4>
                      ชื่อ: {{ Pname }} <br />
                      E-mail: {{ Pemail }} <br />
                      ชื่อบนบัตร: {{ Pncard }} <br />
                      หมายเลขบัตร: {{ Pnumcard }} <br />
                      วันหมดอายุ {{ date }} <br />
                      รหัสรักษาความปลอดภัย {{ Pscode }} <br /></h4
                  ></v-card-text>

                  <v-divider></v-divider>

                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="primary" text @click="dialog = false">
                      แก้ไข
                    </v-btn>
                    <v-btn
                      color="primary"
                      text
                      @click=";(dialog = false), set(), reset()"
                    >
                      ตกลง
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </div>
          </v-col>
        </v-row>
      </v-form>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      Pname: null,
      add: '',
      Address: {},
      Pncard: '',
      Pemail: '',
      Pnumcard: '',
      arr: {},
      Pscode: '',
      date: new Date().toISOString().substr(0, 7),
      menu: false,
      nameRules: [(v) => !!v || 'please required'],
      emailRules: [
        (v) => !!v || 'E-mail is required',
        (v) => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
      valid: true,
    }
  },
  methods: {
    reset() {
      this.$refs.form.reset()
    },
    validate() {
      this.$refs.form.validate()
    },
    set() {
      this.arr = {
        Pname: this.Pname,
        Pemail: this.Pemail,
        Pncard: this.Pncard,
        Pnumcard: this.Pnumcard,
        date: this.date,
        Pscode: this.Pscode,
        address: {
          add: this.add,
          sub_district: this.sub_district,
          district: this.district,
          province: this.province,
        },
        description: this.description,
        date_in: this.datein,
        date_out: this.dateout,
        sub_district: this.sub_district,
        district: this.district,
        province: this.province,
      }
      this.$store.commit('set_arr', this.arr)
    },
  },
}
</script>
