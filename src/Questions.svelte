<script>
    import VoteBtn from './VoteBtn.svelte'

	const fetchQuestions = (async () => {
        const response = await fetch('http://localhost:1337/questions')
        return response.json()
    })()
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto');

    * {
        font-family: 'Roboto', sans-serif;
    }
    span {
        color:#f44336;
    }
</style>

<h1>Questions</h1>

{#await fetchQuestions}
	<p>...waiting</p>
{:then questions}
    <ul>
	{#each questions as question}
        <li>
            {question.title}
        </li>
         <ul>
        {#each question.answers as answer}
            <li>
                <span>({answer.votes})</span> {answer.content} <VoteBtn idAnswer={answer._id} />
            </li>    
        {/each}
        </ul>
    {/each}
    </ul>
{:catch error}
	<p>An error occurred!</p>
{/await}