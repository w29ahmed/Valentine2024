<script lang="ts">
  import { onMount } from "svelte";
  import { fade } from "svelte/transition";
  import ThemeToggleSwitch from "./components/ThemeToggleSwitch.svelte";
  import NoButton from "./components/NoButton.svelte";
  import be_mine_image from "/assets/be_mine.png";
  import yes_image from "/assets/she_said_yes.png";
  import "./app.css";

  // Directly initialize isDarkTheme based on localStorage or default to light theme
  let isDarkTheme: boolean = localStorage.getItem("theme") === "dark";

  let yes_button_clicked: boolean = false;

  // Reactive statement to handle theme changes
  $: {
    console.log("App.Svelte " + isDarkTheme);
    localStorage.setItem("theme", isDarkTheme ? "dark" : "light");
    document.documentElement.classList.toggle("dark", isDarkTheme);
  }

  onMount(() => {
    // Apply the initial theme to the document
    document.documentElement.classList.toggle("dark", isDarkTheme);
  });

  function yesClicked() {
    yes_button_clicked = true;
  }
</script>

<body class="bg-red-300 dark:bg-indigo-950">
  <ThemeToggleSwitch bind:isDarkTheme />

  <div class="flex flex-col items-center justify-center min-h-screen px-4">
    <!-- Wrapper div to align content to the width of the image -->
    <!-- inline-block will shrink to fit the largest item -->
    <div class="inline-block">
      {#if yes_button_clicked}
        <!-- Top Row: Image -->
        <!-- width auto for the container to fit the content -->
        <div class="w-auto" transition:fade={{ duration: 300 }}>
          <!-- max height to ensure image is not too big -->
          <img src={yes_image} alt="Valentine's Image" class="w-full" />
        </div>

        <!-- Bottom Row: Text -->
        <!-- Full width of the parent -->
        <div class="w-full text-center" transition:fade={{ duration: 300 }}>
          <p class="text-4xl text-gray-900 dark:text-gray-200 my-4">Yay!</p>
        </div>
      {:else}
        <!-- Top Row: Image -->
        <!-- width auto for the container to fit the content -->
        <div class="w-auto">
          <!-- max height to ensure image is not too big -->
          <img src={be_mine_image} alt="Valentine's Image" class="w-full" />
        </div>

        <!-- Middle Row: Text -->
        <!-- Full width of the parent -->
        <div class="w-full text-center">
          <p class="text-3xl md:text-4xl text-gray-900 dark:text-gray-200 my-4">
            Will you be my Valentine?
          </p>
        </div>

        <!-- Bottom Row: Buttons -->
        <!-- Full width of the parents -->
        <div class="grid grid-cols-2 w-full py-2">
          <!-- Yes Button -->
          <div class="flex items-center justify-center">
            <button
              on:click={yesClicked}
              class="px-8 py-1 bg-red-500 text-white text-xl md:text-2xl rounded-lg hover:bg-red-700 transition"
              >Yes</button
            >
          </div>
          <!-- No Button -->
          <div class="flex items-center justify-center">
            <NoButton />
          </div>
        </div>
      {/if}
    </div>
  </div>
</body>

<style>
  p,
  button {
    font-family: "Pangolin", cursive;
  }
</style>
