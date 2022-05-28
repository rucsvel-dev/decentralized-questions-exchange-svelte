<script>
  export let question;
</script>

    <div>
        <div>question id: {question?.questionId}</div>
        <div>
          title: {question?.questionTitle}, is proved: {String(question?.isProved)}
        </div>
        <div>description: {question?.questionDescription}</div>
      </div>
