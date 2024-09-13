  <template>
    <!-- Section: Design Block -->
    <section>
      <!-- Jumbotron -->
      <div class="px-4 py-5 px-md-5 text-center text-lg-start" style="background-color: hsl(0, 0%, 96%)">
        <div class="container">
          <div class="row gx-lg-5 align-items-center">
            <div class="col-lg-6 mb-5 mb-lg-0">
              <h1 class="my-5 display-3 fw-bold ls-tight">
                The best offer <br />
                <span class="text-primary">for your business</span>
              </h1>
              <p style="color: hsl(217, 10%, 50.8%)">
                Lorem ipsum dolor sit amet consectetur adipisicing elit.
                Eveniet, itaque accusantium odio, soluta, corrupti aliquam
                quibusdam tempora at cupiditate quis eum maiores libero
                veritatis? Dicta facilis sint aliquid ipsum atque?
              </p>
            </div>

            <div class="col-lg-6 mb-5 mb-lg-0">
              <div class="card">
                <div class="card-body py-5 px-md-5">
                  <form @submit.prevent="signUp">
                    <!-- 2 column grid layout with text inputs for the first and last names -->
                    <div class="row">
                      <div class="col-md-6 mb-4">
                        <div data-mdb-input-init class="form-outline">
                          <input v-model="name" type="text" id="form3Example1" class="form-control" />
                          <label class="form-label" for="form3Example1">First name</label>
                        </div>
                      </div>

                      <div class="col-md-6 mb-4">
                        <div data-mdb-input-init class="form-outline">
                          <input v-model="surname" type="text" id="form3Example2" class="form-control" />
                          <label class="form-label" for="form3Example2">Last name</label>
                        </div>
                      </div>
                    </div>

                    <!-- Email input -->
                    <div data-mdb-input-init class="form-outline mb-4">
                      <input v-model="email" type="email" id="form3Example3" class="form-control" />
                      <label class="form-label" for="form3Example3">Email address</label>
                    </div>

                    <!-- Password input -->
                    <div data-mdb-input-init class="form-outline mb-4">
                      <input v-model="password" type="password" id="form3Example4" class="form-control" />
                      <label class="form-label" for="form3Example4">Password</label>
                    </div>

                    <!-- Checkbox -->
                    <div class="form-check d-flex justify-content-center mb-4">
                      <input v-model="newspaper" class="form-check-input me-2" type="checkbox" id="form2Example33" />
                      <label class="form-check-label" for="form2Example33">
                        Subscribe to our newsletter
                      </label>
                    </div>

                    <!-- Submit button -->
                    <button type="submit" data-mdb-button-init data-mdb-ripple-init class="btn btn-primary btn-block mb-4">
                      Sign up
                    </button>

                    <!-- Register buttons -->
                    <div class="text-center">
                      <p>or sign up with:</p>
                      <button type="button" data-mdb-button-init data-mdb-ripple-init class="btn btn-link btn-floating mx-1">
                        <i class="fab fa-facebook-f"></i>
                      </button>

                      <button type="button" data-mdb-button-init data-mdb-ripple-init class="btn btn-link btn-floating mx-1">
                        <i class="fab fa-google"></i>
                      </button>

                      <button type="button" data-mdb-button-init data-mdb-ripple-init class="btn btn-link btn-floating mx-1">
                        <i class="fab fa-twitter"></i>
                      </button>

                      <button type="button" data-mdb-button-init data-mdb-ripple-init class="btn btn-link btn-floating mx-1">
                        <i class="fab fa-github"></i>
                      </button>
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- Jumbotron -->
    </section>
    <!-- Section: Design Block -->
  </template>

  <script>
  import axios from 'axios';

  export default {
    name: "signup-com",
    data() {
      return {
        name: "",
        surname: "",
        email: "",
        password: "",
        newspaper: false
      }
    },
    methods: {
      async signUp() {
        try {
          // abri ./json no cmd
          // digita json-server --watch db.json
          const response = await axios.post("http://localhost:3000/users", {
            name: this.name,
            surname: this.surname,
            email: this.email,
            password: this.password,
            newspaper: this.newspaper
          });

          console.warn(response);
          if (response.status === 201) {
            alert("Sign up successful!");
            localStorage.setItem("user-info", JSON.stringify(response.data));
            this.$router.push({ name: "Home" });
          }

          console.log("Successfully submitted", response.data);
        } catch (error) {
          console.error("There was an error!", error);
        }
      }
    }
  }
  </script>
