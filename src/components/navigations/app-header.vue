<template>
  <header :class="{ black: isBlack }">
    <component :is="$route.name === 'home' ? 'span' : 'router-link'" to="/"
      >logo</component
    >
    <nav>
      <router-link to="/users">users </router-link>
      <router-link to="/"> home</router-link>
    </nav>
    <div class="rCol">
      <div class="modals">
        <p @click="updateModalValue('login')">login</p>
        <p @click="updateModalValue('register')">register</p>
      </div>
      <lang-switcher></lang-switcher>
      <label class="switch">
        <input type="checkbox" v-model="isBlack" />
        <span class="slider round" :class="{ black: isBlack }"></span>
      </label>
    </div>
    <!-- <app-form ref="asd"/> -->
  </header>
</template>

<script>
import { mapActions } from "vuex";
import langSwitcher from './lang-switcher.vue';
// import appForm from '../app-form.vue';
export default {
  components: { langSwitcher },
  // components: { appForm },
  data() {
    return {
      isBlack: false,
    };
  },
  watch: {
    isBlack(newValue) {
      localStorage.setItem("theme", newValue ? "black" : "white");
      this.$emit("setTheme", newValue ? "black" : "white");
      // newValue ? localStorage.theme = 'white' : localStorage.theme = 'black';
    },
  },
  methods: {
    test() {
      alert("test");
    },
    ...mapActions(["updateModalValue"]),
  },
  mounted() {
    console.log(localStorage.theme);
    localStorage.theme == "black"
      ? (this.isBlack = true)
      : (this.isBlack = false);
  },
};
</script>

<style lang="scss" scoped>
.modals{
  display: flex;
}
header {
  padding: 40px 60px;
  display: flex;
  justify-content: space-between;
  background-color: #173955;

  nav {
    a {
      color: #fff;
    }
    a:not(:last-of-type) {
      margin-right: 10px;
    }
  }
}

/* The switch - the box around the slider */
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

/* Hide default HTML checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

/* The slider */
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider,
.black {
  background-color: #173955;
}

input:focus + .slider,
.black {
  box-shadow: 0 0 10px #b7c8d6;
}

input:checked + .slider:before,
.black:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>
