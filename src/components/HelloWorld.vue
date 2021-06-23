<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="my-4">
        <h1 class="display-2 font-weight-bold mb-3">
          Form Validation Testing v0.1
        </h1>

        <p class="subheading font-weight-regular">
          For help developers to test their applications validation,
          <br>please join our online
          <a
            href="https://community.vuetifyjs.com"
            target="_blank"
          >Discord Community</a>
        </p>
      </v-col>
    </v-row>
    <v-row>
      <v-card class="mx-auto pa-3" style="border-radius:15px;border: 1px solid #e7e7e7" elevation="0" width="820px">
        <v-card-title>Add Requirment</v-card-title>
        <v-form
          class="ma-3"
          ref="form"
          v-model="valid"
          lazy-validation
        >
        <v-row>
          <v-col>
            <v-select
            v-model="select"
            :items="items"
            :rules="[v => !!v || 'Item is required']"
            label="Key"
            required
            outlined
          ></v-select>
          </v-col>
          <v-col>
            <v-text-field
            v-model="name"
            :counter="10"
            :rules="nameRules"
            label="Value"
            required
            outlined
          ></v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-btn
              color="warning"
              @click="resetValidation"
            >
              Add New
            </v-btn>
          </v-col>
        </v-row>
        <v-row class="pb-5">
          <v-col>
            <v-checkbox
            v-model="checkbox1"
            :rules="[v => !!v || 'You must agree to continue!']"
            label="Testing Issue"
            required
          ></v-checkbox>
          </v-col>
          <v-col>
            <v-checkbox
            v-model="checkbox2"
            :rules="[v => !!v || 'You must agree to continue!']"
            label="Equvalance Pertisioning"
            required
          ></v-checkbox>
          </v-col>
          <v-col>
            <v-checkbox
            v-model="checkbox3"
            :rules="[v => !!v || 'You must agree to continue!']"
            label="Boundary Value Analysis"
            required
          ></v-checkbox>
          </v-col>
        </v-row>
          <v-btn
            color="error"
            class="mr-4"
            @click="reset"
          >
            Reset Form
          </v-btn>
          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4"
            @click="validate"
          >
            Calculate
          </v-btn>
        </v-form>
      </v-card>
    </v-row>
    <v-card width="100%" class="mt-10" flat style="background-color:#e7e7e7;">
      <v-card-title align="center" class="mx-auto">
        Testing Result
      </v-card-title>
    </v-card>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 10) || 'Name must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      select: null,
      items: [
        'Data Type',
        'Length',
      ],
      checkbox1: false,
      checkbox2: false,
      checkbox3: false,

    }),

    methods: {
      validate () {
        this.$refs.form.validate()
      },
      reset () {
        this.$refs.form.reset()
      },
      resetValidation () {
        this.$refs.form.resetValidation()
      },
    },
  }
</script>
