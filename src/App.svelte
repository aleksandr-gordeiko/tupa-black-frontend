<script lang="ts">
  import 'smelte/src/tailwind.css';
  import { Button, TextField } from 'smelte';

  let width: number = 1024;
  let height: number = 768;

  const getPng = () => {
    const myHeaders = new Headers();
    myHeaders.append('Content-Type', 'application/x-www-form-urlencoded');

    const urlencoded = new URLSearchParams();
    urlencoded.append('width', String(width));
    urlencoded.append('height', String(height));

    // eslint-disable-next-line no-undef
    const requestOptions: RequestInit = {
      method: 'POST',
      headers: myHeaders,
      body: urlencoded,
      redirect: 'follow',
    };

    const url = 'http://black.simpatiya.ga/api';

    fetch(url, requestOptions)
      .then((t) => t.blob().then((b) => {
        const a = document.createElement('a');
        a.href = URL.createObjectURL(b);
        a.setAttribute('download', `${width}x${height}`);
        a.click();
      }))
      .catch((error) => console.log('error', error));
  };
</script>

<main>
    <div class="main-wrapper">
        <TextField outlined label="Width" type="number" min="12" max="4096" bind:value={width}/>
        <TextField outlined label="Height" type="number" min="12" max="4096" bind:value={height}/>
        <Button block color="black" on:click={getPng}>Get {width} x {height} black png!</Button>
    </div>
</main>

<style>
    .main-wrapper {
        width: 30em;
        position: absolute;
        top: 40%;
        left: 50%;
        margin: 0 -50% 0 0;
        transform: translate(-50%, -50%);
    }
</style>
