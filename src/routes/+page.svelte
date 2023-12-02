<script>
  import axios from "axios";
  import { goto } from "$app/navigation";

  let email = "";
  let password = "";

  let HOST = "https://chatons.sidali.dev";

  function login() {
    axios
      .post(HOST + "/login", {
        user: {
          email,
          password,
        },
      })
      .then((res) => {
        console.log('hey', res);
        localStorage.setItem("token", res.data.jwt);
        goto("/chatons");
      })
      .catch((err) => {
        alert("Erreur de connexion");
      });
  }
</script>

<h1>🐱 Connexion</h1>

<form class="input-group" on:submit|preventDefault={login}>
  <input type="text" bind:value={email} placeholder="Email" />
  <input type="password" bind:value={password} placeholder="Mot de passe" />
  <button >Se connecter</button>
</form>

<style>
  h1 {
    text-align: center;
    color: #333;
  }

  .input-group {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
  }

  input {
    width: 80%;
    margin-bottom: 15px;
    padding: 10px;
    border: 2px solid #ddd;
    border-radius: 8px;
    font-size: 16px;
  }

  button {
    width: 85%;
    padding: 10px;
    border: none;
    border-radius: 8px;
    background-color: #ff6f61;
    color: white;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  button:hover {
    background-color: #ff9570;
  }

  * {
    font-family: 'Arial', sans-serif;
  }
</style>
