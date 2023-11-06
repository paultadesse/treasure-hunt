<template>
  <ModalHint :show="showModal">
    <div>
      <h1 class="font-bold text-2xl">Title</h1>
      <p class="py-4">
        Type <span class="font-bold">correct</span> thats the answer
        <br /><br />
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Repellat in hic
        accusamus ab sit cupiditate? Accusamus, maxime libero iste optio tenetur
        distinctio odit, error facere eaque eligendi itaque adipisci explicabo!
      </p>
      <button
        class="bg-slate-600 text-white text-sm py-2 px-4 rounded-full"
        @click="showModal = false"
      >
        close
      </button>
    </div>
  </ModalHint>
  <div class="bg-slate-700 h-screen">
    <div class="py-12">
      <p
        class="uppercase tracking-wider text-center text-white font-bold text-xl"
      >
        quest name
      </p>
      <p
        class="uppercase tracking-wider text-center text-white font-bold text-4xl py-4"
      >
        {{ active_question.mission_name }} ({{
          given_data.findIndex(
            (mission) => mission.mission_name == active_question.mission_name
          ) + 1
        }}
        / {{ given_data.length }})
      </p>
      <div class="pt-4">
        <QuestionCard
          :question="active_question.question"
          :content="active_question.content"
          :answer="active_question.answer"
          @correct-answer-given="setNextQuestion"
          @show-hint="showModal = true"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
var showModal = ref(false);
var given_data = [
  {
    mission_name: "dead reckoning",
    question: "who are you ?",
    content:
      "Cont - 1, I can hear the notification sound but there is none banner. Also ... Notifications > Allow notifications when mirroring or sharing the display.This page can help out with checking on the Notifications settings",
    answer: "correct",
  },
  {
    mission_name: "Fallout",
    question: "who are you ?",
    content:
      "Cont - 2, I can hear the notification sound but there is none banner. Also ... Notifications > Allow notifications when mirroring or sharing the display.This page can help out with checking on the Notifications settings",
    answer: "correct",
  },
  {
    mission_name: "ghost protocol",
    question: "who are you ?",
    content:
      "Cont - 3, I can hear the notification sound but there is none banner. Also ... Notifications > Allow notifications when mirroring or sharing the display.This page can help out with checking on the Notifications settings",
    answer: "correct",
  },
  {
    mission_name: "rogue nation",
    question: "who are you ?",
    content:
      "Cont -4, I can hear the notification sound but there is none banner. Also ... Notifications > Allow notifications when mirroring or sharing the display.This page can help out with checking on the Notifications settings",
    answer: "correct",
  },
];

var active_index = ref(0);
var active_question = ref(given_data[active_index.value]);

function setNextQuestion() {
  if (active_index.value + 1 == given_data.length) return;
  active_question.value = given_data[++active_index.value];
}
</script>
