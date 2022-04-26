<script>
  import { createEventDispatcher } from "svelte";

  // we cannot use event forwarding
  // bcz it doesnt send the data
  let dispatch = createEventDispatcher();

  let name;
  let color;
  let age;

  let skills = [];

  const handleSubmit = () => {
    const person = {
      name, 
      color, 
      age,
      skills,
      id: Math.random(), 
    };

    dispatch('addPerson', person);
  };
</script>

<!-- submit event autmatically bind to any button in the form -->
<!-- if not prevdef, page refresh, bcz that is the default action -->
<form on:submit|preventDefault={handleSubmit}>
  <input type="text" placeholder="name" bind:value={name} />
  <input type="number" placeholder="age" bind:value={age} />

  <label>Skills:</label>
  <input type="checkbox" bind:group={skills} value="fighting" />fighting<br />
  <input type="checkbox" bind:group={skills} value="sneaking" />sneaking<br />
  <input type="checkbox" bind:group={skills} value="running" />running<br />

  <label>Belt color:</label>
  <select bind:value={color}>
    <option value="black">black</option>
    <option value="orange">orange</option>
    <option value="brown">brown</option>
    <option value="white">white</option>
  </select>

  <br />
  <button>Add person</button>
</form>

<style>
</style>
