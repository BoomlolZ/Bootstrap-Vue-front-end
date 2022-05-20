<template>
  <b-container>
    <b-row align-h="center" class="mt-3">
      <b-col cols="5"><h1>Welcome to Data-Table</h1></b-col>
    </b-row>
    <b-row align-h="end">
      <b-col cols="3">
        <AddBtn @save="saveUser" />
      </b-col>
    </b-row>
    <div class="mt-4 text-center">
      <b-table-simple hover>
          <b-thead >
            <b-tr variant="dark">
              <b-th class="text-center"><h2>First-Name</h2></b-th>
              <b-th class="text-center"><h2>Last-Name</h2></b-th>
              <b-th class="text-center"><h2>User-Name</h2></b-th>
              <b-th class="text-center"><h2>Avatar</h2></b-th>
              <b-th class="text-center"><h2>Edit</h2></b-th>
              <b-th class="text-center"><h2>Delete</h2></b-th>
            </b-tr>
          </b-thead>
          <b-tbody >
            <b-tr v-for="user in users" :key="user.id" variant="warning ">
              <b-td>{{ user.fname }}</b-td>
              <b-td>{{ user.lname }}</b-td>
              <b-td>{{ user.username }}</b-td>
              <b-td>
                <b-avatar size="50px" :src="user.avatar"></b-avatar>
              </b-td>
              <b-td>
                <EditBtn
                  :id="user.id"
                  :fname="user.fname"
                  :lname="user.lname"
                  :username="user.username"
                  :email="user.email"
                  :avatar="user.avatar"
                  @edit="EditUser"
                />
              </b-td>
              <b-td><DeleteBtn :id="user.id" @delete="delUser"/></b-td>
            </b-tr>
          </b-tbody>
      </b-table-simple>
    </div>
  </b-container>
</template>
<script>
import AddBtn from "./components/AddBtn.vue";
import EditBtn from "./components/EditBtn.vue";
import DeleteBtn from "./components/DeleteBtn.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    AddBtn,
    DeleteBtn,
    EditBtn,
  },
  data() {
    return {
      users: [],
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    async getData() {
      const users = await axios.get("http://localhost:3333/user")
      // console.log(users.daata.length)
      if (users.status == "200") {
        this.users = users.data;
      } else {
        console.log(users);
      }
      return users
    },
    async saveUser(value) {
              const user = await axios.post("http://localhost:3333/user",value);
              console.log(user.data.message)
              console.log('success');
              if (user.data.status == "error1") {
                alert(user.data.message)
              } else {
              if (user.data.status == "ok") {
                alert(user.data.message)
                this.getData();
              }else{
                alert(user.data.message)
              }
              }
    },
    async EditUser(value) {
      const users = this.users
        // console.log(users)
        if (value.p_username == '') {
          alert("Username required / Username can't be null")
          console.log("ERROR: Username required")
        } else {
          for (let i = 0; i < users.length; i++) {
            // console.log(users[i].username)
            if ((value.p_username === users[i].username)) {
              // console.log("error")
              alert("username already exits")
              break;
            }else{
              // console.log('success');
              const user = await axios.put("http://localhost:3333/user",
              {
                id: value.id,
                fname: value.p_fname,
                lname: value.p_lname,
                username: value.p_username,
                email: value.p_email,
                avatar: value.p_avatar,
              });
              if (user.status == "200") {
                this.getData();
              }
            }
          }
        }
      },

      
    async delUser(value) {
      console.log(value);
      const user = await axios.delete(
        "http://localhost:3333/user",
        { data: { id: value.id } }
      );

      if (user.status == "200") {
        this.getData();
      }
    },
  },
};
</script>
