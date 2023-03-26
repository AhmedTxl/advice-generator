<template>
  <main>
    <div class="containerDiv shadow-[32px_36px_28px_4px_rgba(0,0,0,.1)] justify-center flex flex-col items-center">
      <p class=" text-sm text-[#52ffa8] uppercase font-medium tracking-[0.35em]" v-if="!loading">
        advice #{{ adviceID }}
      </p>
      <div v-show="loading">
        <img class="relative top-[10px]" src="./../../images/Rolling-1.2s-214px.svg" alt="loading spinner" />
      </div>
      <h1 class="text-center mt-4" v-if="!loading">“{{ adviceContent }}”</h1>
      <svg class="mt-[1.425rem] mb-[8px]" viewBox="12 0 420 20" xmlns="http://www.w3.org/2000/svg">
        <g fill="none" fill-rule="evenodd">
          <path fill="#4F5D74" d="M0 8h196v1H0zM248 8h196v1H248z" />
          <g transform="translate(212)" fill="#CEE3E9">
            <rect width="6" height="16" rx="3" />
            <rect x="14" width="6" height="16" rx="3" />
          </g>
        </g>
      </svg>
    </div>
    <button
      class="relative bottom-[32px] p-3 w-16 h-16 rounded-full bg-[#18da90] hover:shadow-[0_0_50px_#00f57a] transition ease-out shadow-[#00f57a] active:bg-[#00d66b]"
      @click="fetchData()"
      aria-label="Fetch Button">
      <svg width="25" height="25" xmlns="http://www.w3.org/2000/svg" class="max-[375px]:w-[25px] max-[375px]:h-[25px]">
        <path
          d="M20 0H4a4.005 4.005 0 0 0-4 4v16a4.005 4.005 0 0 0 4 4h16a4.005 4.005 0 0 0 4-4V4a4.005 4.005 0 0 0-4-4ZM7.5 18a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Z"
          fill="#00" />
      </svg>
    </button>
  </main>
  <footer class="text-slate-300 mt-8">
    Challenge by
    <a href="https://www.frontendmentor.io?ref=challenge" target="_blank">Frontend Mentor</a>.
    <br>
    Coded by <a href="https://github.com/AhmedTxl">AhmedTx</a>.
  </footer>
</template>

<script>
import axios from "axios";

export default {
  name: "adviceGenerator",
  data() {
    return {
      adviceID: 0,
      adviceContent: null,
      loading: true,
      errored: false,
    };
  },
  methods: {
    async fetchData() {
      this.loading = true;
      setTimeout(() => {
        axios
          .get("https://api.adviceslip.com/advice", {
            params: {
              _: new Date().getTime()
            }
          })
          .then((response) => {
            this.adviceID = response.data.slip.id;
            this.adviceContent = response.data.slip.advice;
          })
          .catch((error) => {
            console.log(error);
            this.errored = true;
          })
          .finally(() => (this.loading = false));
      }, 500);
    },
  },
  mounted() {
    this.fetchData();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "../styles.css";
</style>