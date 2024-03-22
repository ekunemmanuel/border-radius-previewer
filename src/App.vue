<template>
  <div class="bg-[#282828] grid place-items-center min-h-screen">
    <div class="max-w-[600px] w-full space-y-4">
      <h1 class="text-white text-[40px] text-center">
        Border Radius Previewer
      </h1>
      <div class="flex gap-4 w-full justify-between flex-1">
        <div class="">
          <label for="tl">Top Left</label>
          <input
            type="text"
            class="w-full"
            v-model="borderRadius.tl"
            @blur="checkValue('tl')"
            @input="validateInput('tl')"
            name="tl"
            id="tl"
          />
        </div>
        <div class="">
          <label for="tr">Top Right</label>
          <input
            type="text"
            class="w-full"
            v-model="borderRadius.tr"
            @blur="checkValue('tr')"
            @input="validateInput('tr')"
            name="tr"
            id="tr"
          />
        </div>
        <div class="">
          <label for="bl">Bottom Left</label>
          <input
            type="text"
            class="w-full"
            v-model="borderRadius.bl"
            @blur="checkValue('bl')"
            @input="validateInput('bl')"
            name="bl"
            id="bl"
          />
        </div>
        <div class="">
          <label for="br">Bottom Right</label>
          <input
            type="text"
            class="w-full"
            v-model="borderRadius.br"
            @blur="checkValue('br')"
            @input="validateInput('br')"
            name="br"
            id="br"
          />
        </div>
      </div>
      <div
        class="bg-black w-full min-h-[400px] text-white grid place-items-center"
        :style="dynamicStyle"
      >
        <code>
          {{ snippet }}
        </code>
      </div>
      <div class="space-x-2 flex justify-center items-center text-white">
        <span class="hover:text-[#7b7a7a] duration-200">
          <a href="https://github.com/ekunemmanuel/border-radius-previewer" target="_blank">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="35"
              height="35"
              viewBox="0 0 24 24"
            >
              <path
                fill="currentColor"
                d="M12 2A10 10 0 0 0 2 12c0 4.42 2.87 8.17 6.84 9.5c.5.08.66-.23.66-.5v-1.69c-2.77.6-3.36-1.34-3.36-1.34c-.46-1.16-1.11-1.47-1.11-1.47c-.91-.62.07-.6.07-.6c1 .07 1.53 1.03 1.53 1.03c.87 1.52 2.34 1.07 2.91.83c.09-.65.35-1.09.63-1.34c-2.22-.25-4.55-1.11-4.55-4.92c0-1.11.38-2 1.03-2.71c-.1-.25-.45-1.29.1-2.64c0 0 .84-.27 2.75 1.02c.79-.22 1.65-.33 2.5-.33c.85 0 1.71.11 2.5.33c1.91-1.29 2.75-1.02 2.75-1.02c.55 1.35.2 2.39.1 2.64c.65.71 1.03 1.6 1.03 2.71c0 3.82-2.34 4.66-4.57 4.91c.36.31.69.92.69 1.85V21c0 .27.16.59.67.5C19.14 20.16 22 16.42 22 12A10 10 0 0 0 12 2"
              ></path></svg
          ></a>
        </span>
        <span class="hover:text-[#7b7a7a] duration-200">
          <a href="https://emmanuelapabiekun.vercel.app/app-ideas" target="_blank">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="35"
              height="35"
              viewBox="0 0 24 24"
            >
              <path
                fill="currentColor"
                d="M12 12q-1.65 0-2.825-1.175T8 8q0-1.65 1.175-2.825T12 4q1.65 0 2.825 1.175T16 8q0 1.65-1.175 2.825T12 12m-8 8v-2.8q0-.85.438-1.562T5.6 14.55q1.55-.775 3.15-1.162T12 13q1.65 0 3.25.388t3.15 1.162q.725.375 1.163 1.088T20 17.2V20z"
              /></svg
          ></a>
        </span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, watch, ref } from "vue";

const dynamicStyle = reactive({ borderRadius: "0px 0px 0px 0px" });
const borderRadius = reactive({ tl: "0", tr: "0", bl: "0", br: "0" });
const snippet = ref({
  "border-radius": `${borderRadius.tl}px ${borderRadius.tr}px ${borderRadius.br}px ${borderRadius.bl}px`,
});

// watch for changes on the dom
watch(borderRadius, ({ tl, tr, bl, br }) => {
  dynamicStyle.borderRadius = `${tl}px ${tr}px ${br}px ${bl}px`;

  snippet.value = {
    "border-radius": `${tl}px ${tr}px ${br}px ${bl}px`,
  };
});

// check if the input is empty
const checkValue = (key: keyof typeof borderRadius) => {
  if (borderRadius[key] === "") {
    borderRadius[key] = "0";
  }
};

// make sure the input is a number
const validateInput = (key: keyof typeof borderRadius) => {
  borderRadius[key] = borderRadius[key].replace(/\D/g, "");
};
</script>

<style scoped>
input {
  background-color: #282828;
  color: white;
  border: 1px solid white;
  padding: 0.5rem;
}
label {
  color: white;
}
</style>
