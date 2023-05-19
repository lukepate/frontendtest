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
        <div v-for="column in 8" :key="column" class="flex-container">
            <div v-for="row in 8" :key="row" :class="this.checkCell(column,row)" @click="this.setActive(column, row)">
                <div v-if="row === 1" class="col-title">{{ column }}</div>
                <div v-if="column === 8" class="row-title">{{ maps[row] }}</div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .container {
        width: 64vw;
        height: 64vw;
        max-width: 840px;
        max-height: 840px;
    }
    .flex-container {
        padding: 0;
        margin: 0;
        display: flex;
        justify-content: center; 
    }

    .flex-item {
        flex: 1 0 auto;
        aspect-ratio: 1/1;
        background-color: #f0dab5;
        color: #b58962; 
        display: flex;
        font-weight: 700;
    }
    .flex-item div {
        width: 0;
        display: flex;
    }

    .flex-container:nth-child(even) .flex-item:nth-child(odd), 
    .flex-container:nth-child(odd) .flex-item:nth-child(even) {
        background-color: #b58962;   
        color: #f0dab5;  
    }
    .flex-item:nth-child(odd) .row-title {
        color: #f0dab5;   
    }
    .flex-item:nth-child(even) .row-title {
        color: #b58962;   
    }
    .active {
        background-color: #ffff00!important;
        opacity: 80%;
    }
    .hint {
        background-color: #de9280!important;
        opacity: 80%;
    }
    .row-title {
        justify-content: flex-end;
        flex-direction: column;
        margin-left: calc(100% - 16px);
    }
    .col-title {
        margin-left:4px;
        margin-top:2px;
    }

    @media screen and (max-width: 920px) {
        .row-title, col-title {
            display: none;
        }
  }

</style>