<script>
  import { writable } from "svelte/store";

  const questions = [
    {
      text: "Question 1: When you have free time, you usually:",
      answers: [
        {
          id: "answer1-1",
          text: "Read books or learn something new",
          value: "Innovator",
        },
        { id: "answer1-2", text: "Work on your own projects", value: "Maker" },
        { id: "answer1-3", text: "Brainstorm new ideas", value: "Visionary" },
        { id: "answer1-4", text: "Socialize with friends", value: "Networker" },
      ],
    },
    {
      text: "Question 2: If you won the lottery, you would:",
      answers: [
        {
          id: "answer2-1",
          text: "Invest in stocks and real estate",
          value: "Innovator",
        },
        { id: "answer2-2", text: "Start your own company", value: "Maker" },
        {
          id: "answer2-3",
          text: "Donate to charity and help others",
          value: "Visionary",
        },
        { id: "answer2-4", text: "Travel the world", value: "Networker" },
      ],
    },
    {
      text: "Question 3: Your dream job would be:",
      answers: [
        { id: "answer3-1", text: "CEO of a tech company", value: "Innovator" },
        { id: "answer3-2", text: "Running a small business", value: "Maker" },
        {
          id: "answer3-3",
          text: "Leading a non-profit organization",
          value: "Visionary",
        },
        {
          id: "answer3-4",
          text: "Working in public relations",
          value: "Networker",
        },
      ],
    },
    {
      text: "Question 4: Your favorite subject in school was:",
      answers: [
        { id: "answer4-1", text: "Science and technology", value: "Innovator" },
        { id: "answer4-2", text: "Business and economics", value: "Maker" },
        { id: "answer4-3", text: "Art and humanities", value: "Visionary" },
        { id: "answer4-4", text: "Social studies", value: "Networker" },
      ],
    },
    {
      text: "Question 5: You would describe yourself as:",
      answers: [
        { id: "answer5-1", text: "Analytical and logical", value: "Innovator" },
        { id: "answer5-2", text: "Practical and hands-on", value: "Maker" },
        {
          id: "answer5-3",
          text: "Creative and idealistic",
          value: "Visionary",
        },
        { id: "answer5-4", text: "Outgoing and social", value: "Networker" },
      ],
    },
  ];

  const scores = writable({
    Innovator: 0,
    Maker: 0,
    Visionary: 0,
    Networker: 0,
  });
  const currentQuestion = writable(0);
  const selectedAnswer = writable(null);
  const showModal = writable(false);
  const result = writable("");

  const handleAnswer = (answer) => {
    scores.update((s) => {
      s[answer]++;
      return s;
    });
    selectedAnswer.set(null);
    currentQuestion.update((n) => n + 1);
  };

  const finishQuiz = () => {
    scores.subscribe((s) => {
      const maxScore = Object.keys(s).reduce((a, b) => (s[a] > s[b] ? a : b));
      result.set(`You're a(n) ${maxScore} entrepreneur!`);
    });
    showModal.set(true);
  };
</script>

<svelte:head>
  <title>Entrepreneur Quiz</title>
</svelte:head>

<div class="quiz-container">
  {#each questions as question, index (question.text)}
    {#if $currentQuestion === index}
      <div>
        <h3>{question.text}</h3>
        <ul>
          {#each question.answers as answer}
            <li>
              <input
                type="radio"
                id={answer.id}
                name="answer"
                bind:group={$selectedAnswer}
                value={answer.value}
              />
              <label for={answer.id}>{answer.text}</label>
            </li>
          {/each}
        </ul>
        {#if index < questions.length - 1}
          <button
            on:click={() => handleAnswer($selectedAnswer)}
            disabled={!$selectedAnswer}
          >
            Next
          </button>
        {:else}
          <button on:click={finishQuiz} disabled={!$selectedAnswer}>
            Finish
          </button>
        {/if}
      </div>
    {/if}
  {/each}
</div>

{#if $showModal}
  <div class="modal">
    <div class="modal-content">
      <p>{$result}</p>
      <button on:click={() => showModal.set(false)}>Close</button>
    </div>
  </div>
{/if}

<style>
  body {
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
    background-color: #edf2f7;
  }

  .quiz-container {
    max-width: 800px;
    margin: 2rem auto;
    background-color: #fff;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
    border-radius: 10px;
    padding: 2rem;
    text-align: center;
  }

  h3 {
    font-size: 1.5rem;
    margin-bottom: 1.5rem;
    color: #2d3748;
  }

  ul {
    list-style: none;
    padding: 0;
    display: grid;
    gap: 1rem;
  }

  li {
    display: flex;
    background: #f7fafc;
    border-radius: 5px;
    padding: 15px;
    align-items: center;
    transition: all 0.2s ease-in-out;
    cursor: pointer;
  }

  li:hover {
    transform: scale(1.02);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
  }

  label {
    flex: 1;
    margin-left: 15px;
  }

  button {
    display: inline-block;
    padding: 10px 20px;
    margin-top: 2rem;
    background-color: #48bb78;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: all 0.2s ease-in-out;
  }

  button:hover {
    background-color: #38a169;
    transform: scale(1.05);
  }
</style>
