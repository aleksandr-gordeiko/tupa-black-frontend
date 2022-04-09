<script lang="ts">
  import 'smelte/src/tailwind.css';
  import { Button, TextField } from 'smelte';

  let widthError: string = '';
  let heightError: string = '';
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

    const url = 'https://black.simpatiya.ga/api';

    fetch(url, requestOptions)
      .then((t) => t.blob().then((b) => {
        const a = document.createElement('a');
        a.href = URL.createObjectURL(b);
        a.setAttribute('download', `${width}x${height}`);
        a.click();
      }))
      .catch((err) => console.log('error', err));
  };

  const onGetPngClick = () => {
    if (width > 4096 || width < 12) widthError = 'The width must be within 12:4096 range'; else widthError = '';
    if (height > 4096 || height < 12) heightError = 'The height must be within 12:4096 range'; else heightError = '';
    if (widthError === '' && heightError === '') getPng();
  };
</script>

<main>
    <div class="main-wrapper">
        <TextField outlined label="Width" type="number" bind:value={width} bind:error={widthError}/>
        <TextField outlined label="Height" type="number" bind:value={height} bind:error={heightError}/>
        <Button block color="black" on:click={onGetPngClick}>Get {width} x {height} black png!</Button>
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
