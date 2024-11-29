<script>
    import { Card } from "../Grid"
    export const {a, b, operator} = $props()

    function amount_calc (a, b, operator) {
        if(operator == '+'){
            return a + b;
        }
        if(operator == '-'){
        return a - b;
        }
        if(operator == '*'){
        return a * b;
        }
        if(operator == '/'){
            return a / b;
        }
        return 0;
    }
    const amount = $derived(amount_calc(a, b, operator))
</script>
<Card>
    {amount}
</Card>