<template>
  <div class="word-counter-container">
    <div class="inner-container">
      <h1 class="title">Word Counter</h1>
      <form @submit.prevent="countWords" class="form">
        <div class="input-group">
          <div for="word-input" class="input-label" @click.prevent>Enter your text:</div>
          <textarea
            id="word-input"
            v-model="text"
            class="custom-textarea"
            placeholder="Type or paste your text here..."
          />
        </div>
        <button
          type="submit"
          class="count-button"
        >
          Count Words
        </button>
      </form>
      <p
        id="word-count"
        class="word-count"
      >
        <span v-if="wordCount !== 0">
          {{ wordCount }} {{ wordCount === 1 ? 'word' : 'words' }}
        </span>
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const text = ref('');
const wordCount = ref(0);

const countWords = () => {
  const trimmedText = text.value.trim();
  const words = trimmedText === '' ? [] : trimmedText.split(/\s+/);
  wordCount.value = words.length;
};
</script>

<style lang="scss" scoped>
$round: 0.375rem;
$shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);

.word-counter-container {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;

  .inner-container {
    width: 100%;
    max-width: 100vw;
    padding: 2rem;
    background-color: white;
    border-radius: $round;
    box-shadow: $shadow-md;
    display: flex;
    flex-direction: column;
    gap: 1rem;

    .title {
      font-size: 1.5rem;
      line-height: 2rem;
      font-weight: 700;
      text-align: center;
      color: var(--color-gray-bold);
    }

    .form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    .input-group {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;

      .input-label {
        font-size: 0.875rem;
        line-height: 1.25rem;
        font-weight: 500;
        color: var(--color-gray-medium);
      }

      .custom-textarea {
        height: 10rem;
        padding: 0.75rem;
        color: var(--color-gray-medium);
        background-color: #f3f4f6;
        border-radius: $round;
        border: none;
        resize: vertical;
        transition: all 0.2s;

        &:focus {
          outline: none;
          background-color: white;
          box-shadow: 0 0 0 2px var(--color-primary);
        }
      }
    }

    .count-button {
      width: 100%;
      padding: 0.75rem 1.5rem;
      background-color: var(--color-primary);
      color: white;
      border: none;
      border-radius: $round;
      font-size: 1rem;
      font-weight: 500;
      cursor: pointer;
      transition: background-color 0.2s;

      &:hover {
        background-color: var(--color-secondary);
      }

      &:focus {
        outline: none;
        box-shadow: 0 0 0 2px var(--color-primary), 0 0 0 4px rgba(var(--color-primary), 0.5);
      }
    }

    .word-count {
      font-size: 1.125rem;
      line-height: 1.75rem;
      font-weight: 600;
      height: 1.75rem;
      text-align: center;
      color: var(--color-gray-medium);
      margin: 0;
    }
  }
}

@media (min-width: 768px) {
  .word-counter-container {
    .inner-container {
      max-width: 40rem;
    }
  }
}
</style>
