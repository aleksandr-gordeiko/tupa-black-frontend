<script lang="ts">
  import 'smelte/src/tailwind.css';
  import { Button, TextField } from 'smelte';

  let width: number = 1024;
  let height: number = 768;
</script>

<main>
    <div class="main-wrapper">
        <TextField outlined label="Width" type="number" min="12" max="4096" bind:value={width}/>
        <TextField outlined label="Height" type="number" min="12" max="4096" bind:value={height}/>
        <Button block color="black">Get {width} x {height} black png!</Button>
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
