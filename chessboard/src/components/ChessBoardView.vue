<script>
import PlayerView from './PlayerView.vue';

export default {
    name: 'ChessBoard',
    props: {
        setActive: Function,
        activeCell: String,
        hintCell: String,
        combineString: Function,
        maps: Object
    },
    methods: {
        checkCell(column, row) {
            switch (this.combineString(column, row)) {
                case this.activeCell:
                    return 'flex-item active';
                case this.hintCell:
                    return 'flex-item hint';
                default:
                    return "flex-item"
            }
        }
    },
    components: {
        PlayerView
    }
}
</script>

<template>
    <div class="container">
        <PlayerView 
            name="Hikaru"
            rating="2775"
            img="https://images.chesscomfiles.com/uploads/v1/master_player/5c8147c2-bd7f-11e8-863f-15ded6970bf6.00cda418.250x250o.1040af1a37a1.png" 
            :pieces="[
                'piece fa-solid fa-chess-bishop-piece black',
                'piece fa fa-chess-bishop black',
                'piece fa fa-chess-knight black',
                'piece fa fa-chess-knight black',
                'piece fa fa-chess-rook black',
                'piece fa fa-chess-rook black',
                'piece fa fa-chess-queen black',
            ]"
        />
        <div v-for="column in 8" :key="column" class="flex-container">
            <div v-for="row in 8" :key="row" :class="this.checkCell(column,row)" @click="this.setActive(column, row)">
                <div v-if="row === 1" class="col-title">{{ column }}</div>
                <div v-if="column === 8" class="row-title">{{ maps[row] }}</div>
            </div>
        </div>
        <PlayerView 
            name="Freeiphone10s"
            rating="-700"
            img="https://images.chesscomfiles.com/uploads/v1/user/13147554.f0d2393d.50x50o.0a8f94b349c5.jpg" 
            :pieces="['piece fas fa-chess-pawn']"
        />
    </div>
</template>

<style scoped>
    .container {
        width: 64vw;
        height: 64vw;
        max-width: 740px;
        max-height: 740px;
    }
    .flex-container {
        padding: 0;
        margin: 0;
        display: flex;
        justify-content: center; 
    }

    .flex-item {
        flex: 1 0 auto;
        aspect-ratio: 1 / 1;
        background-color: var(--light-cell, white);
        color: var(--dark-cell, brown); 
        display: flex;
        font-weight: var(--font-bold);
    }
    .flex-item div {
        width: 0;
        display: flex;
    }

    .flex-container:nth-child(even) .flex-item:nth-child(odd), 
    .flex-container:nth-child(odd) .flex-item:nth-child(even) {
        background-color: var(--dark-cell, brown);   
        color: var(--light-cell, white);  
    }
    .flex-item:nth-child(odd) .row-title {
        color: var(--dark-cell, brown);   
    }
    .flex-item:nth-child(even) .row-title {
        color: var(--light-cell, white);   
    }
    .active {
        background-color: var(--active-cell, white)!important;
        opacity: var(--light-opacity);
    }
    .hint {
        background-color: var(--hint-cell)!important;
        opacity: var(--light-opacity);
    }
    .row-title {
        justify-content: flex-end;
        flex-direction: column;
        margin-left: calc(100% - 16px);
    }
    .col-title {
        margin-left: var(--space-sm);
        margin-top: var(--space-xsm);
    }
    @media screen and (max-width: 920px) {
        .container {
            width: 84vw;
            height: 84vw;
        }
        .row-title, col-title {
            display: none;
        }
    }

</style>