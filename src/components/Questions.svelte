<script>
  import { onMount } from 'svelte'
  import { gun } from "../gun"

  import Question from './Question.svelte';

  let questionTitleInput = ''
  let questionDescriptionInput = ''
  let questions = []

  onMount(() => {
    gun.get('questions')
      .map()
      .once(async (question, id) => {
        questions = [...questions, question]
      })
  })

  const createQuestion = async () => {
    gun.get('questions').get(questionTitleInput).put({ isProved: false, questionId: questionTitleInput, questionDescriptionInput })
  }
</script>

<div class="container">
  <input
    type="text"
    placeholder="Question title"
    bind:value={questionTitleInput}/>
  <input
    type="text"
    placeholder="Question description"
    bind:value={questionDescriptionInput} />
  <button type="submit" on:click|preventDefault={createQuestion}>
    create question
  </button>
  <div>
    {#each questions as question (question?.questionId)}
      <Question {question} />
    {/each}
  </div>
</div>
