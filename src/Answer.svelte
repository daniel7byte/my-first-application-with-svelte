<script>
    export let idAnswer, votes, content;

    const handleInput = (event) => {
        console.time("Voto")
        vote(idAnswer)
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
            votes = data.votes
            console.timeEnd("Voto")
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

<span>{votes}</span>
{content}
<button on:click={handleInput}>+1</button>