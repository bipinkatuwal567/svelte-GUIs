<script>
  class Temperature {
    #c = $state(0);
    #f = $state(0);

    get c() {
      return this.#c;
    }

    set c(value) {
      this.#c = value;
      this.#f = this.#c * (9 / 5) + 32;
    }

    get f() {
      return this.#f;
    }

    set f(value) {
      this.#f = value;
      this.#c = (this.#f - 32) * (5 / 9);
    }
  }

  const temperature = new Temperature();
</script>

<div class="container">
  <input type="number" bind:value={temperature.c} />
  <p>Celcius</p>
  <p>=</p>
  <input type="number" bind:value={temperature.f} />
  <p>Fahrenheit</p>
</div>

<style>
  .container {
    margin-top: 15rem;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 0.5rem;
  }

  input {
    padding: 0.5rem;
    border-radius: 0.2rem;
    outline: none;
    border: 1px solid rgb(85, 83, 83);
  }
</style>
