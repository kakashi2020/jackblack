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
        data() { 
            return {
                deck: {}
            } 
        },
        mounted() {
            this.getDeck()  
        },
        methods: {
            getDeck() {
                let uri = 'https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1';
                this.$axios.get(uri).then(response => {
                    this.deck = response.data
                }).catch(() => { alert('oops: error!') });

            }
        }
    }
</script>

<style>

</style>
