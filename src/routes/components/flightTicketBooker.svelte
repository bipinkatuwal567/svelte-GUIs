<script lang="ts">
  type Options = "one-way" | "return";

  function getDate() {
    const date = new Date();
    const [day, month, year] = date
      .toLocaleDateString("en-US", {
        year: "numeric",
        month: "2-digit",
        day: "2-digit",
      })
      .split("/");

    return `${year}-${month}-${day}`;
  }

  let selected = $state<Options>("one-way");
  let startDate = $state(getDate());
  let returnDate = $state(getDate());

  function handleSubmit(e: Event) {
    e.preventDefault();
    alert(`You have booked a ${selected} flight on ${startDate}`);
  }

  $inspect(selected, startDate, returnDate);
</script>

<div>
  <form onsubmit={handleSubmit}>
    <select bind:value={selected}>
      <option value="one-way">one way ticket</option>
      <option value="return">return ticket</option>
    </select>

    <label>
      <input type="date" bind:value={startDate} min={getDate()} required />
    </label>

    <label>
      <input
        type="date"
        bind:value={returnDate}
        min={getDate()}
        disabled={selected !== "return"}
        required
      />
    </label>

    <button
      type="submit"
      disabled={!startDate || (selected === "return" && returnDate < startDate)}
      >Book</button
    >
  </form>
</div>

<style>
  div {
    height: 100vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  form {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 0.5rem;
    max-width: 30rem;
  }

  select {
    padding: 0.4rem;
    border-radius: 0.2rem;
    outline: none;
    border: none;
    width: 100%;
  }

  input {
    padding: 0.4rem;
    border-radius: 0.2rem;
    width: 100%;
  }

  button {
    padding: 0.6rem;
    background-color: rgb(142, 255, 13);
    border-radius: 0.4rem;
    font-size: 0.8rem;
    width: 100%;
  }
</style>
