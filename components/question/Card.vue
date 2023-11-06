<template>
  <div class="w-1/2 mx-auto p-8" :class="statusClass">
    <div class="bg-slate-600 text-slate-400 p-8 rounded-lg">
      <div>
        <div>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6 float-right cursor-pointer"
            @click="exposeHint"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M11.25 11.25l.041-.02a.75.75 0 011.063.852l-.708 2.836a.75.75 0 001.063.853l.041-.021M21 12a9 9 0 11-18 0 9 9 0 0118 0zm-9-3.75h.008v.008H12V8.25z"
            />
          </svg>
        </div>
        <div>
          {{ content }}
        </div>
      </div>
      <div class="py-8">
        <p>Question: {{ question }}</p>
        <div class="py-4">
          <input
            type="text"
            class="p-4 border rounded-full bg-slate-600 w-full placeholder:uppercase placeholder:text-sm placeholder:tracking-wider"
            placeholder="your answer"
            v-model="user_answered"
          />
        </div>
      </div>
      <div>
        <button
          class="bg-slate-500 rounded-full text-white uppercase px-12 py-4 flex items-center space-x-3"
          @click="checkAnswer"
          v-if="question_status != 'answered'"
        >
          <span>{{ button_text }}</span>

          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
            v-if="question_status == 'pending'"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M4.5 12h15m0 0l-6.75-6.75M19.5 12l-6.75 6.75"
            />
          </svg>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
            v-else="question_status == 'failed'"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M18.364 18.364A9 9 0 005.636 5.636m12.728 12.728A9 9 0 015.636 5.636m12.728 12.728L5.636 5.636"
            />
          </svg>
        </button>

        <!-- show button that navigate to the next question -->

        <button
          class="bg-slate-500 rounded-full text-white uppercase px-12 py-4 flex items-center space-x-3"
          @click="navigateToNextQuestion"
          v-if="question_status == 'answered'"
        >
          <span>{{ button_text }}</span>

          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
            />
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>
<script setup>
defineProps({
  question: String,
  content: String,
  answer: String,
});

const emit = defineEmits(["correct-answer-given", "show-hint"]);

var button_text = ref("check answer");
var user_answered = ref(null);

/**
 * pending
 * answered
 * failed
 */
var question_status = ref("pending");

function checkAnswer() {
  // some logic goes here but for now this is enough
  if (user_answered.value == "correct") {
    button_text.value = "Continue";
    question_status.value = "answered";
  } else {
    button_text.value = "Retry";
    question_status.value = "failed";
  }
}

var statusClass = computed(() => ({
  "bg-green-500": question_status.value == "answered",
  "bg-red-500": question_status.value == "failed",
}));

function navigateToNextQuestion() {
  setSettingsToInitials();
  emit("correct-answer-given");
}

function exposeHint() {
  emit("show-hint");
}

function setSettingsToInitials() {
  button_text.value = "check answer";
  user_answered.value = null;
  question_status.value = "pending";
}
</script>
