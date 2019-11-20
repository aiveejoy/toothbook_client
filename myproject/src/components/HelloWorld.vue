<template>
  <v-container>
    <v-layout text-center wrap>
      <v-flex xs12>
        <v-img :src="require('@/assets/totii.png')" class="my-3" contain height="200"></v-img>
      </v-flex>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-dialog v-model="dialog" persistent max-width="600px">
            <template v-slot:activator="{ on }">
              <v-btn color="primary" dark v-on="on">BOOK SCHEDULE</v-btn>
            </template>
              <v-card class="elevation-12">
                <v-toolbar>
                  <!-- color="primary" dark flat -->
                  <img src="@/assets/totii.png" style="width:50px;height:auto" />
                  <v-spacer />
                  <v-toolbar-title>Please fill-in the following information</v-toolbar-title>
                  <v-spacer />
                </v-toolbar>
                <v-card-text>
                  <v-form ref="form" v-model="valid" lazy-validation>
                    <v-select
                    v-model="select"
                    :items="items"
                    :rules="[v => !!v || 'Item is required']"
                    label="Services"
                    required
                  ></v-select>
                  <v-menu
                    v-model="showPicker"
                    :close-on-content-click="false"
                    transition="scale-transition"
                    offset-y
                    full-width
                    max-width="290px"
                    min-width="290px"
                  >
                    <template v-slot:activator="{ on }">
                      <v-text-field
                        v-model="selectedDate"
                        label="Choose the date"
                        hint="YYYY/MM/DD"
                        persistent-hint
                        readonly
                        v-on="on"
                        aria-required="safsd"
                      ></v-text-field>
                    </template>
                    <v-date-picker v-model="selectedDate" no-title @input="showPicker = false"></v-date-picker>
                  </v-menu>
                    <v-text-field
                      v-model="name"
                      :counter="10"
                      :rules="nameRules"
                      label="Name"
                      required
                    ></v-text-field>
                    <v-text-field
                      v-model="lname"
                      :counter="10"
                      :rules="lnameRules"
                      label="Lastname"
                      required
                    ></v-text-field>

                    <v-text-field v-model="email" :rules="emailRules" label="E-mail" required></v-text-field>

                    <v-checkbox
                      v-model="checkbox"
                      :rules="[v => !!v || 'You must agree to continue!']"
                      label="Do you agree?"
                      required
                    ></v-checkbox>
                    <v-row justify="center">
                      <v-dialog v-model="dialog2" persistent max-width="290">
                        <template v-slot:activator="{ on }">
                          <v-btn color="success" dark @click="validate" v-on="on">Submit</v-btn>
                          <v-btn color="error" class="mr-4" @click="reset">Reset Form</v-btn>
                        </template>
                        <v-card>
                          <v-card-title class="headline">Successfully Saved!!!</v-card-title>
                          <!-- <v-card-text>Let Google help apps determine location. This means sending anonymous location data to Google, even when no apps are running.</v-card-text> -->
                          <v-card-actions>
                            <v-spacer></v-spacer>
                            <!-- <v-btn color="green darken-1" text @click="dialog = false">Disagree</v-btn> -->
                            <v-btn color="green darken-1" text @click="dialog = false">OK</v-btn>
                          </v-card-actions>
                        </v-card>
                      </v-dialog>
                    </v-row>

                    <!-- <v-btn color="warning" @click="resetValidation">Reset Validation</v-btn> -->
                  </v-form>
                </v-card-text>
                <v-card-actions>
                  <v-spacer />
                  <!-- <v-btn color="primary">Login</v-btn> -->
                </v-card-actions>
              </v-card>
          </v-dialog>
        </v-row>
      </v-container>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: "HelloWorld",
  data: () => ({
    dialog: false,
    dialog2: false,
    valid: true,
    name: "",
    nameRules: [
      v => !!v || "Name is required",
      v => (v && v.length <= 10) || "Name must be less than 10 characters"
    ],
    lnameRules: [
      v => !!v || "Name is required",
      v => (v && v.length <= 10) || "Name must be less than 10 characters"
    ],
    email: "",
    emailRules: [
      v => !!v || "E-mail is required",
      v => /.+@.+\..+/.test(v) || "E-mail must be valid"
    ],
    select: null,
    items: [
      "Dental Cleaning",
      "Fluoride Treatment",
      "Tooth Filling",
      "Extraction",
      "Cosmetic Dentistry",
      "Dental Implants"
    ],
    checkbox: false,
    picker: new Date().toISOString().substr(0, 10),
    showPicker: false,
    selectedDate: null
  }),
  methods: {
    validate() {
      if (this.$refs.form.validate()) {
        this.snackbar = true;
      }
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    }
  }
  
};
</script>
