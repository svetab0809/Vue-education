<script>

import { reactive, computed, defineComponent } from 'vue';
import axios from "axios";
import UButton from "@/components/UButton.vue";
import UFile from "@/components/global/UFile.vue";

export default defineComponent( {

  name: 'ReviewForm',
  components: {UFile, UButton},

  setup() {
    const review = reactive({
      author: '',
      stars: null,
      text: '',
      photo: null,
      isRecommended: true
    })

    const stars = [1,2,3,4,5]

    const submit = () => {
      console.log('submit')

      axios.post('/api/review', review, {
        headers: {
          'Content-Type': 'multipart/form-data'
        }
      })
          .then((res) => {
            console.log(res)
          })
          .catch((err) => {
            console.log(err)
          })
          .finally(() => {
            console.log('End!')
          })
    }

    return {
      review,
      stars,
      submit
    }
  }
})


</script>

<template>
  <form
      @submit.prevent.stop="submit"
      class="container pt-5 pb-5"
  >

    <UInput
        v-model = "review.author"
        placeholder="What is your name?"
    />

    <UInput
        type="textarea"
        v-model = "review.text"
        placeholder="What do you like or not like?"
    />


    <h4>Rating</h4>

    <div
        v-for="star in stars"
        :key = "star"
        class="form-check">
      <input
          class="form-check-input"
          type="checkbox"
          v-model="review.stars"
          :true-value="star"
          :false-value="null"
          value=""
          :id="`star$ {star}`">

      <label class="form-check-label" :for="`star$ {star}`">
        {{star}}
      </label>
    </div>

    <UFile
    v-model="review.photo"
    label="Photo"
    model-value="Array"
    />



    <div class="form-check">
      <input
          class="form-check-input"
          type="radio"
          id="adv1"
          v-model="review.isRecommended"
          value="true"
      >
      <label class="form-check-label" for="adv1">
        I recommend
      </label>
    </div>
    <div class="form-check">
      <input
          class="form-check-input"
          type="radio"
          id="adv2"
          v-model="review.isRecommended"
          value="false"
      >
      <label class="form-check-label" for="adv2">
        I don't recommend it
      </label>
    </div>

    <UButton>
      Send
    </UButton>
  </form>
</template>