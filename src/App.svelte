<script lang="ts">
  import { onMount } from "svelte";
  import ThemeToggleSwitch from "./components/ThemeToggleSwitch.svelte";
  import walle_eve_image from "./assets/walle_eve_no_bg_heart.png";
  // import walle_eve_image from "./assets/walle_eve.jpg";

  import "./app.css";

  // Directly initialize isDarkTheme based on localStorage or default to light theme
  let isDarkTheme: boolean = localStorage.getItem("theme") === "dark";

  // Reactive statement to handle theme changes
  $: {
    console.log("App.Svelte " + isDarkTheme);
    localStorage.setItem("theme", isDarkTheme ? "dark" : "light");
    document.documentElement.classList.toggle("dark", isDarkTheme);
  }

  let totalX = 0;
  let totalY = 0;

  function moveButton(event) {
    const button = event.target;
    const rect = button.getBoundingClientRect();

    // Current position
    const currentX = rect.x;
    const currentY = rect.y;

    // Viewport dimensions and button dimensions
    const viewportWidth = window.innerWidth;
    const viewportHeight = window.innerHeight;
    const buttonWidth = button.offsetWidth;
    const buttonHeight = button.offsetHeight;

    // Calculate max position in pixels
    const maxX = viewportWidth - buttonWidth;
    const maxY = viewportHeight - buttonHeight;

    // Generate random position
    const newX = Math.floor(Math.random() * maxX);
    const newY = Math.floor(Math.random() * maxY);


    // Calculate difference
    const diffX = newX - currentX;
    const diffY = newY - currentY;

    // Update total translations
    totalX += diffX;
    totalY += diffY;

    // Translate
    button.style.transform = `translate(${totalX}px, ${totalY}px)`;
  }

  onMount(() => {
    // Apply the initial theme to the document
    document.documentElement.classList.toggle("dark", isDarkTheme);
  });
</script>

<style>
  p, button {
    font-family: 'Pangolin', cursive;
  }

  .no-button {
    transition: transform 0.5s ease;
  }
</style>

<body class="bg-red-300 dark:bg-gray-900">
  <ThemeToggleSwitch bind:isDarkTheme />

  <div class="flex flex-col items-center justify-center min-h-screen px-4">
    <!-- Wrapper div to align content to the width of the image -->
    <!-- inline-block will shrink to fit the largest item -->
    <div class="inline-block">

      <!-- Top Row: Image -->
      <div class="w-auto"> <!-- width auto for the container to fit the content -->
        <!-- max height to ensure image is not too big -->
        <img src={walle_eve_image} alt="Valentine's Image" class="w-full">
      </div>

      <!-- Middle Row: Text -->
      <!-- Full width of the parent -->
      <div class="w-full text-center">
        <p class="text-4xl text-gray-900 dark:text-gray-200 my-4">Will you be my Valentine?</p>
      </div>

      <!-- Bottom Row: Buttons -->
      <!-- Full width of the parents -->
      <div class="grid grid-cols-2 w-full py-2">
        <!-- Yes Button -->
        <div class="flex items-center justify-center">
          <button class="px-8 py-1 bg-red-500 text-white text-2xl rounded-lg hover:bg-red-700 transition">Yes</button>
        </div>
        <!-- No Button -->
        <div class="flex items-center justify-center">
          <button on:click={moveButton} class="no-button px-8 py-1 bg-gray-500 text-white text-2xl rounded-lg hover:bg-gray-700 transition">No</button>
        </div>
      </div>

    </div>
  </div>
</body>
