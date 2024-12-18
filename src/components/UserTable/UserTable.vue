<template>
  <v-data-table
    :headers="headers"
    :items="users"
    :footer-props="{
      showFirstLastPage: true,
    }"
    :loading="loadingUsers"
    :sort-by="[{ key: 'id', order: 'asc' }]"
    loading-text="Loading users... Please wait"
  >
    <template v-slot:top>
      <v-toolbar flat>
        <v-toolbar-title>Users Table</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn color="primary" dark @click="openNewUserDialog">
          New User
        </v-btn>
        <v-btn color="primary" dark @click="fetchUsers">
          Refresh Data
        </v-btn>
      </v-toolbar>
    </template>

    <template v-slot:item.actions="{ item }">
      <v-icon class="me-2" size="small" @click="editItem(item)">
        mdi-pencil
      </v-icon>
      <v-icon size="small" @click="deleteItem(item)">
        mdi-delete
      </v-icon>
    </template>
  </v-data-table>

  <v-dialog v-model="dialog" max-width="500px">
    <v-card>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12">
              <v-text-field v-model="editedItem.name" label="Name"></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field v-model="editedItem.email" label="E-mail"></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field v-model="editedItem.address" label="Address"></v-text-field>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue-darken-1" variant="text" @click="close">
          Cancel
        </v-btn>
        <v-btn color="blue-darken-1" variant="text" @click="save">
          Save
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>

  <v-dialog v-model="dialogDelete" max-width="500px">
    <v-card>
      <v-card-title class="text-h6">Are you sure you want to delete this item?</v-card-title>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue-darken-1" variant="text" @click="closeDelete">Cancel</v-btn>
        <v-btn color="blue-darken-1" variant="text" @click="deleteItemConfirm">OK</v-btn>
        <v-spacer></v-spacer>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
import { ref, onMounted } from "vue";
import axios from "axios";

export default {
  name: "UserTable",
  setup() {
    const dialog = ref(false);
    const dialogDelete = ref(false);
    const users = ref([]);
    const loadingUsers = ref(false);
    const editedIndex = ref(-1);
    const editedItem = ref({
      name: "",
      email: "",
      address: "",
    });
    const defaultItem = {
      name: "",
      email: "",
      address: "",
    };

    const headers = [
      { title: "ID", key: "id", sortable: true },
      { title: "Name", key: "name" },
      { title: "E-mail", key: "email" },
      { title: "Address", key: "address" },
      { title: "Actions", key: "actions", sortable: false },
    ];

    const fetchUsers = async() => {
      loadingUsers.value = true;
      try {
        const {data} = await axios.get("https://jsonplaceholder.typicode.com/users")
        users.value = data.map((user) => ({
            id: user.id,
            name: user.name,
            email: user.email.toLowerCase(),
            address: `${user.address.street}, ${user.address.city}`,
          }));
          loadingUsers.value = false;
      } catch (error) {
        users.value= []
      }
      // axios
      //   .get("https://jsonplaceholder.typicode.com/users")
      //   .then((res) => {
      //     users.value = res.data.map((user) => ({
      //       id: user.id,
      //       name: user.name,
      //       email: user.email,
      //       address: `${user.address.street}, ${user.address.city}`,
      //     }));
      //   })
      //   .catch((error) => {
      //     console.error("Error fetching users:", error);
      //   })
      //   .finally(() => {
      //     loadingUsers.value = false;
        // });
    };

    const openNewUserDialog = () => {
      editedIndex.value = -1;
      editedItem.value = Object.assign({}, defaultItem);
      dialog.value = true;
    };

    const editItem = (item) => {
      editedIndex.value = users.value.indexOf(item);
      editedItem.value = Object.assign({}, item);
      dialog.value = true;
    };

    const save = () => {
      if (editedIndex.value > -1) {
        Object.assign(users.value[editedIndex.value], editedItem.value);
      } else {
        users.value.push({
          id: users.value.length + 1,
          ...editedItem.value,
        });
      }
      close();
    };

    const deleteItem = (item) => {
      editedIndex.value = users.value.indexOf(item);
      dialogDelete.value = true;
    };

    const deleteItemConfirm = () => {
      if (editedIndex.value > -1) {
        users.value.splice(editedIndex.value, 1);
      }
      closeDelete();
    };

    const close = () => {
      dialog.value = false;
      editedIndex.value = -1;
    };

    const closeDelete = () => {
      dialogDelete.value = false;
      editedIndex.value = -1;
    };

    onMounted(() => {
       fetchUsers();
    });

    return {
      dialog,
      dialogDelete,
      users,
      loadingUsers,
      editedItem,
      editedIndex,
      headers,
      fetchUsers,
      openNewUserDialog,
      editItem,
      save,
      deleteItem,
      deleteItemConfirm,
      close,
      closeDelete,
    };
  },
};
</script>

<style src="./UserTable.css"></style>
