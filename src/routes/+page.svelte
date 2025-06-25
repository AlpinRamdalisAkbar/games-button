<script lang="ts">
    import { fly } from "svelte/transition";

    let visible: boolean = false;
    let glowDirection: 'top' | 'bottom' | 'left' | 'right' = 'top';

    function glowClass(dir: string): string {
        switch (dir) {
            case 'top': return 'shadow-[0_-10px_20px_#00FF00]';     // green
            case 'right': return 'shadow-[10px_0_20px_#FF0000]';    // red
            case 'bottom': return 'shadow-[0_10px_20px_#00BFFF]';   // blue
            case 'left': return 'shadow-[-10px_0_20px_#FF69B4]';    // pink
            default: return '';
        }
    }

    function toggleVisibility() {
        visible = !visible;

        if (visible) {
			// Pick direction randomly or based on logic
			const directions = ['top', 'right', 'bottom', 'left'];
			glowDirection = directions[Math.floor(Math.random() * 4)];
		}
    }
</script>

<div class="relative flex justify-center items-center h-dvh bg-gray-800">
    {#if visible}
            <!-- triangle  -->
            <svg in:fly={{ x: 0, y: 200, duration: 600 }} out:fly={{ x: 0, y: 200, duration: 600 }} class="absolute top-10 w-20 h-20 drop-shadow-[0_0_10px_#00FF00]" viewBox="0 0 24 24">
                <polygon points="12,4 4,20 20,20" fill="none" stroke="#00FF00" stroke-width="2" />
            </svg>
            
            <!-- Square (Left) -->
            <svg in:fly={{ x: 600, y: 0, duration: 600 }} out:fly={{ x: 600, y: 0, duration: 600 }} class="absolute left-10 w-20 h-20 drop-shadow-[0_0_10px_#FF69B4]" viewBox="0 0 24 24">
                <rect x="4" y="4" width="16" height="16" fill="none" stroke="#FF69B4" stroke-width="2" />
            </svg>
            
            <!-- Circle (Right) -->
            <svg in:fly={{ x: -600, y: 0, duration: 600 }} out:fly={{ x: -600, y: 0, duration: 600 }} class="absolute right-10 w-20 h-20 drop-shadow-[0_0_10px_#FF0000]" viewBox="0 0 24 24">
                <circle cx="12" cy="12" r="10" fill="none" stroke="#FF0000" stroke-width="2" />
            </svg>

            <!-- Cross (Bottom) -->
            <svg in:fly={{ x: 0, y:-200, duration: 600 }} out:fly={{ x: 0, y:-200, duration: 600 }} class="absolute bottom-10 w-20 h-20 drop-shadow-[0_0_10px_#00BFFF]" viewBox="0 0 24 24">
                <line x1="6" y1="6" x2="18" y2="18" stroke="#00BFFF" stroke-width="2" />
                <line x1="18" y1="6" x2="6" y2="18" stroke="#00BFFF" stroke-width="2" />
            </svg>
    {/if}


    <input
        on:click={toggleVisibility}
        type="button"
        value="Let's Play"
        class={`z-10 duration-300 ease-in pt-5 pb-5 pr-10 pl-10 rounded-2xl text-gray-300 bg-gray-700
            ${visible ? glowClass(glowDirection) : ''}`}
    />
</div>
<style lang="postcss">
    @reference "tailwindcss";
    :global(html) {
        background-color: theme(--color-gray-800);
    }
</style>