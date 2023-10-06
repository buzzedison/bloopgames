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
    font-family: "Roboto", sans-serif;
    background-color: #f5f5f5;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .quiz-container {
    width: 90%;
    max-width: 800px;
    background-color: #ffffff;
    box-shadow: 0px 14px 24px rgba(0, 0, 0, 0.1);
    border-radius: 12px;
    padding: 2em;
    text-align: left;
  }

  h3 {
    font-size: 1.25rem;
    color: #3c4043;
    margin-bottom: 1.25em;
    font-weight: 500;
  }

  ul {
    list-style: none;
    padding: 0;
  }

  li {
    display: flex;
    align-items: center;
    background: #e8f0fe;
    padding: 1em;
    border-radius: 8px;
    margin-bottom: 1em;
    cursor: pointer;
    transition: background 0.3s;
  }

  li:hover {
    background: #dceafb;
  }

  label {
    margin-left: 1em;
    color: #202124;
    font-size: 1rem;
  }

  input[type="radio"] {
    height: 20px;
    width: 20px;
    background-color: #dceafb;
  }

  button {
    background: #1a73e8;
    padding: 0.75em 1.5em;
    color: #ffffff;
    border: none;
    border-radius: 4px;
    font-size: 1rem;
    cursor: pointer;
    transition: background 0.3s;
    margin-top: 2em;
    display: block;
    width: 100%;
  }

  button:hover {
    background: #185abc;
  }
</style>
