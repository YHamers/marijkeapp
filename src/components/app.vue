<template>


  <f7-app v-bind="f7params" >




  <!-- Left panel with cover effect-->
  <f7-panel left cover theme-dark>
    <f7-view>
      <f7-page>
        <f7-navbar title="Left Panel"></f7-navbar>
        <f7-block>Does it work</f7-block>
      </f7-page>
    </f7-view>
  </f7-panel>

  <form class="list" id="my-form">
    <label>Product</label>
    <input type="text" v-model="this.product">
    <hr>
    
    <f7-list-button  type="submit" @click="add">Submit</f7-list-button>
    <f7-list-button  type="submit" @click="seeStatus">check Satus for product</f7-list-button>
    <f7-list-button  type="submit" @click="showItems">Check out your new items</f7-list-button>


  </form>

  <div class="error_label" v-if="showError">
    You must enter a name

  </div>

  <f7-block-title>Products to handle</f7-block-title>
      <f7-list>
        <f7-list-item v-for="(item, index) in items" :key="index" >
          {{item}}
          
          
        </f7-list-item>
      </f7-list>

      <hr>
      <hr>
    





  <!-- Right panel with reveal effect-->
  <f7-panel right reveal theme-dark>
    <f7-view>
      <f7-page>
        <f7-navbar title="Right Panel"></f7-navbar>
        <f7-block>Right panel content goes here</f7-block>
      </f7-page>
    </f7-view>
  </f7-panel>


  <!-- Your main view, should have "view-main" class -->
  <f7-view main class="safe-areas" url="/"></f7-view>


    <!-- Popup -->
    <f7-popup id="my-popup">
      <f7-view>
        <f7-page>
          <f7-navbar title="Popup">
            <f7-nav-right>
              <f7-link popup-close>Close</f7-link>
            </f7-nav-right>
          </f7-navbar>
          <f7-block>
            <p>Popup content goes here.</p>
          </f7-block>
        </f7-page>
      </f7-view>
    </f7-popup>

    <f7-login-screen id="my-login-screen">
      <f7-view>
        <f7-page login-screen>
          <f7-login-screen-title>Login</f7-login-screen-title>
          <f7-list form>
            <f7-list-input
              type="text"
              name="username"
              placeholder="Your username"
              v-model:value="username"
            ></f7-list-input>
            <f7-list-input
              type="password"
              name="password"
              placeholder="Your password"
              v-model:value="password"
            ></f7-list-input>
          </f7-list>
          <f7-list>
            <f7-list-button title="Sign In" @click="alertLoginData"></f7-list-button>
            <f7-block-footer>
              Some text about login information.<br>Click "Sign In" to close Login Screen
            </f7-block-footer>
          </f7-list>
        </f7-page>
      </f7-view>
    </f7-login-screen>
  </f7-app>
</template>
<script>
  import { ref, onMounted } from 'vue';
  import { f7, f7ready } from 'framework7-vue';



  


  import routes from '../js/routes.js';
  import store from '../js/store';

  

  export default {
    data(){
      return{
        items: ["groente", "fruit"],
        newproduct: '',
        product: ''
      }

    },
    setup() {

      // Framework7 Parameters
      const f7params = {
        name: 'marijkeapp3', // App name
        theme: 'auto', // Automatic theme detection
        showError: false,
        show: true,



        // App store
        store: store,
        // App routes
        routes: routes,
        // Register service worker
        serviceWorker: {
          path: '/service-worker.js',
        },
      };
      
      // Login screen data
      const username = ref('');
      const password = ref('');

      const alertLoginData = () => {
        f7.dialog.alert('Username: ' + username.value + '<br>Password: ' + password.value, () => {
          f7.loginScreen.close();
        });
      }
      onMounted(() => {
        f7ready(() => {


          // Call F7 APIs here
        });
      });
      

      return {
        f7params,
        username,
        password,
        alertLoginData,
      }
    },
    methods: {
      add(){
        if (this.validate(this.product)){
          this.items.push(this.product);
          this.product = "";
          console.log(this.items);

        }
        else{
          alert("idosodcsn");

        }
          
        },
      validate(value){
        if (value === ''){
          return false

        }
        else{
          return true

        }

      }

      
    },
    seeStatus(){
      console.log(this.f7params.product);
    },
    
   
    
    }
    

</script>