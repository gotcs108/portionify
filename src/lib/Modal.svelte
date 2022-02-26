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
    let quantity = 0;

    let selectedItem;
    let apple = {name: "Apple", calories:30};
    let chocolate = {name: "Chocolate", calories:100};
    let paperTowel = {name: "Paper Towel", quantity:30};
    let toiletPaper = {name: "Toilet Paper", quantity:30};
</script>

<div class="background" style="--display: {isOpenModal ? 'block' : 'none'};" on:click={closeModal}></div>
<div class="modal" style="--display: {isOpenModal ? 'block' : 'none'};">
    <p>Split</p>
    <button on:click={() => tab = "food"}>Food</button>
    <button on:click={() => tab = "item"}>Item</button>
    <!-- If food -->
    <!-- List of food to select from with calories-->
    {#if tab==="food"}
        <p>Split food</p>
        <div>
            <button on:click={() => selectedItem = apple}>
                {apple.name}
                {apple.calories}cal
            </button>
            <button on:click={() => selectedItem = chocolate}>
                {chocolate.name}
                {chocolate.calories}cal
            </button>
        </div>

        <!-- TODO: cap it to 100 -->
        Split <input bind:value={percentage}>%

        <p>{selectedItem ? `You get ${selectedItem.calories*percentage*0.01}cal` : 'Please select a food'}</p>
        <button on:click={() => dispatch('reservation', { selectedItem: {type:'food', name: selectedItem.name, percentage} })}>
            Reserve
        </button>
    {/if}

    {#if tab==="item"}
        <p>Split item</p>
        <div>
            <button on:click={() => selectedItem = paperTowel}>
                {paperTowel.name}
                {paperTowel.quantity}#
            </button>
            <button on:click={() => selectedItem = toiletPaper}>
                {toiletPaper.name}
                {toiletPaper.quantity}#
            </button>
        </div>

        <!-- TODO: cap it to 100 -->
        Quantity <input bind:value={quantity}>

        <button on:click={() => dispatch('reservation', { selectedItem: {type:'item', name: selectedItem.name, quantity} })}>
            Reserve
        </button>
    {/if}
</div>

<style>
    button {
        border: 2px solid black;
        background-color: white;
        color: black;
        padding: 14px 28px;
    }
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