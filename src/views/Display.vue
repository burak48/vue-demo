<template>
  <div class="container" style="margin-top: 2%;">

      <v-form>
    <v-layout row wrap>

      <v-row align="center">
        <v-col class="d-flex" cols="12">
          <v-select
            :items="items"
            label="Department"
          >
          </v-select>
        </v-col>
      </v-row>

      <v-spacer></v-spacer>

      <v-row align="center">
        <v-col class="d-flex" cols="12">
          <v-select
            :items="items"
            label="Team"
          >
          </v-select>
        </v-col>
      </v-row>

<v-spacer></v-spacer>

      <v-row align="center">
        <v-col class="d-flex" cols="12">
          <v-select
            :items="items"
            label="User"
          >
          </v-select>
        </v-col>
      </v-row>
    
    <v-spacer></v-spacer>

    <v-flex xs6 sm12 md4 style="margin-top: 0.75rem;">
      <v-menu
        v-model="modal"
        :close-on-content-click="false"
        persistent
        lazy
        transition="scale-transition"
        offset-y
        full-width
        min-width="290px"
      >
        <template v-slot:activator="{ on }">
          <v-text-field
            v-model="dateRangeText"
            label="Select Date Range"
            readonly
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker v-model="dates" range></v-date-picker>
      </v-menu>
    </v-flex>


  </v-layout>

      <v-btn
        color="primary"
        class="mr-4"
        @click="validate"
      >
      Filter
    </v-btn>

    <v-btn
      color="error"
      class="mr-4"
      @click="reset"
    >
      Reset
    </v-btn>

      </v-form>


    <v-card-title>
      Records
    </v-card-title>
    <v-data-table hide-default-footer item-key="name" class="elevation-1" loading loading-text="Loading... Please wait"></v-data-table>
    <v-data-table v-model="selected"
                  :headers="headers"
                  :items="desserts"
                  item-key="name"
                  show-select
                  class="elevation-1"
    >
    </v-data-table>
    
    <v-card style="border-top-left-radius: 0; border-top-right-radius: 0; box-shadow: 0px 5px 1px -2px rgba(0, 0, 0, 0.2), 0px 5px 2px 0px rgba(0, 0, 0, 0.14), 0px 5px 5px 0px rgba(0, 0, 0, 0.12);">
    <v-card-text>
            <div style="position: absolute; top: -42px" class="body-1 font-weight-bold">
              <v-btn text normal >Export by Month</v-btn>
            <v-btn text normal >Export by Day</v-btn>
            </div>
          </v-card-text>
          
          <!--
          <v-card-actions class="actionsDetails" style="background: rgb(249, 249, 249); border-top-left-radius: 0; border-top-right-radius: 0">
            <v-btn text normal >Export by Month</v-btn>
            <v-btn text normal >Export by Day</v-btn>
          </v-card-actions>
          -->
    </v-card>

  </div>
</template>

<script>
  export default {
    data () {
      return {
        date: new Date().toISOString().substr(0, 10),
        dates: ['2019-09-10', '2019-09-20'],
        menu: false,
        modal: false,
        menu2: false,
        items: ['Foo', 'Bar', 'Fizz', 'Buzz'],
        singleSelect: false,
        selected: [],
        headers: [
          {
            text: 'User ID',
            align: 'start',
            sortable: false,
            value: 'user',
          },
          { text: 'Attendance', value: 'attendance', sortable: false },
          { text: 'Description', value: 'description', sortable: false }
        ],
        desserts: [
          {
            user: 'Frozen Yogurt',
            attendance: 159,
            description: 6.0,
          },
          {
            user: 'Ice cream sandwich',
            attendance: 237,
            description: 9.0
          },
          {
            user: 'Eclair',
            attendance: 262,
            description: 16.0
          },
          {
            user: 'Cupcake',
            attendance: 305,
            description: 3.7
          },
          {
            user: 'Gingerbread',
            attendance: 356,
            description: 16.0
          },
          {
            user: 'Jelly bean',
            attendance: 375,
            description: 0.0
          },
          {
            user: 'Lollipop',
            attendance: 392,
            description: 0.2
          },
          {
            user: 'Honeycomb',
            attendance: 408,
            description: 3.2
          },
          {
            user: 'Donut',
            attendance: 452,
            description: 25.0
          },
          {
            user: 'KitKat',
            attendance: 518,
            description: 26.0
          },
        ],
      }
    },
    computed: {
      dateRangeText () {
        return this.dates.join(' ~ ')
      },
    },
    methods: {
      validate () {
        this.$refs.form.validate()
      }
    }
  }
</script>
