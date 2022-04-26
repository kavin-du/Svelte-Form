<script>
  import Modal from "./Modal.svelte";
  import AddPersonForm from "./AddPersonForm.svelte";

  let showModal = false;

  let people = [
    { id: 1, name: "first", color: "red" },
    { id: 2, name: "second", color: "blue" },
    { id: 3, name: "third", color: "green" },
  ];

  const handleDelete = (id) => {
    people = people.filter((person) => person.id !== id);
  };

  const toggleModal = () => {
    showModal = !showModal;
  };

	const addPersonHandler = (e) => {
		const person = e.detail;
		// cannot do people.push(person)
		// bcz we have to reassign in svelte

		people = [...people, person];
		showModal = false;
	}
</script>

<Modal {showModal} on:click={toggleModal}>
	<!-- custom event name then, handler name -->
	<AddPersonForm on:addPerson={addPersonHandler} />
</Modal>

<main>
  <button on:click|once={toggleModal}>Show modal</button>
  {#each people as p (p.id)}
    <div>
      <h4>{p.name}</h4>
      <p>favorite color is {p.color}</p>
      {#if p.color === "blue"}
        <p><strong>BLUE FAVORITE</strong></p>
      {/if}
      <button on:click={() => handleDelete(p.id)}>delete</button>
    </div>
  {:else}
    <p>all are empty</p>
  {/each}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
