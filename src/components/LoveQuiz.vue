<script setup>
import { computed, nextTick, ref } from 'vue'
const props = defineProps({ questions: { type: Array, default: () => [] } })
const index = ref(0)
const selected = ref(null)
const score = ref(0)
const finished = ref(false)
const heading = ref(null)
const question = computed(() => props.questions[index.value])
const answered = computed(() => selected.value !== null)
const correct = computed(() => answered.value && selected.value === question.value.answer)
async function focusHeading() { await nextTick(); heading.value?.focus() }
function choose(option) {
  if (answered.value) return
  selected.value = option
  if (option === question.value.answer) score.value++
}
function next() {
  if (!answered.value) return
  if (index.value === props.questions.length - 1) finished.value = true
  else { index.value++; selected.value = null }
  focusHeading()
}
function restart() { index.value = 0; selected.value = null; score.value = 0; finished.value = false; focusHeading() }
</script>

<template>
  <section v-if="questions.length" id="quiz" class="quiz-section section">
    <p class="eyebrow">A LITTLE GAME, JUST FOR US</p>
    <h2>How well do you<br><em>remember us?</em></h2>
    <p class="quiz-intro">A few questions. A few smiles. A whole lot of us.</p>
    <div class="quiz-card">
      <template v-if="!finished">
        <div class="quiz-meta"><span>QUESTION {{ index + 1 }} OF {{ questions.length }}</span><span>♡</span></div>
        <progress :value="index + 1" :max="questions.length" :aria-label="`Question ${index + 1} of ${questions.length}`"></progress>
        <h3 ref="heading" tabindex="-1">{{ question.question }}</h3>
        <div class="quiz-options" role="group" :aria-label="question.question">
          <button v-for="(option, optionIndex) in question.options" :key="`${index}-${optionIndex}`" class="quiz-option" :class="{ 'is-selected': selected === optionIndex, 'is-correct': answered && optionIndex === question.answer, 'is-wrong': selected === optionIndex && !correct }" :disabled="answered" @click="choose(optionIndex)">
            <span class="option-letter">{{ String.fromCharCode(65 + optionIndex) }}</span><span>{{ option }}</span><span v-if="answered && optionIndex === question.answer" class="option-mark" aria-label="Correct answer">✓</span><span v-else-if="selected === optionIndex" class="option-mark" aria-label="Incorrect answer">×</span>
          </button>
        </div>
        <div class="quiz-feedback" role="status" aria-live="polite"><template v-if="answered"><strong>{{ correct ? 'You remembered! ♡' : 'A little reminder ♡' }}</strong><p v-if="!correct">The answer is: {{ question.options[question.answer] }}.</p><p>{{ question.note }}</p></template></div>
        <button class="primary" :disabled="!answered" @click="next">{{ index === questions.length - 1 ? 'See our result' : 'Next question' }} <span>↗</span></button>
      </template>
      <div v-else class="quiz-result">
        <span class="result-heart" aria-hidden="true">♡</span><h3 ref="heading" tabindex="-1">{{ score === questions.length ? 'You know our story by heart.' : 'Every memory is worth revisiting.' }}</h3>
        <p class="quiz-score">{{ score }} <span>/ {{ questions.length }}</span></p><p>Whatever the score, you are still my favourite person.</p>
        <button class="primary" @click="restart">Play again <span>↻</span></button>
      </div>
    </div>
  </section>
</template>
