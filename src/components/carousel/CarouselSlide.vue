<template>
    <div class="nocarou_item" :data-index="index" :style="{width: itemRatio}">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        props: {
            index: {
                type: Number,
                default: 0
            }
        },

        computed: {
            /** Item width ratio in percent
             * @returns {string} */
            itemRatio() {
                return (100 / this.$parent.itemsToShow) / this.$parent.ratio + "%";
            }
        },
    }
</script>
