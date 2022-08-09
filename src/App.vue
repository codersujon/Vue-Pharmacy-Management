<template>
  <div>
      <Login></Login>
     <div class="toasts">
       <Toast v-for="(toast, i) in toasts" 
       :key="i" 
       :toastType="toast.type" 
       :message="toast.message"></Toast>
     </div>
  </div>
</template>

<script>
import Login from './components/Login.vue'
import Toast from './components/Toast.vue';
export default {
  name: 'PharmacyManagementApp',

  data() {
    return {
      toasts:[
        // {
        //   type: "Success",
        //   message: "Done Successfully!"
        // },
        // {
        //   type: "Error",
        //   message: "Something Went to Wrong!"
        // },
      ]
    };
  },

  mounted() {
    this.$eventBus.on("toast", (data)=>{
      // console.log(data);
      this.toasts.push(data);
      this.removeOnToast();
    })
  },

  components:{
    Login,
    Toast
  },

  methods: {
    removeOnToast (){
      setTimeout(()=>{
         this.toasts.shift();
      },2000);
    }
  },
};
</script>

<style scoped>

</style>