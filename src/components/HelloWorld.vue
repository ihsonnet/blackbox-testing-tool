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
          >Facebook Community</a>
        </p>
      </v-col>
    </v-row>
    <v-row>
      <v-card class="mx-auto pa-5" style="border-radius:15px;border: 1px solid #e7e7e7" elevation="0" width="820px">
        <v-card-title>Add Requirment</v-card-title>
        <v-form
          class="ma-3"
          ref="form"
          v-model="valid"
          lazy-validation
        >

<!-- dynamic row -->
        <v-row class="text-field" v-for="input,idx in requirements" :key="idx">
          <v-col>
            <v-select
            v-model="input.key"
            :items="items"
            :rules="[v => !!v || 'Item is required']"
            label="Key"
            required
            outlined
            dense
          ></v-select>
          </v-col>
          <v-col>
            <v-text-field
            v-model="input.value"
            :counter="10"
            :rules="nameRules"
            label="Value"
            :placeholder="input.key=='Input Type' ? 'ex. Text , Email , Password etc.' : 'ex. 0-30'"
            required
            outlined
            dense
          ></v-text-field>
          </v-col>
          <v-col cols="2">
            <v-btn :disabled="requirements.length<='1'" @click="deleteReq(input,requirements)" justify="center" rounded elevation="0" class="mx-auto" color="error lighten-1">
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </v-col>
        </v-row>

<!-- add btn  -->
        <v-row>
          <v-col>
            <v-btn
              color="warning lighten-1"
              @click="addReq(1,requirements)"
              elevation="0"
            >
              Add New
            </v-btn>
          </v-col>
        </v-row>

<!-- selector -->
        <v-row class="pb-5">
          <v-col>
            <v-checkbox
            v-model="issue"
            :rules="[issue==true || ecp==true || vba==true || 'You must Select at least one calculate method.']"
            label="Testing Issue"
          ></v-checkbox>
          </v-col>
          <v-col>
            <v-checkbox
            v-model="ecp"
            :rules="[issue==true || ecp==true || vba==true || 'You must Select at least one calculate method.']"
            label="Equvalance Pertisioning"
          ></v-checkbox>
          </v-col>
          <v-col>
            <v-checkbox
            v-model="vba"
            :rules="[issue==true || ecp==true || vba==true || 'You must Select at least one calculate method.']"
            label="Boundary Value Analysis"
          ></v-checkbox>
          </v-col>
        </v-row>
          <v-btn
            color="error lighten-1"
            class="mr-4"
            @click="reset"
            elevation="0"
          >
            Reset Form
          </v-btn>
          <v-btn
            :disabled="!valid"
            color="success lighten-1"
            class="mr-4"
            @click="validate"
            elevation="0"
          >
            Calculate
          </v-btn>
        </v-form>
      </v-card>
    </v-row>
    <v-card width="100%" class="mt-10 pa-3" flat style="background-color:#e7e7e7;border-radius:15px">
      <v-card-title align="center" class="mx-auto">
        Testing Result
      </v-card-title>
      <v-divider color="#e7e7e7"></v-divider>
       <v-card-text v-if="calculate">
         <v-row v-if="issue">
         <v-col>
            <h3>Testing Issues</h3>
          * Comming Soon
         </v-col>
        </v-row>
        <br>
        <v-row v-if="ecp">
         <v-col>
            <h3>Equbalance Class Pertisioning</h3>
          * Comming Soon
         </v-col>
        </v-row>
        <br>
         <v-row v-if="vba">
         <v-col>
            <h3>Boundary Value Analysis</h3>
            <br>
            <v-card class="mx-auto pa-5" elevation="0" style="max-width:900px;background-color:white;border-radius:15px">
              <v-row class="mx-auto" style="max-width:800px;">
              <v-col cols="6" style="text-align:center">
                <div style="margin-left:100px;color:red;">Boundary</div>
              </v-col>
              <v-col cols="6" style="text-align:center">
                <div style="margin-right:100px;color:red;">Boundary</div>
              </v-col>
            </v-row>
            <v-row 
              class="mx-auto" 
              style="max-width:800px;text-align:center;border-bottom: 2px dotted gray">
              <v-col>
                <div style="text-align:right">{{minBoundary-1}}<span style="margin-left:30px;color:red" ><b>{{minBoundary}}</b></span></div>
              </v-col>
              <v-col>
                <div style="margin-left:10px;text-align:left">{{parseInt(minBoundary)+1}}<span style="text-align:right;margin-left:190px;" >{{maxBoundary-1}}</span></div>
              </v-col>
              <v-col>
                <div style="text-align:left"><span style="margin-right:30px;color:red" ><b>{{maxBoundary}}</b></span>{{ parseInt(maxBoundary)+1 }}</div>
              </v-col>
            </v-row>
            <v-row class="mx-auto" style="max-width:800px;">
              <v-col cols="6" style="text-align:right;padding-right:40px">
                <div>Boundary-1 <span style="margin-left:50px;">Boundary+1</span></div>
              </v-col>
              <v-col cols="6" style="text-align:left;padding-left:60px">
                <div><span style="margin-right:50px;">Boundary-1</span>Boundary+1</div>
              </v-col>
            </v-row>

