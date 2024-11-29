<script>
    import { Card } from "../Grid"
    export let backgroundColor2;

</script>
    <Card>
        <button on:click ={() =>{
        if(backgroundColor2 == 'white'){
            return backgroundColor2 = 'green';
        }
        if(backgroundColor2 == 'green'){
        return backgroundColor2 = 'blue';
        }
        if(backgroundColor2 == 'blue'){
        return backgroundColor2 = 'red';
        }
        if(backgroundColor2 == 'red'){
            return backgroundColor2 = 'white';
        }}}>
    Back
    </button>
    </Card>


<style>
    button {
        padding: 3px 3px;
        font-size: 16px;
        border: none;
        cursor: pointer;
    }
</style>
