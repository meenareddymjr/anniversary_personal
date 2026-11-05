<script setup>
import { ref } from 'vue'
import { content } from './content'
import LoveQuiz from './components/LoveQuiz.vue'
const letterOpen = ref(false)
</script>

<template>
  <header class="nav"><a class="brand" href="#home">you & me<span> / since 2016</span></a>
    <nav aria-label="Main navigation"><a href="#memories">Our moments</a><a href="#quiz">Our quiz</a><a href="#letter">A
        little letter <span>↗</span></a></nav>
  </header>
  <main>
    <section class="hero" id="home">
      <div class="hero-copy">
        <p class="eyebrow"><span class="line"></span> A LITTLE SOMETHING, JUST FOR YOU</p>
        <h1>A decade<br>of <em>us.</em><span class="star">✧</span></h1>
        <p class="dedication">For {{ content.name }}. My {{ content.nickname }}.<br>{{ content.dedication }}</p><a
          class="primary" href="#memories">Take a walk down memory lane <span>↗</span></a>
        <p class="edition">06.11.2016 — 06.11.2026 <span>•</span> OUR FIRST TEN YEARS</p>
      </div>
      <div class="hero-art">
        <div class="orbit"></div><span class="small-star">✧</span>
        <div class="photo-frame"><img v-if="content.heroPhoto" :src="content.heroPhoto" alt="Our favourite photograph">
          <div v-else class="photo-placeholder"><svg viewBox="0 0 300 350" aria-hidden="true">
              <circle cx="150" cy="112" r="59" fill="#d2ad82" />
              <path d="M0 238 Q90 159 164 242 T300 209 V350 H0Z" fill="#686c53" />
              <path d="M0 283 Q91 216 190 292 T300 260 V350 H0Z" fill="#343e32" />
              <path d="M101 299q-10-56 9-77q15-17 28 1l13 29 13-29q15-17 27 0q14 27 6 76" fill="#202b26" />
              <circle cx="122" cy="205" r="13" fill="#202b26" />
              <circle cx="178" cy="205" r="13" fill="#202b26" />
            </svg><span>YOUR FAVOURITE PHOTO HERE</span></div>
          <div class="photo-note">my favourite place is beside you.</div>
        </div><span class="handwritten">ten years, still you ♡</span><span class="vertical-note">A LOVE STORY, STILL
          BEING WRITTEN</span>
      </div>
      <div class="hero-bottom"><span>01 / THE BEGINNING</span><a href="#memories">SCROLL TO REMEMBER ↓</a><span>A
          FOREVER KIND OF THING ♡</span></div>
    </section>
    <section class="memories section" id="memories">
      <div class="section-heading">
        <div>
          <p class="eyebrow">THE MOMENTS THAT MADE US</p>
          <h2>Little moments.<br><em>A whole lot of love.</em></h2>
        </div>
        <p>Some memories never get old.<br>These are a few of ours.</p>
      </div>
      <div class="memory-grid">
        <article v-for="(memory, index) in content.memories" :key="index" class="memory">
          <div class="memory-photo"><img v-if="memory.photo" :src="memory.photo" :alt="memory.title">
            <div v-else class="empty-photo"><span>♡</span>
              <p>A memory belongs here</p>
            </div><span class="memory-number">0{{ index + 1 }}</span>
          </div>
          <h3>{{ memory.title }}</h3>
          <p>{{ memory.caption }}</p>
        </article>
      </div>
    </section>
    <LoveQuiz :questions="content.quiz" />
    <section class="letter-section section" id="letter">
      <p class="eyebrow">SOME WORDS, FROM MY HEART</p><span class="envelope" aria-hidden="true">♡</span>
      <h2>To my <em>{{ content.nickname }}.</em></h2>
      <p>There are a few things I want you to know.</p><button class="primary" @click="letterOpen = !letterOpen"
        :aria-expanded="letterOpen" aria-controls="love-letter">{{ letterOpen ? 'Close your letter' : 'Open your letter'
        }} <span>{{ letterOpen ? '−' : '↗' }}</span></button>
      <Transition name="letter">
        <div v-if="letterOpen" id="love-letter" class="letter-paper">
          <p>{{ content.letter }}</p><span class="handwritten">{{ content.signature }} ♡</span>
        </div>
      </Transition>
    </section>
    <footer><a class="brand" href="#home">vishnu & meena</a>
      <p>Ten years down. A lifetime to go.</p><span>{{ content.anniversary }} · ♡</span>
    </footer>
  </main>
</template>
