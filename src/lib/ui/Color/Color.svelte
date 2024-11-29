<script>
    import { Card } from "../Grid"
    export let backgroundColor;

</script>
    <Card>
        <button on:click ={() =>{
        if(backgroundColor == 'white'){
            return backgroundColor = 'red';
        }
        if(backgroundColor == 'red'){
        return backgroundColor = 'blue';
        }
        if(backgroundColor == 'blue'){
        return backgroundColor = 'green';
        }
        if(backgroundColor == 'green'){
            return backgroundColor = 'white';
        }}}>
    Next
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
