<script>
    import { Card } from "../Grid"
    export let operator;
</script>

<div class="button-grid">
    <Card col={3}>
        <button on:click={() => operator = '+'} class:active={operator == '+'}>
            <span class="operator">+</span>
            <span class="label">ADD</span>
        </button>
    </Card>

    <Card col={3}>
        <button on:click={() => operator = '-'} class:active={operator == '-'}>
            <span class="operator">-</span>
            <span class="label">SUBTRACT</span>
        </button>
    </Card>

    <Card col={3}>
        <button on:click={() => operator = '*'} class:active={operator == '*'}>
            <span class="operator">×</span>
            <span class="label">MULTIPLY</span>
        </button>
    </Card>

    <Card col={3}>
        <button on:click={() => operator = '/'} class:active={operator == '/'}>
            <span class="operator">÷</span>
            <span class="label">DIVIDE</span>
        </button>
    </Card>
</div>

<style>
    .button-grid {
        display: block;
        gap: 10px;
        
    }

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

    button:hover {
        transform: translateY(-2px);
        box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
    }

    button:active, button.active {
        transform: translateY(1px);
        background: linear-gradient(145deg, #009ffd, #2a2a72);
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
    }

    .operator {
        font-size: 28px;
        font-weight: bold;
        display: block;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    }

    .label {
        font-size: 12px;
        opacity: 0.9;
        display: block;
        margin-top: 5px;
    }

    @media (max-width: 600px) {
        .button-grid {
            flex-direction: column;
        }
        
        .label {
            font-size: 10px;
        }
        
        .operator {
            font-size: 24px;
        }
    }
</style>
