<template>
  <div>
    <section
      class="text-3xl flex justify-center content-center flex-col mx-auto text-center"
    ></section>
    <section class="flex text-6xl justify-center content-center">
      <div class="days mr-2">
        {{ displayDays }}
        <div class="label text-sm">
          days
        </div>
      </div>
      <span>:</span>
      <div class="hours mx-2">
        {{ displayHours }}
        <div class="label text-sm ">
          hours
        </div>
      </div>

      <span>:</span>
      <div class="minutes mx-2">
        {{ displayMinutes }}
        <div class="label text-sm ">
          mins
        </div>
      </div>

      <span>:</span>
      <div class="seconds ml-2">
        {{ displaySeconds }}
        <div class="label text-sm ">
          seconds
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data: () => ({
    displayDays: 0,
    displayHours: 0,
    displayMinutes: 0,
    displaySeconds: 0,
  }),
  computed: {
    _seconds: () => 1000,
    _minutes() {
      return this._seconds * 60;
    },
    _hours() {
      return this._minutes * 60;
    },
    _days() {
      return this._hours * 24;
    },
  },
  mounted() {
    this.showRemaining();
  },
  methods: {
    formatNum: (num) => {
      return num < 10 ? "0" + num : num;
    },
    showRemaining() {
      const timer = setInterval(() => {
        const now = new Date();
        const end = new Date(2021, 8, 1, 0, 0, 0, 0);
        const distance = end.getTime() - now.getTime();

        if (distance < 0) {
          clearInterval(timer);
          return;
        }

        const days = Math.floor(distance / this._days);
        const hours = Math.floor((distance % this._days) / this._hours);
        const minutes = Math.floor((distance % this._hours) / this._minutes);
        const seconds = Math.floor((distance % this._minutes) / this._seconds);
        this.displayMinutes = this.formatNum(minutes);
        this.displaySeconds = this.formatNum(seconds);
        this.displayHours = this.formatNum(hours);
        this.displayDays = this.formatNum(days);
      }, 1000);
    },
  },
};
</script>

<style></style>
