<script>
    import { Card } from "../Grid"
    
    export let count;
</script>

<Card>
    <button  on:click={() => {
        count++
        
        }}>
        <span class="count">{count}</span>
        <span class="label">CLICKS</span>
    </button>
    <slot />
</Card>

<style>
    button {
        width: 100%;
        background: linear-gradient(145deg, #2a2a72, #009ffd);
        border: none;
        padding: 15px 25px;
        border-radius: 12px;
        cursor: pointer;
        color: white;
        font-family: 'Arial', sans-serif;
        text-transform: uppercase;
        position: relative;
        overflow: hidden;
        transition: transform 0.2s, box-shadow 0.2s;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
    }
    button.black {
        background: black;
    }
    button:hover {
        transform: translateY(-2px);
        box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
    }

    button:active {
        transform: translateY(1px);
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
    }

    .count {
        font-size: 24px;
        font-weight: bold;
        display: block;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    }

    .label {
        font-size: 14px;
        opacity: 0.9;
        display: block;
        margin-top: 5px;
    }
</style>