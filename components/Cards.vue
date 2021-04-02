<template>
    <ul>  
        <li>
            Ace of Hearts
        </li>
        <li>
            Ace of Spades 
        </li>
        <li>
            Jack of Diamonds 
        </li>
        <li>
            10 of Clovers
        </li>
        <li>
            4 of Spades
        </li>
    </ul>
</template>

<script>
    export default {
        name: "Cards",
        mounted() {
            this.showCards()  
        },
        methods: {
            showCards() {
                alert('Showing the cards');
            }
        }
    }
</script>

<style>

</style>
