<script>
  import { onMount } from "svelte";
  import axios from "axios";
  let chatons = [];

  onMount(() => {
    axios
      .get("https://chatons.sidali.dev/cats", {
        headers: {
          Authorization: "Bearer " + localStorage.getItem("token"),
        },
      })
      .then((res) => {
        chatons = res.data;
      });
  });
</script>

<style>
  .card-container {
    display: flex;
    flex-wrap: wrap;
  }

  .card {
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 16px;
    margin: 10px;
    width: 200px;
    text-align: center;
  }

  .card img {
    max-width: 100%;
    height: auto;
    border-radius: 50%;
  }

  .card p {
    margin: 4px 0;
  }
</style>

<div class="card-container">
  {#each chatons as chaton}
    <div class="card">
      <img src={chaton.image_url} alt={chaton.name} />
      <p><strong>{chaton.name}</strong></p>
      <p>Race: {chaton.race}</p>
      <p>Age: {chaton.age} ans</p>
    </div>
   {:else}
    <p>Pas de chatons 😿</p>
  {/each}
</div>
