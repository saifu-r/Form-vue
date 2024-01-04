<template>
  <div class="container">
    <form @submit.prevent="submitForm">
      <header><h2>Form Application</h2></header>
      <div class="form">
        <div
          class="text-input"
          :class="{ invalid: nameValidity === 'invalid' }"
        >
          <label>Enter Name</label>
          <input
            id="name"
            name="name"
            type="text"
            @blur="checkNameValidity"
            v-model="enteredName"
          />
          <p v-if="nameValidity === 'invalid'" style="color: red; margin: 0">
            *Please Input Name*
          </p>
        </div>
        <div class="number-input">
          <label>Enter Age</label>
          <input
            id="age"
            name="age"
            type="number"
            min="1"
            max="100"
            v-model.number="enteredAge"
          />
        </div>

        <div class="dropbox-input">
          <label for="referrer">How did you hear about us?</label>
          <select name="referrer" id="referrer" v-model="enteredReferrer">
            <option value="google">Google</option>
            <option value="wom">Word of mouth</option>
            <option value="newspaper">Newpaper</option>
          </select>
        </div>

        <div class="radiobutton-input">
          <h2>How do you learn?</h2>
          <div>
            <input
              type="radio"
              name="how"
              id="video"
              value="video"
              v-model="enteredHow"
            />
            <label for="video">Video Course</label>
          </div>
          <div>
            <input
              type="radio"
              name="how"
              id="blogs"
              value="blogs"
              v-model="enteredHow"
            />
            <label for="blogs">Blogs</label>
          </div>
          <div>
            <input
              type="radio"
              name="how"
              id="others"
              value="others"
              v-model="enteredHow"
            />
            <label for="others">Others</label>
          </div>
        </div>

        <div class="checkbox-input">
          <h2>What are you interested in?</h2>
          <div>
            <input
              type="checkbox"
              name="interest"
              id="news"
              value="news"
              v-model="enteredinterest"
            />
            <label for="news">News</label>
          </div>
          <div>
            <input
              type="checkbox"
              name="interest"
              id="tutorials"
              value="tutorials"
              v-model="enteredinterest"
            />
            <label for="tutorials">Tutorials</label>
          </div>
          <div>
            <input
              type="checkbox"
              name="interest"
              id="nothing"
              value="nothing"
              v-model="enteredinterest"
            />
            <label for="nothing">Nothing</label>
          </div>
        </div>

        <div class="button-input">
          <rating-control v-model="rating"></rating-control>
        </div>
       

        <div class="agreement">
          <input
            type="checkbox"
            name="agreement"
            id="agreement"
            value="agreement"
            v-model="enteredAgreement"
          />
          <label for="agreement">Agree to terms and conditions?</label>
        </div>
        <br>
        <base-button>Submit</base-button>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import RatingControl from "./RatingControl.vue";


export default defineComponent({
  components: { RatingControl },
  setup() {
    const enteredName = ref("");
    const enteredAge = ref();
    const enteredReferrer = ref("google");
    const enteredHow = ref("");
    const enteredinterest = ref([]);
    const enteredAgreement = ref("");
    const nameValidity = ref("pending");
    const rating = ref(null);

    const submitForm = () => {
      console.log("Referrer:" + enteredReferrer.value);
      console.log("Rating:" + rating.value);
      rating.value= null

    };

    const checkNameValidity = () => {
      if (enteredName.value.trim() === "") {
        nameValidity.value = "invalid";
      } else {
        nameValidity.value = "valid";
      }
    };

    return {
      enteredName,
      enteredAge,
      enteredReferrer,
      enteredHow,
      enteredinterest,
      enteredAgreement,
      nameValidity,
      checkNameValidity,
      submitForm,
      rating,
    };
  },
});
</script>

<style scoped>
.container {
  position: relative;
  top: 20%;
  width: 50%;
  left: 25%;
  border: 0.1rem solid black;
  border-radius: 15px;
  /* padding: 2rem; */
}

header {
  background-color: #3a0061;
  color: white;
  border-top-right-radius: 12px;
  border-top-left-radius: 12px;
  padding: 1rem;
}

header h2 {
  margin: 0;
}

.form {
  padding: 2rem;
}

.text-input,
.number-input,
.dropbox-input {
  display: flex;
  flex-direction: column;
  padding-bottom: 1rem;
  margin: 0;
}

.text-input.invalid input {
  border-color: red;
}
</style>
