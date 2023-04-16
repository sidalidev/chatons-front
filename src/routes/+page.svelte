<script >
    let email = ''
    let password = ''
    let chatons = []
    let HOST = 'https://chatons.fly.dev'

     function login() {
        fetch(HOST+'/login', {
            method: 'POST', // ver
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                user: {
                    email,
                    password
                }
            })
        })
        .then(res => res.json())
        .then(data => {
            console.log(data.jwt)
            localStorage.setItem('jwt', data.jwt)
        })
    }

    function show_cats() {
        fetch(HOST+'/cats',{
            headers: {
                authorization: 'Bearer ' + localStorage.getItem('jwt')
            }
        }
        )
        .then(res => res.json())
        .then(data => {
            chatons = data
        })
    }
</script>

<button on:click={show_cats}>Afficher les chatons</button>

{#each chatons as chaton }
<p>{chaton.name}</p>
{/each}

<h1>Connexion</h1>

<input type="text" bind:value={email} placeholder="Email">
<input type="password" bind:value={password} placeholder="Mot de passe">

<button on:click={login}>Se connecter</button>

<style>
    * {
        font-family: sans-serif;
    }

    button {
        display: block;
        margin: 10px 0;
        border-radius: 5px;
        border: 1px solid #ccc;
        padding: 10px;
        color: white;
        background: peru;
    }

    input {
        display: block;
        margin: 10px 0;
        border-radius: 5px;
        border: 1px solid #ccc;
        padding: 10px;
    }

</style>