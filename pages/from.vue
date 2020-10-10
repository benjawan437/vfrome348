<template>
  <div>
    <h2>จองตั๋วหนัง</h2>
    <v-card class="mx-auto pa-6" color="#FFAB40" max-width="900" elevation="15">
      <h3>รายละเอียดการจอง</h3>
      <v-form ref="form" v-model="valid" lazy-validation>
        <v-row>
          <v-col cols="6" sm="6">
            <v-select
              v-model="nmovie"
              :rules="nameRules"
              :items="['Foo', 'Bar', 'Fizz', 'Buzz']"
              label="ชื่อภาพยนตร์"
              required
            ></v-select>
          </v-col>
          <v-col cols="6" sm="6">
            <v-select
              v-model="cinema"
              :rules="nameRules"
              :items="[
                'เซ็นทรัลเฟสติวัล เชียงใหม่',
                'เมญ่าไลฟ์สไตล์ช็อปปิ้งเซ็นเตอร์',
                'เซ็นทรัลพลาซา เชียงใหม่ แอร์พอร์ต',
              ]"
              label="ชื่อโรงภาพยนตร์"
              required
            ></v-select>
          </v-col>
        </v-row>
        <h4>รอบ</h4>
        <v-row>
          <v-col cols="6" sm="6">
            <v-select
              v-model="day"
              :rules="nameRules"
              :items="['9/10/2020', '10/10/2020', '11/10/2020', '12/10/2020']"
              prepend-icon="mdi-calendar"
              label="รอบวันที่"
              required
            ></v-select>
          </v-col>

          <v-col cols="6" sm="6">
            <v-select
              v-model="time"
              :rules="nameRules"
              :items="['11.30', '14.00', '16.30', '19.00']"
              prepend-icon="mdi-clock"
              label="รอบเวลา"
              required
            ></v-select>
          </v-col>
        </v-row>
        <h4>ที่นั่ง</h4>
        <v-row>
          <v-col cols="12">
            <v-img
              class="center"
              height="500"
              width="500"
              src="https://storage.googleapis.com/techsauce-prod/ugc/uploads/2020/5/A4F22C8A-FEB1-4EB4-B7F9-88A0313B216A.jpeg"
            ></v-img>
          </v-col>
          <v-col cols="6" sm="6">
            <v-select
              v-model="numpeo"
              :rules="nameRules"
              :items="items"
              prepend-icon="mdi-human"
              label="จำนวนคน"
              required
            ></v-select>
          </v-col>
          <v-col cols="6" sm="6">
            <v-select
              v-model="seat"
              :rules="nameRules"
              :items="[
                'VP1',
                'VP2',
                'VP3',
                'VP4',
                'A1',
                'A2',
                'A3',
                'C1',
                'C2',
              ]"
              prepend-icon="mdi-popcorn"
              label="ที่นั่ง"
              required
            ></v-select>
          </v-col>
        </v-row>
        <v-divider></v-divider>
        <h3>รายละเอียดผู้จอง</h3>
        <v-row>
          <v-col cols="6" sm="6">
            <v-text-field
              v-model="name"
              :rules="nameRules"
              label="ชื่อ-นามสกุล"
              required
            ></v-text-field>
          </v-col>
          <v-col cols="6">
            <v-text-field
              v-model="email"
              :rules="nameRules"
              label="E-mail"
              prepend-icon="mdi-email"
              required
            >
            </v-text-field>
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
                    color="#E65100"
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
                      ชื่อ: {{ name }} <br />
                      E-mail: {{ email }} <br />
                      ภาพยนตร์: {{ nmovie }} <br />
                      โรงภาพยนตร์: {{ cinema }} <br />
                      รอบวันที่: {{ day }} | เวลา: {{ time }}<br />
                      จำนวนคน: {{ numpeo }} คน | ที่นั่ง: {{ seat }}<br /></h4
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
      nmovie: null,
      cinema: '',
      add: '',
      Address: {},
      name: '',
      email: '',
      items: [1, 2, 3, 4, 5, 6],
      arr: {},
      description: '',
      numpeo: '',
      seat: '',
      time: '',
      day: '',
      dialog: false,
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
        nmovie: this.nmovie,
        cinema: this.cinema,
        email: this.email,
        name: this.name,
        day: this.day,
        time: this.time,
        numpeo: this.numpeo,
        seat: this.seat,
        address: {
          add: this.add,
          district: this.district,
          province: this.province,
        },
        description: this.description,
        district: this.district,
        province: this.province,
      }
      this.$store.commit('set_arr', this.arr)
    },
  },
}
</script>
