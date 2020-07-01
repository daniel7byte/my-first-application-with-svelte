<script>
    export let idAnswer, votes, content;

    let disabled = false;

    const vote = async () => {

        console.time("Voto")

        disabled = true;

        votes++;

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
            disabled = false;
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
    button:disabled {
        background-color: #F44336;
    }
</style>

<span>{votes}</span>
{content}
<button {disabled} on:click={vote}>+1</button>