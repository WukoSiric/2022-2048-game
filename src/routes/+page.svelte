<script lang="ts">
    import Modal from './Modal.svelte';
    import Board from './Board.svelte';
    import Footer from './Footer.svelte';
    import Controls from './Controls.svelte';
    import { Direction } from './types/Direction';
    import { trigger_keypress } from './Keypress/trigger_keypress'

    let board: Board
    let controls: Controls
    let tiles: number[][]
    let has_lost: boolean
    let has_won: boolean

</script>

<!-- HTML START -->
<svelte:head>
    <meta charset="utf-8">
    <title>2048 Clone</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;700&display=swap" rel="stylesheet" defer>
</svelte:head>

<!-- <button on:click={board.fill_all}>Put near finish</button> -->
<Modal message="Out of moves!" show_modal={has_lost} on:click={() => board.start_game(tiles)}/>
<Modal message="Nice job!" show_modal={has_won} on:click={() => board.start_game(tiles)}/>

<div class="content">
    <div class="header">
        <h1>2048</h1> 
        <p>Clone of the sliding tile puzzle video game by Gabriele Cirulli.</p>
    </div>
    <Board bind:tiles bind:has_lost bind:has_won bind:this={board}/>
    <Controls 
        on:up={() => board.execute_keydown(trigger_keypress(Direction.Up))}
        on:down={() => board.execute_keydown(trigger_keypress(Direction.Down))}
        on:left={() => board.execute_keydown(trigger_keypress(Direction.Left))}
        on:right={() => board.execute_keydown(trigger_keypress(Direction.Right))}
    />
    <Footer --color="black" />
</div>

<!-- STYLE -->
<style> 
    :global(body) {
        padding: 0;
        border: 0;
        margin: 0;
    }

    :global(h1) {
        margin: 0;
        padding: 0;
    }

    :global(p) {
        margin: 0;
        padding: 0;
    }

    .content {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 15px;
        font-family: Inter;
        gap: 30px;
    }

    
    .header {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    .header h1 {
        font-size: 4em;
        text-align: center;
    }

    .header p {
        font-weight: 400;
        text-align: center;
    }

</style>