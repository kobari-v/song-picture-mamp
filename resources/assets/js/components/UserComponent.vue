<template>
  <div>
    <button @click="createModal" class="btn btn-primary btn-block">Add New Task</button>

    <table class="table" v-if="users">
      <thead>
        <tr>
          <th scope="col">id</th>
          <th scope="col">Name</th>
          <th scope="col">Body</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user,index) in users" :key="index">
          <td>{{ index+1 }}</td>
          <!-- <td>{{ task.id }}</td> -->
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>
            <button class="btn btn-info">Edit</button>
          </td>
          <td>
            <button class="btn btn-danger">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
    <!-- create-modal -->
    <div
      class="modal fade"
      id="create-modal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Create Modal</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="alert alert-danger" v-if="errors.length > 0">
              <ul>
                <li v-for="error in errors" :key="error">{{ error }}</li>
              </ul>
            </div>
            <div class="form-group">
              <label for="name">Name</label>
              <input v-model="user.name" type="text" name id="name" class="form-control" />
            </div>

            <div class="form-group">
              <label for="email">email</label>
              <input v-model="user.email" type="text" name id="email" class="form-control" />
            </div>

            <div class="form-group">
              <label for="password">password</label>
              <input v-model="user.password" type="text" name id="password" class="form-control" />
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            <button @click="createUser" type="button" class="btn btn-primary">Save changes</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      user: {
        name: "",
        email: "",
        password: ""
      },
      users: [],
      uri: "http://localhost:8000/user",
      errors: []
    };
  },
  methods: {
    createModal() {
      $("#create-modal").modal("show");
    },
    createUser() {
      axios
        .post(this.uri, {
          name: this.user.name,
          email: this.user.email,
          password: this.user.password
        })
        .then(response => {
          this.users.push(response.data.user);
          $("#create-modal").modal("hide");
        })
        .catch(error => {
          this.errors = [];
          if (error.response.data.errors.name) {
            this.errors.push(error.response.data.errors.name[0]);
          }

          if (error.response.data.errors.email) {
            this.errors.push(error.response.data.errors.email[0]);
          }

          if (error.response.data.errors.password) {
            this.errors.push(error.response.data.errors.password[0]);
          }
        });
    },
    loadTasks() {
      axios.get(this.uri).then(response => {
        this.users = response.data.users;
      });
    }
  },
  mounted() {
    this.loadTasks();
    console.log(this.loadTasks);
  }
};
</script>