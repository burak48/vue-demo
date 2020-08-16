<template>
  <div class="container">
    <apexchart :id="`chart`"
               type="area"
               :options="options"
               :series="series"
               height="250"
    />

    <v-data-table :headers="headers"
                 :items="desserts"
                  sort-by="calories"
                  hide-default-footer
                  class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar flat color="white">
          <v-toolbar-title>Records</v-toolbar-title>
            <v-divider class="mx-4"
                       inset
                       vertical
            >
            </v-divider>
            <v-spacer></v-spacer>
            <v-dialog v-model="dialog" max-width="500px">
              <v-card>
                <v-card-text>
                  <v-container>
                    <v-row>
                      <v-col cols="12" sm="4" md="4">
                        <v-text-field v-model="editedItem.user" label="User ID"></v-text-field>
                      </v-col>
                      <v-col cols="12" sm="4" md="4">
                        <v-text-field v-model="editedItem.attendance" label="Attendance"></v-text-field>
                      </v-col>
                      <v-col cols="12" sm="4" md="4">
                        <v-text-field v-model="editedItem.description" label="Description"></v-text-field>
                      </v-col>
                    </v-row>
                  </v-container>
                </v-card-text>
              </v-card>
            </v-dialog>
          </v-toolbar>
        </template>
        <template v-slot:no-data>
          <v-btn color="primary" @click="initialize">Reset</v-btn>
        </template>
    </v-data-table>

    <!--
    <section id="counter-stats" class="wow fadeInRight" data-wow-duration="1.4s">
      <div class="container">
        <div class="row">

          <div class="col-lg-2 stats">
            <i class="fa fa-code" aria-hidden="true"></i>
            <div class="counting" data-count="900000">350</div>
            <h5>Records</h5>
          </div>

          <div class="col-lg-3 stats">
            <i class="fa fa-check" aria-hidden="true"></i>
            <div class="counting" data-count="280">700</div>
            <h5>Views</h5>
          </div>

          <div class="col-lg-2 stats">
            <i class="fa fa-user" aria-hidden="true"></i>
            <div class="counting" data-count="75">15</div>
            <h5>User</h5>
          </div>

          <div class="col-lg-3 stats">
            <i class="fa fa-coffee" aria-hidden="true"></i>
            <div class="counting" data-count="999">1</div>
            <h5>Team</h5>
          </div>

          <div class="col-lg-2 stats">
            <i class="fa fa-coffee" aria-hidden="true"></i>
            <div class="counting" data-count="999">1</div>
            <h5>Department</h5>
          </div>
          
        </div>
      </div>
    </section>
    -->

  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      options: {
        chart: {
          height: 250,
          type: 'area',
          toolbar: {
            show: false
          },
        },
        dataLabels: {
          enabled: false
        },
        stroke: {
          curve: 'smooth'
        },
        xaxis: {
          type: 'datetime',
          categories: ["2018-09-19T00:00:00.000Z", "2018-09-19T01:30:00.000Z", "2018-09-19T02:30:00.000Z", "2018-09-19T03:30:00.000Z", "2018-09-19T04:30:00.000Z", "2018-09-19T05:30:00.000Z", "2018-09-19T06:30:00.000Z"]
        },
        tooltip: {
          x: {
            format: 'dd/MM/yy HH:mm'
          },
        },
      },
      series: [
        {
          name: 'Views',
          data: [31, 40, 28, 51, 42, 109, 100]
        },
        {
          name: 'Records',
          data: [11, 32, 45, 32, 34, 52, 41]
        }
      ],
      dialog: false,
      headers: [
        {
          text: 'User ID',
          align: 'start',
          value: 'user',
        },
        { text: 'Attendance', value: 'attendance', sortable: false },
        { text: 'Description', value: 'description' }
      ],
      desserts: [],
      editedIndex: -1,
      editedItem: {
        user: '',
        attendance: 0,
        description: 0
      },
      defaultItem: {
        user: '',
        attendance: 0,
        description: 0
      },
    }
  },
    created () {
      this.initialize()
    },

    methods: {
      initialize () {
        this.desserts = [
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
        ]
      },
    }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}

section#counter-stats {
	display: flex;
	justify-content: center;
	margin-top: 100px;
}

.stats {
	text-align: center;
	font-size: 35px;
	font-weight: 700;
	font-family: "Montserrat", sans-serif;
}

.stats .fa {
	color: #008080;
	font-size: 60px;
}

section#counter-stats[data-v-fae5bece] {
	display: flex;
	justify-content: center;
	margin-top: 0 !important;
}

</style>
