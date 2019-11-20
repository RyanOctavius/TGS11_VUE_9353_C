<template>
<v-container mb-4>
        <v-card pa-2>
            <v-container  grid-list-md style="margin-top:10%" >
                <v-layout row wrap >
                    <v-flex md4 class="text-center lg5" style="margin-top:3% ; margin-left:5%">
                       <v-responsive>
                        <v-img src="https://pbs.twimg.com/media/DQDDZxNW0AAX-Qu.jpg" ></v-img>
                      </v-responsive>
                    </v-flex >
                    <v-flex md4 class="text-center lg5" style="margin-left:7%">
                      <v-icon size="90" color="blue accent-3">mdi-account</v-icon>
                        <h1 style="margin-top:-2%">LOG IN PAGE</h1>
                        <v-text-field placeholder="Email" v-model="user.email"></v-text-field>
                        <v-text-field placeholder="Password" type="password" v-model="user.password"></v-text-field>
                        <v-btn depressed dark rounded style="text-transform: none !important;" color="blue accent-3" @click="login()">
                            LOG IN
                        </v-btn>
                        <br>
                        <v-card-text>Don't have an account?</v-card-text>
                        <v-btn elevation="0">SIGN UP</v-btn>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-card>
        <v-snackbar v-model="snackbar"
        :color="color" 
        :multi-line="true" 
        :timeout="3000">
        <v-icon>mdi-close</v-icon> {{ text }} 
        <v-btn dark text @click="snackbar = false"> </v-btn> </v-snackbar>
    </v-container>
</template>
<script>
export default {
  data() {
         return {
             snackbar: false,
             load: false,
             user: {
                 email: '',
                 password:''
             },
             users: new FormData,
             errors: '',
             updatedId: '',
             text: '',
             color: null,
             load: false,
         }
     },
     methods: {
        login() {
            var url = this.$apiUrl + "/Auth";
            this.users = new FormData();
            this.users.append("email", this.user.email);
            this.users.append("password", this.user.password);
            this.$http.post(url, this.users).then(response => {
                if (response.data.token) {
                    localStorage.setItem("token", response.data.token);
                    this.$router.push('/branches');
                } else {
                    this.snackbar = true;
                    this.text = "Invalid Username or Password!";
                    this.color = "red";
                    this.load = false;
                }
            });
        }
        }
        }
</script>