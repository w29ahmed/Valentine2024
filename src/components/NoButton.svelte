<!--
  A button that says "No" and every time you click it, it "runs away" from you. A random position within
  the viewport is selected and the button is translated there. It's as if the button can never be pressed!
-->

<script lang="ts">
  // When CSS applies translations, its always from the original position of the element for some reason.
  // Because of this, keep track of the total X and Y translations applied to ensure every translation is
  // valid and actually moves the button to the desired location.
  let totalXTranslation = 0;
  let totalYTranslation = 0;

  function moveButton(event) {
    const button = event.target;
    const rect = button.getBoundingClientRect();

    // Current position of the button
    const currentX = rect.x;
    const currentY = rect.y;

    // Viewport dimensions and button dimensions
    const viewportWidth = window.innerWidth;
    const viewportHeight = window.innerHeight;
    const buttonWidth = button.offsetWidth;
    const buttonHeight = button.offsetHeight;

    // Calculate max possible position, subtract button dimensions to ensure entire button is always visible
    const maxX = viewportWidth - buttonWidth;
    const maxY = viewportHeight - buttonHeight;

    // Generate random position
    const newX = Math.floor(Math.random() * maxX);
    const newY = Math.floor(Math.random() * maxY);

    // Calculate difference
    const diffX = newX - currentX;
    const diffY = newY - currentY;

    // Update total translations
    totalXTranslation += diffX;
    totalYTranslation += diffY;

    // Translate
    button.style.transform = `translate(${totalXTranslation}px, ${totalYTranslation}px)`;
  }
</script>

<style>
  button {
    /* Animate translations */
    transition: transform 0.5s ease;
    font-family: 'Pangolin', cursive;
  }
</style>

<button
  on:click={moveButton}
  class="px-8 py-1 bg-gray-500 text-white text-2xl rounded-lg hover:bg-gray-700 transition">
  No
</button>
