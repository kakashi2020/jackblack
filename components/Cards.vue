<template>
    <div>
        <p v-if="deck != null">
            The deck has been shuffled 
        </p>
        <p v-else> 
            Shuffling deck... 
        </p>
    </div>    
</template>

<script>
    export default {
        name: "Cards",
        data() { 
            return {
                deck: null,
                drawnCards: []
            } 
        },
        mounted() {
            this.getDeck()  
        },
        methods: {
            getDeck() {
                let uri = 'https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1';
                this.$axios.get(uri).then(response => {
                    this.deck = response.data;
                    this.drawCards(2, this.deck.deck_id)
                }).catch(() => { alert('oops: error!') });
            },
            drawCards(numCards, deckId) {
                let uri = `https://deckofcardsapi.com/api/deck/${deckId}/draw/?count=${numCards}`;
                this.$axios.get(uri).then(response => {
                    let cards = response.data.cards
                    for (let i = 0; i < cards.length; i++) {
                        this.drawnCards.push(cards[i]);
                    }
                }).catch(() => { alert('oops: error!') });
            }
        }
    }
</script>

<style>

</style>
