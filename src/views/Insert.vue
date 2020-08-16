<template>
    <div class="container" style="margin-top: 2%;">
        <v-data-table :headers="headers"
                      :items="desserts"
                      sort-by="calories"
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
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn color="primary"
                                       dark
                                       class="mb-2"
                                       v-bind="attrs"
                                       v-on="on"
                                >
                                    New Record
                                </v-btn>
                            </template>
                            <v-card>
                                <v-card-title>
                                    <span class="headline">{{ formTitle }}</span>
                                </v-card-title>
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
                                <v-card-actions>
                                    <v-spacer></v-spacer>
                                    <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
                                    <v-btn color="blue darken-1" text @click="save">Save</v-btn>
                                </v-card-actions>
                            </v-card>
                        </v-dialog>
                    </v-toolbar>
                </template>
                <template v-slot:item.actions="{ item }">
                    <v-icon small
                            class="mr-2"
                            @click="editItem(item)"
                    >
                        mdi-pencil
                    </v-icon>
                    <v-icon small
                            @click="deleteItem(item)"
                    >
                        mdi-delete
                    </v-icon>
                </template>
                <template v-slot:no-data>
                    <v-btn color="primary" @click="initialize">Reset</v-btn>
                </template>
            </v-data-table>
        </div>
</template>

<script>
export default {
    data: () => ({
      dialog: false,
      headers: [
        {
          text: 'User ID',
          align: 'start',
          sortable: false,
          value: 'user',
        },
        { text: 'Attendance', value: 'attendance', sortable: false },
        { text: 'Description', value: 'description', sortable: false },
        { text: 'Actions', value: 'actions', sortable: false },
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
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
      },
    },

    watch: {
      dialog (val) {
        val || this.close()
      },
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

      editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        const index = this.desserts.indexOf(item)
        confirm('Are you sure you want to delete this item?') && this.desserts.splice(index, 1)
      },

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.desserts[this.editedIndex], this.editedItem)
        } else {
          this.desserts.push(this.editedItem)
        }
        this.close()
      },
    }
}
</script>
