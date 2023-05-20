<script>
export default {
    props: {
        addMove: Function,
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
    }
}
</script>

<template>
    <div class="container">
        <div class="player-container">
            <img alt="User Avatar" src="https://images.chesscomfiles.com/uploads/v1/master_player/5c8147c2-bd7f-11e8-863f-15ded6970bf6.00cda418.250x250o.1040af1a37a1.png" data-cy="chat-message-avatar" width="40" height="40" class="user-image" />
            <div class="player-name-container">
                <div class="player-name">
                    Hikaru <span>(2775)</span>
                    <img src="https://icons.iconarchive.com/icons/custom-icon-design/all-country-flag/128/United-States-Flag-icon.png" width="18" height="18" />
                </div>
                <div class="piece-container">
                    <i class='piece fas fa-chess-bishop black'></i>
                    <i class='piece fas fa-chess-bishop black'></i>
                    <i class='piece fas fa-chess-knight black'></i>
                    <i class='piece fas fa-chess-knight black'></i>
                    <i class='piece fas fa-chess-rook black'></i>
                    <i class='piece fas fa-chess-rook black'></i>
                    <i class='piece fas fa-chess-queen black'></i>
                </div>
            </div>
        </div>
        <div v-for="column in 8" :key="column" class="flex-container">
            <div v-for="row in 8" :key="row" :class="this.checkCell(column,row)" @click="this.setActive(column, row)">
                <div v-if="row === 1" class="col-title">{{ column }}</div>
                <div v-if="column === 8" class="row-title">{{ maps[row] }}</div>
            </div>
        </div>
        <div class="player-container">
            <img alt="User Avatar" src="https://images.chesscomfiles.com/uploads/v1/user/13147554.f0d2393d.50x50o.0a8f94b349c5.jpg" data-cy="chat-message-avatar" width="40" height="40" class="user-image" />
            <div class="player-name-container">
                <div class="player-name">
                    Freeiphone10s <span>(-700)</span>
                    <img src="https://icons.iconarchive.com/icons/custom-icon-design/all-country-flag/128/United-States-Flag-icon.png" width="18" height="18" />
                </div>
                <div class="piece-container">
                    <i class='piece fas fa-chess-pawn'></i>
                </div>
            </div>
        </div>
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
    .player-container{
        display: flex;
        padding: var(--space-lg) 0;
        color: var(--main-light-1);
    }
    .player-name {
        font-weight: bold;
        padding: 0 var(--space-md);
        font-size: var(--font-size-md);
        display: flex;
        justify-content: center;
        gap: var(--space-sm);
    }
    .player-name-container {
        display: flex;
        flex-direction: column;
    }
    .piece-container {
        display: flex;
        padding: var(--space-xsm) var(--space-md);
    }
    .piece {
        padding: 0 var(--space-xsm);
    }
    .black {
        color: var(--main-dark-1, black);
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