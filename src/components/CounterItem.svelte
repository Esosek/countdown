<script>
  import { beforeUpdate, onMount } from 'svelte';

  export let label;
  export let value = 0;

  let boardElement = undefined;

  onMount(() => {
    boardElement = document.getElementById(`board-${label}`);
  });

  // Fix this, it's optimized and not working
  beforeUpdate(() => {
    if (boardElement) {
      boardElement.classList.remove('flip-animation');

      setTimeout(() => {
        boardElement.classList.toggle('flip-animation');
      }, 50);
    }
  });
</script>

<div class="relative overflow-clip">
  <div
    id={`board-${label}`}
    class="board flip-animation flex items-center justify-center
    bg-gradient-to-b from-blue-600/50 to-50% to-blue-600 from-50%
    size-[4.25rem] sm:size-[8rem] rounded-md shadow-lg
    before:bg-blue-800 after:bg-blue-800"
  >
    <p class="text-primary-red text-xl sm:text-[4.5rem]">
      {value.toLocaleString('en-US', { minimumIntegerDigits: 2 })}
    </p>
  </div>
  <p
    class="text-primary-blue text-sm sm:text-base uppercase tracking-[2px] my-4"
  >
    {label}
  </p>
</div>

<style>
  .board {
    transform: rotateX(90deg);
  }

  .flip-animation {
    transform: none;
    transition: transform 400ms ease-out;
  }

  .board::before,
  .board::after {
    --radius: 0.5rem;
    content: '';
    position: absolute;
    width: var(--radius);
    height: var(--radius);
    border-radius: 50%;
  }

  .board::before {
    left: calc(var(--radius) / -2);
  }

  .board::after {
    right: calc(var(--radius) / -2);
  }

  @media only screen and (min-width: 640px) {
    .board::before,
    .board::after {
      --radius: 1rem;
    }
  }
</style>
