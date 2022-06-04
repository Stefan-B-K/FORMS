<template>
  <form @submit.prevent='submitForm'>

    <div class='form-control' :class="{ invalid: form.userNameValid === 'invalid' }">
      <label for='user-name'>Your Name</label>
      <input
          v-model.trim="form.userName"
          @blur="validateInput"
          id='user-name'
          type='text'
      />
      <h6 v-if="form.userNameValid === 'invalid'">Please, enter a valid name</h6>
    </div>

    <div class='form-control'>
      <label for='age'>Your Age (Years)</label>
      <input id='age' type='number' v-model="form.userAge"/>
    </div>

    <div class='form-control'>
      <label for='referrer'>How did you hear about us?</label>
      <select id='referrer' v-model="form.referer">
        <option :value="null">-- select --</option>
        <option v-for="(title, value) in dropDowns" :key="value"  :value='value'>
          {{ title }}
        </option>
      </select>
    </div>

    <div class='form-control'>
      <h2>What are you interested in?</h2>
      <div v-for="(value, key) in checkBoxes" :key="value.id">
        <input
            v-model="form.interest"
            :id="value.id"
            type="checkbox"
            :value="key"
        />
        <label :for="value.id">{{ value.title }}</label>
      </div>
    </div>

    <div class='form-control'>
      <h2>How do you learn?</h2>
      <div v-for="(value, key) in radioButtons" :key="value.id">
        <input
            v-model="form.how"
            :id="value.id"
            type="radio"
            :value="key"
        />
        <label for="value.id">{{ value.title }}</label>
      </div>
    </div>

    <div class="form-control">
      <h2>Your Rating?</h2>
      <rating-control v-model="form.rating"></rating-control>
    </div>

    <div class="form-control">
      <input type="checkbox" id="confirm-terms" v-model="form.confirm">
      <label for="confirm-terms">Agree to EULA?</label>
    </div>

    <div>
      <button>Save Data</button>
    </div>

  </form>
</template>


<script>
import RatingControl from "@/components/RatingControl"

export default {
  components: {RatingControl},
  data() {
    return {
      dropDowns: {
        google: 'Google',
        wom: 'Word of mouth',
        newspaper: 'Newspaper'
      },
      checkBoxes: {
        news: { id: 'interest-news', title: 'News' },
        tutorials: { id: 'interest-tutorials', title: 'Tutorials' },
        nothing: { id: 'interest-nothing', title: 'Nothing' }
      },
      radioButtons: {
        video: { id: 'how-video', title: 'Video Courses' },
        blogs: { id: 'how-blogs', title: 'Blogs' },
        other: { id: 'how-other', title: 'Other' }
      },
      form: {
        ...this.formDefaults()
      }
    }
  },
  methods: {
    submitForm() {
      this.form = {...this.formDefaults()}
    },
    formDefaults() {
      return {
        userName: '',
        userAge: null,
        referer: null,
        interest: [],
        how: null,
        rating: null,
        confirm: false,
        userNameValid: 'pending'
      }
    },
    validateInput() {
      if (this.form.userName === '') this.form.userNameValid = 'invalid'
      else this.form.userNameValid = 'valid'
    }
  }
};
</script>

<style scoped>
form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #ffffff;
}

.form-control {
  margin: 0.5rem 0;
}

label {
  font-weight: bold;
}

h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}

h6 {
  margin: 3px;
}

input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

.invalid input {
  border-color: red;
}

.invalid label {
  color: red;
}

button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  padding: 0.75rem 2rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}
</style>