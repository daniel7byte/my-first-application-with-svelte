<script>
	const fetchQuestions = (async () => {
        const response = await fetch('http://localhost:1337/questions')
        return response.json()
    })()

    const handleInput = (event) => {
        console.time("Voto")
        let idAnswer = event.target.getAttribute('data-answer-id')
        vote(idAnswer)
        console.timeEnd("Voto")
    }

    const vote = async (idAnswer) => {

        let votesCurrent = 0;

        const fetchAnswer = await fetch(`http://localhost:1337/answers/${idAnswer}`)
                                .then(res => res.json())
                                .then((data) => {
                                    votesCurrent = data.votes
                                })

        await fetch(`http://localhost:1337/answers/${idAnswer}`, {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                votes: votesCurrent + 1
            })
        })
        .then(res => res.json())
        .then(data => {
            const span = document.getElementById(idAnswer)
            span.innerHTML = data.votes 
        })
    }
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto');

    * {
        font-family: 'Roboto', sans-serif;
    }
    span {
        color:#f44336;
        text-decoration-line: underline;
    }
    button {
        background-color: #4caf50;
        color: white;
        border-radius: 6px;
    }
    button:active {
        background-color: #1b5e20;
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
                <div>
                    <span id={answer._id}>{answer.votes}</span>
                    {answer.content}
                    <button data-answer-id={answer._id} on:click={handleInput}>+1</button>
                </div>

            </li>    
        {/each}
        </ul>
    {/each}
    </ul>
{:catch error}
	<p>An error occurred!</p>
{/await}