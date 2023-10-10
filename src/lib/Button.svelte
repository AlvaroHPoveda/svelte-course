<script>
    export let size = 'small';
    export let shadow = false;
    export let bgColor = 'inherit';
    export let textColor = 'inherit';
    export let disabled = false;
    
    let isLefrHovered;
</script>

<button
    on:click
    {disabled}
    style:--background-color={bgColor}
    style:--buttonTextColor={textColor}
    class:size-lg={size === 'large'}
    class:size-sm={size === 'small'}
    class:has-left={$$slots.leftContent}
    class:shadow
    {...$$restProps}
    >
    {#if $$slots.leftContent}
        <div class="left-content" role="button" tabindex="0"
            on:mouseenter={() => (isLefrHovered = true)}
            on:mouseleave={() => (isLefrHovered = false)}
        >
            <slot name="leftContent" {isLefrHovered}/>
        </div>        
    {/if}
    <slot>Fallback</slot>
</button>

<style lang="scss">

    button {
        display: flex;
        align-items: center;
        border: none;
        background-color: var(--background-color);
        color: var(--buttonTextColor);
        padding: 15px 20px; 
        font-weight: bold;
        border-radius: 5px;
        cursor: pointer;
        .left-content {
            margin-right: 10px;
        }
        &:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }
        &:hover {
            background-image: linear-gradient(rgba(0, 0, 0, 0.4) 0 0);
        }
        &:active {
            background-image: linear-gradient(rgba(255, 255, 255, 0.1) 0 0);
        }
        &.size-sm {
            padding: 15px 20px; 
        }
        &.size-lg {
            padding: 20px 25px; 
            font-size: 20px;
        }
        &.shadow {
            box-shadow: 0 0 10px rgba(1, 1, 1, 0.3);
        }
    }
</style>
