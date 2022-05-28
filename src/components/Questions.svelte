<script>
  import { onMount } from 'svelte'
  import GUN from 'gun'
  import 'gun/axe';

  import Question from './Question.svelte';

  const db = GUN()

  let questionTitleInput = ''
  let questionDescriptionInput = ''
  let questions = []

  onMount(() => {
    db.get('questions')
      .map()
      .once(async (question, id) => {
        questions = [...questions, question]
      })
  })
console.log('===== updated')
  const createQuestion = async () => {
    db.get('questions').get(questionTitleInput).put({ isProved: false, questionId: questionTitleInput, questionDescriptionInput })
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
