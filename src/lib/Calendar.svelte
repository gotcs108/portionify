<script>
  let items = [];
  items[0] = [
    {name:"water", percentage:"30%"},
    undefined,
    {name:"popcorn", percentage:"30%"},
  ];

  let selectedTime = {date: undefined, hour: undefined};

  let isOpenModal = false;
  const openModal = () => {
    isOpenModal = true;
  }
  const openRequest = (date, hour) => {
    openModal();
    selectedTime.date = date;
    selectedTime.hour = hour;
  };

  const updateTable = (data) => {
    const selectedItem = data.detail.selectedItem;
    const date = selectedTime.date;
    const hour = selectedTime.hour;
    if (!items[date]){
      items[date] = [];
    }
    items[date][hour] = selectedItem;
  }
  import Modal from './Modal.svelte';
</script>
<Modal isOpenModal={isOpenModal} on:closeModal={(data)=>isOpenModal=data.detail.isOpenModal} on:reservation={updateTable}/>
{isOpenModal}

<table class="timetable">
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
            {items[d]?.[h] ? `${items[d]?.[h].name} (${items[d]?.[h].percentage}%)` : 'click to add details'}
          </button>
        </td>
      {/each}
    </tr>
  {/each}
</table>


<style>
  table, tr, td {
    border: 1px solid;
  }
</style>
