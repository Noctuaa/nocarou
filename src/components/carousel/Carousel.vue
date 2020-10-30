<template>
    <div class="nocarou" tabindex="0" v-on:keyup.left="prev" v-on:keyup.right="next">
        <div class="nocarou_container">
        <div class="nocarou_track" ref="items" :style="{width: (ratio * 100) + '%'}">
            <slot></slot>
        </div>
        </div>
        <button class="next" v-show="showButton('next')" @click='next'></button>
        <button class="prev" v-show="showButton('prev')" @click='prev'></button>
    </div>
</template>

<script>
    export default {
        props: {
            /** Number of items to scroll.
             * @param {Number} itemsToScroll - 1 */
            itemsToScroll: {
                type: Number,
                default: 1
            },
            /** Number of elements displayed in a slide
             * @param {Number} itemsToShow - 1 */
            itemsToShow: {
                type: Number,
                default: 1
            },
            /** Should we looped at the end of the slide
             * @param { boolean } loop - false */
            loop: {
                type: Boolean,
                default: false
            },
            /** Transition speed of the slide
             * @param {number} transition - 500 */
            transition: {
                type: Number,
                default: 500
            },
        },
        data() {
            return {
                slides: [],
                currentItem: 0,
                ratio: '',
            }
        },

        methods: {
            /** Go to next item */
            next() {
                this.goTo(this.currentItem + this.itemsToScroll);
            },
            /** Go to previous item */
            prev() {
                this.goTo(this.currentItem - this.itemsToScroll);
            },

            /** Moves the slider to the targeted item.
             * @param {number} index - Current item */
            goTo(index) {
                if (index < 0) {
                    if(this.loop){ index = this.itemsCount - this.itemsToShow}
                    else { return }
                } else if (index >= this.itemsCount || (this.slides[this.currentItem + this.itemsToShow] === undefined) && index > this.currentItem) {
                    if(this.loop) { index = 0 }
                    else { return }             
                }
                const translateX = index * -100 / this.itemsCount
                this.$refs.items.style.transform = "translate3d(" + translateX + '%, 0, 0)';
                this.$refs.items.style.transition = this.transition + 'ms';
                this.currentItem = index;
            },

            /** Condition when to display button
             * @param {string} direction - Slider direction 
             */
            showButton(direction){
                if(this.loop){
                    return true;
                }else if(direction === 'prev'){
                    return this.currentItem == 0 ? false : true;
                }else if(direction === 'next'){
                     return this.currentItem >= this.itemsCount || this.slides[this.currentItem + this.itemsToShow] === undefined ? false : true;
                }
            }
        },

        computed: {
            /** Total number of items
             * @returns {number}
             */
            itemsCount() {
                return this.slides.length;
            },
        },

        mounted() {
            this.slides = [].slice.call(this.$refs.items.children); /** Get child elements and convert them to a new array */
            this.ratio = this.$refs.items.children.length / this.itemsToShow;
        },
    }
</script>
