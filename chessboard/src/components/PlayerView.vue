<script>
export default {
    name: 'PlayerView',
    props: {
        img: String,
        name: String,
        rating: Number,
        pieces: Object
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
    <div class="player-container">
        <img alt="User Avatar"
            :src="this.img"
            data-cy="chat-message-avatar" width="40" height="40" class="user-image" />
        <div class="player-name-container">
            <div class="player-name">
                {{ this.name }} <span>({{ this.rating }})</span>
                <img src="https://icons.iconarchive.com/icons/custom-icon-design/all-country-flag/128/United-States-Flag-icon.png"
                    width="18" height="18" />
            </div>
            <div class="piece-container">
                <div v-for="piece of pieces" :key="piece">
                    <i :class='piece'></i>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.player-container {
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
</style>