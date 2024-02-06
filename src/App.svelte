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

  // Apply the initial theme to the document
  onMount(() => {
    document.documentElement.classList.toggle("dark", isDarkTheme);
  });
</script>

<style>
  p, button {
    font-family: 'Pangolin', cursive;
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
        <div class="flex items-center justify-center">
          <button class="px-8 py-1 bg-red-500 text-white text-2xl rounded-lg hover:bg-red-700 transition">Yes</button>
        </div>
        <div class="flex items-center justify-center">
          <button class="px-8 py-1 bg-gray-500 text-white text-2xl rounded-lg hover:bg-gray-700 transition">No</button>
        </div>
      </div>

    </div>
  </div>
</body>
