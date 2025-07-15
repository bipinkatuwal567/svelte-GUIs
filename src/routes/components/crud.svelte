<script lang="ts">
  type Person = {
    name: string;
    surname: string;
  };

  let persons: Person[] = $state([
    {
      name: "Evan",
      surname: "You",
    },
    {
      name: "Rich",
      surname: "Harris",
    },
    {
      name: "Ryan",
      surname: "Carniato",
    },
  ]);

  let selected = $state<Person>();
  let person = $state({ name: "", surname: "" });
  let prefix = $state("");
  let filteredPerson = $derived(
    prefix
      ? persons.filter((p) => p.surname.toLowerCase().startsWith(prefix))
      : persons
  );

  $effect(() => {
    person = {
      name: selected?.name || "",
      surname: selected?.surname || "",
    };
  });

  function CreatePerson() {
    persons.push(person);
    clearInputs();
  }

  function UpdatePerson() {
    const findIndex = persons.indexOf(selected!);
    persons[findIndex] = {
      name: person.name,
      surname: person.surname,
    };
    clearInputs();
  }

  function DeletePerson() {
    persons = persons.filter(
      (p) => p.name !== person?.name || p.surname !== person?.surname
    );
    clearInputs();
  }

  function clearInputs() {
    person = { name: "", surname: "" };
  }
</script>

<div class="container">
  <div class="prefix">
    <label>Filter prefix: <input type="text" bind:value={prefix} /></label>
  </div>

  <div class="mid-container">
    <select class="select-container" bind:value={selected} size="5">
      {#each filteredPerson as person}
        <option value={person}>{person.surname}, {person.name}</option>
      {/each}
    </select>

    <div class="input-container">
      <label>
        Name:
        <input type="text" bind:value={person.name} />
      </label>
      <label>
        Surname:
        <input type="text" bind:value={person.surname} />
      </label>
    </div>
  </div>

  <div class="button-container">
    <button onclick={CreatePerson}>Create</button>
    <button onclick={UpdatePerson}>Update</button>
    <button onclick={DeletePerson}>Delete</button>
  </div>
</div>

<style>
  .container {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    color: white;
    width: 500px;
    font-size: 18px;
    background: #4b5e8f;
    padding: 1rem;
    border-radius: 1rem;
  }

  .prefix {
    width: 50%;
    label {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    input {
      outline: none;
      border: none;
      font-size: 16px;
      border-radius: 0.2rem;
      width: 50%;
      padding: 0.4rem 0.3rem;
      height: 100%;
    }
  }

  .mid-container {
    display: flex;
    justify-content: space-between;
    gap: 1rem;

    .select-container {
      width: 50%;
      font-size: 16px;
      background: #555454;
      color: white;
      padding: 0.5rem;
    }

    .input-container {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
      width: 50%;

      label {
        display: flex;
        gap: 0.5rem;
        justify-content: space-between;

        input {
          outline: none;
          border: none;
          font-size: 16px;
          border-radius: 0.2rem;
          width: 50%;
          padding: 0.4rem 0.3rem;
        }
      }
    }
  }

  .button-container {
    display: flex;
    gap: 2rem;
  }
</style>
