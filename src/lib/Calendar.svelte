<script>
  let items = [];
  items[0] = [
    {name:"water", percentage:"30%"},
    undefined,
    {name:"popcorn", percentage:"30%"},
  ];

  let selectedTime = {date: undefined, hour: undefined};

  let isOpenModal = false;
  let openModal = () => {
    isOpenModal = true;
  }
  let openRequest = (date, hour) => {
    openModal();
    selectedTime.date = date;
    selectedTime.hour = hour;
  };
  import Modal from './Modal.svelte';
</script>
<Modal isOpenModal={isOpenModal} on:closeModal={(openState)=>isOpenModal=openState.detail.isOpenModal}/>
{isOpenModal}

<table>
  <tr>
    <td></td>
    <td>Sun 2/20</td>
    <td>Mon 2/21</td>
    <td>Tue 2/22</td>
    <td>Wed 2/23</td>
    <td>Thu 2/24</td>
    <td>Fri 2/25</td>
    <td>Sat 2/26</td>
  </tr>
  {#each Array(24) as _, h}
    <tr>
      <td>{h}:00</td>
      {#each Array(7) as _, d}
        <td>
          <button on:click={() => openRequest(d,h)}>
            {items[d]?.[h] ? `${items[d]?.[h].name} (${items[d]?.[h].percentage})` : 'click to add details'}
          </button>
        </td>
      {/each}
    </tr>
  {/each}
</table>


<style>
</style>
