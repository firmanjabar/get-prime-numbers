<template>
  <div class="hello">
    <h3>Get Prime Numbers</h3>
    <div class="container d-flex justify-content-center">
      <form @submit="handleSubmit" class="my-3">
        <div class="my-3">
          <label for="number" class="form-label">Input Number</label>
          <input
            type="number"
            class="form-control"
            id="number"
            aria-describedby="numberInfo"
            v-model="data"
          />
          <div id="numberInfo" class="form-text">
            We will check how many prime numbers bellow this number ({{ data }})
          </div>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </div>
    <div class="container">
      <button type="button" class="btn btn-primary">
        Total Prime Numbers:
        <span class="badge text-bg-danger">{{ result.length }}</span>
      </button>
      <div class="my-5">
        <h5
          class="badge rounded-pill text-bg-primary"
          v-for="numb in result"
          :key="numb"
        >
          {{ numb }}
        </h5>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const data = ref(2);
    const result = ref([]);

    const handleSubmit = (e) => {
      e.preventDefault();
      getPrimes(data.value);
    };

    function getPrimes(n) {
      function checkPrime(number) {
        if (number <= 1) {
          return false;
        } else {
          for (let i = 2; i < number; i++) {
            if (number % i == 0) {
              return false;
            }
          }
          return true;
        }
      }

      let arr = [];
      let newArr = [];
      for (let j = 2; j <= n; j++) {
        arr.push(j);
      }

      arr.forEach(function (element) {
        const isPrime = checkPrime(element);
        if (isPrime) {
          newArr.push(element);
        }
      });

      result.value = newArr;
    }

    // expose to template and other options API hooks
    return {
      data,
      handleSubmit,
      result,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
