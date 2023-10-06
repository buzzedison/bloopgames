<script>
  // Import SVG icons or use inline SVGs here
  let games = [
    {
      title: "Business Games",
      description: "Engage in strategic business simulations.",
      icon: `
          <svg xmlns="http://www.w3.org/2000/svg" width="64" height="64" fill="#000000" class="bi bi-briefcase" viewBox="0 0 16 16">
            <path d="M3.5 0a.5.5 0 0 0-.5.5V5h1V.5a.5.5 0 0 0-.5-.5zM1 6.5V14h14V6.5a.5.5 0 0 0-.5-.5H14V5a1 1 0 0 0-1-1H3a1 1 0 0 0-1 1v1H1a.5.5 0 0 0-.5.5zM1 15a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v7a2 2 0 0 1-2 2H1z"/>
          </svg>
        `,
    },
    {
      title: "Leisure Games",
      description: "Relax and enjoy casual games.",
      icon: `
          <svg xmlns="http://www.w3.org/2000/svg" width="64" height="64" fill="#000000" class="bi bi-controller" viewBox="0 0 16 16">
            <path d="M0 6.5A2.5 2.5 0 0 1 2.5 4H4V2.5A2.5 2.5 0 0 1 6.5 0h3A2.5 2.5 0 0 1 12 2.5V4h1.5A2.5 2.5 0 0 1 16 6.5v3a2.5 2.5 0 0 1-2.5 2.5H14v1.5A2.5 2.5 0 0 1 11.5 16h-3A2.5 2.5 0 0 1 6 13.5V12H4.5A2.5 2.5 0 0 1 2 9.5v-3zM4 5V2.5A1.5 1.5 0 0 1 5.5 1h5A1.5 1.5 0 0 1 12 2.5V5H4z"/>
            <path d="M8 9.5a.5.5 0 0 1 .5-.5h1a.5.5 0 0 1 0 1h-1a.5.5 0 0 1-.5-.5z"/>
            <path d="M7.5 10a.5.5 0 0 1 0-1h1a.5.5 0 0 1 0 1h-1z"/>
          </svg>
        `,
    },
    {
      title: "General Games",
      description: "Explore a wide variety of games.",
      icon: `
          <svg xmlns="http://www.w3.org/2000/svg" width="64" height="64" fill="#000000" class="bi bi-joystick" viewBox="0 0 16 16">
            <path d="M2 5a4 4 0 0 1 4-4h2a4 4 0 0 1 4 4v3a1 1 0 0 1 1 1v3a4 4 0 0 1-4 4H6a4 4 0 0 1-4-4V9a1 1 0 0 1-1-1V5a4 4 0 0 1 4-4z"/>
            <path d="M7.5 14.697a1 1 0 0 1-.5-1.732L8.732 12.5 6 9.768a1 1 0 1 1 1.414-1.414l3 3a1 1 0 0 1 0 1.414l-3 3a1 1 0 0 1-.707.293z"/>
          </svg>
        `,
    },
  ];
</script>

<main>
  <section class="hero">
    <h1>Welcome to GameHub</h1>
    <p>Discover a world of games and fun.</p>
  </section>

  <section class="sub-section">
    {#each games as game}
      <div class="game-card">
        <div class="game-icon" on:click={() => handleCategoryClick(game.title)}>
          {@html game.icon}
        </div>
        <h2>{game.title}</h2>
        <p>{game.description}</p>
      </div>
    {/each}
  </section>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding: 2rem;
  }

  .hero {
    background-color: #007bff;
    color: #fff;
    padding: 3rem;
    border-radius: 10px;
    text-align: center;
  }

  .hero h1 {
    font-size: 2.5rem;
    margin: 0;
  }

  .hero p {
    font-size: 1.2rem;
  }

  .sub-section {
    display: flex;
    justify-content: space-around;
    margin: 2rem 0;
  }

  .game-card {
    width: 300px;
    padding: 1.5rem;
    border: 1px solid #ddd;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    text-align: center;
  }

  .game-icon {
    width: 64px;
    height: 64px;
    margin: 0 auto;
    cursor: pointer;
  }

  .game-card h2 {
    font-size: 1.5rem;
    margin: 1rem 0;
  }

  .game-card p {
    font-size: 1rem;
  }
</style>
