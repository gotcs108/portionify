<!-- src/Modal.svelte -->
<script>
    import { createEventDispatcher } from 'svelte';

    export let isOpenModal;
    const dispatch = createEventDispatcher();
    
    const closeModal = () => {
        isOpenModal = false;
        dispatch('closeModal', { isOpenModal });
    }

    let tab = "food";
    let percentage = 100;

    let selectedFood;
    let apple = {name: "Apple", calories:30};
    let chocolate = {name: "Chocolate", calories:100};
</script>

<div class="background" style="--display: {isOpenModal ? 'block' : 'none'};" on:click={closeModal}></div>
<div class="modal" style="--display: {isOpenModal ? 'block' : 'none'};">
    <p>Split from</p>
    <button>Food</button>
    <button>Item</button>
    <!-- If food -->
    <!-- List of food to select from with calories-->
    {#if tab==="food"}
    <div>
        <button on:click={() => selectedFood = apple}>
            {apple.name}
            {apple.calories}
        </button>
        <button on:click={() => selectedFood = chocolate}>
            {chocolate.name}
            {chocolate.calories}
        </button>
    </div>

    <!-- TODO: cap it to 100 -->
    Split <input bind:value={percentage}>%

    <p>{selectedFood ? `You get ${selectedFood.calories*percentage*0.01}cal` : 'Please select a food'}</p>
    {/if}
</div>

<style>
    .background {
        display: var(--display);
        position: fixed;
        z-index: 1;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
    }

    .modal {
        display: var(--display);
        position: fixed;
        z-index: 2;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: #fff;
        filter: drop-shadow(0 0 20px #333);
    }
</style>