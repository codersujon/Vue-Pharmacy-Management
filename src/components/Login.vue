<template>
  <div class="login-page">
    <div class="login-card">
      <div class="text-center">
        <img src="/images/lock.png" alt="" class="login-card__icon">
        <h1>User Login</h1>
      </div>
      <form action="#" @submit.prevent="handleSubmit">
        <label class="block">Email</label>
        <input type="email" placeholder="Enter your email" v-model="formData.email"  ref="email">
        <label class="block mt-3">Password</label>
        <input type="password" placeholder="Enter your password" v-model="formData.password" required ref="password">
        <button type="submit" class="block mt-3 w-100">Login</button>
        <div class="d-flex jc-between mt-3">
          <div>
            <label>
              <input type="checkbox">
              Remember Me
            </label>
          </div>
          <div>
            <a href="#">Forgot Password?</a>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>

  export default {
    data: () => ({
      formData: {
        email: "",
        password: ""
      }
    }),

    methods: {
      handleSubmit() {
        console.log(this.formData);
        if (!this.formData.email) {
          // alert("Email can't be empty.");
          //TODO: Show Error Message on toast
           this.$eventBus.emit('toast', { 
            type: "Success",
            message: "Email can't be empty."
          })
          this.$refs.email.focus();
          return;
        }

        if (this.formData.password.length < 6) {
          // alert("Password must be at least 6 characters long.");
          //TODO: SHOW ERROR MESSAGE ON TOAST
          this.$eventBus.emit('toast', { 
            type: "Error",
            message: "Password must be at least 6 characters long."
          })
          this.$refs.password.focus();
          return;
        }

        //TODO: CALL API
      }
    }
  };
</script>

<style scoped>
  .login-page {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgb(235, 235, 235);
  }

  .login-card {
    width: 400px;
    min-height: 193px;
    box-shadow: 0px 2px 9px 4px #dfdfdf;
    background-color: #fff;
    border-radius: 5px;
    padding: 44px 33px;
  }

  .login-card input[type="email"],
  .login-card input[type="password"] {
    width: 100%;
  }

  .login-card__icon {
    max-width: 77px;
  }

  @keyframes showhide {
    0% {
      opacity: 0;
      transform: scale(0.5);
    }

    50% {
      opacity: 0.5;
      transform: scale(1.2);
    }

    100% {
      opacity: 1;
      transform: scale(1);
    }
  }
</style>