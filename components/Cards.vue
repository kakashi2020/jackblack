<template>
    <div>
        <p v-if="deck != null">
            The deck has been shuffled 
        </p>
        <p v-else> 
            Shuffling deck... 
        </p>
        <button v-if="deck != null" @click="drawCards(1, deck.deck_id)" type="button">Draw Cards</button>
        <ul v-if="deck != null">
            <li v-for="(card, i) in drawnCards" :key="i">
                <img :src="card.image" width="50">
                <span>
                    {{card.value}} of {{card.suit}}
                </span>
            </li>
        </ul>
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
                }).catch(() => { alert('The dealer was distracted try again!') });
            }
        }
    }
</script>

<style>

</style>