<!-- test case -->
            <v-row>
              <v-col>
                <br>
                <b>Test Cases are : </b> {{parseInt(minBoundary)-1}} , {{parseInt(minBoundary)}} , {{parseInt(minBoundary)+1}} , {{parseInt(maxBoundary)-1}} , {{parseInt(maxBoundary)}}  , {{parseInt(maxBoundary)+1}}  <br>
                <br>
                <table>
                  <tr>
                    <th>Valid Test Case</th>
                    <th>Invalid TestCase</th>
                  </tr>
                  <tr>
                    <td>{{parseInt(minBoundary)}} , {{parseInt(minBoundary)+1}} , {{parseInt(maxBoundary)-1}} , {{parseInt(maxBoundary)}}  </td>
                    <td>{{parseInt(minBoundary)-1}} , {{parseInt(maxBoundary)+1}} </td>
                  </tr>
                </table>
              </v-col>
            </v-row>

            </v-card>
         </v-col>
        </v-row>
       </v-card-text>
       <br>
    </v-card>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      idx:0,
      issue: false,
      ecp: false,
      vba: false,
      calculate: false,
      requirements: [
        {
          key: "",
          value: ""
        }
      ],
      minBoundary:"",
      maxBoundary:"",
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Value is required',
        v => (v && v.length <= 10) || 'Value must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      select: null,
      items: [
        'Input Type',
        'Range',
      ],
      checkbox1: false,
      checkbox2: false,
      checkbox3: false,

    }),

    methods: {
      addReq(input,field){
        field.push({key:"",value: ""});
        console.log(this.requirements)
      },
      deleteReq(index,field){
        field.splice(index, 1)
      },
      calculateRange(){
        var ranges 
          for(var i=0;i<this.requirements.length;i++){
            if(this.requirements[i].key=="Range"){
            ranges  = this.requirements[i].value.split('-');
            }
          }
          this.minBoundary = ranges[0]
          this.maxBoundary = ranges[1]
      },
      validate () {
        this.$refs.form.validate()
        if(this.$refs.form.validate()){
          this.calculate=true;
          this.calculateRange();
        }
        else{
          this.calculate=false;
        }
      },
      reset () {
        this.$refs.form.reset()
        this.calculate=false;
      },
      resetValidation () {
        this.$refs.form.resetValidation()
      },
    },
  }
</script>
<style>
.text-field .col {
  padding-bottom: 0 !important;
  padding-top: 0 !important;
}
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td, th {
  border: 1px solid #dddddd;
  text-align: center;
  padding: 8px;
}

tr:nth-child(odd) {
  background-color: #dddddd;
}
</style>
