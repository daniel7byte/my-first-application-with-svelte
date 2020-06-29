<script>
    export let idAnswer = '';
    
    const fetchAnswer = (async () => {
        const response = await fetch(`http://localhost:1337/answers/${idAnswer}`)
        return response.json()
    })()

    const vote = async () => {

        let votesCurrent = 0;

        const answer = await fetchAnswer.then((data) => {
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
        .then(data => console.log(data))
    }
</script>

<style>
    button {
        background-color: #4caf50;
        color: white;
        border-radius: 6px;
    }
    button:active {
        background-color: #1b5e20;
    }
</style>

<button on:click={vote}>+1</button>