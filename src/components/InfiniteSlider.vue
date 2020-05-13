<template>
    <div :style="{'--width': `${sliderWidth}px`}">
        <button @click="animate">Click</button>
        <div class="slider--container">
            <ul class="slider--grid" ref="sliderContainer" :style="{'--width': `${sliderWidth}px`, 'left': `${leftValue}px`}" >
                <li v-for="(item,index) in items" :key="index" class="slider--item" >
                    <h1>{{ item }}</h1>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: 'InfiniteSlider',
    data() {
        return {
            items: ['1', '2', '3', '4'],
            length: 0,
            currentX: 1,
            leftValue: 0,

        }
    },
    methods: {
        animate() {
            let random = Math.round(Math.random());
            random = random === 0 ? -1 : random;
            this.currentX += random;
                        this.$refs['sliderContainer'].animate([{
                    left: `${this.leftValue}px`
                }, 
                { 
                    left: `${this.leftValue + (this.sliderWidth * random * - 1)}px` 
                }], {
                    duration: 1000,
                    iterations: 1
                });

            this.leftValue = this.leftValue + (this.sliderWidth * random * -1);
            const shouldCycle = this.currentX > this.length || this.currentX === 0;
            if (shouldCycle) {
                switch(true) {
                    case this.currentX > this.length:
                        this.leftValue = 0;
                        this.currentX = 1;
                        break;
                    case this.currentX === 0:
                        this.leftValue = this.sliderWidth * -1 * (this.length);
                        this.currentX = this.length;
                        break;
                }
           }

        }
    },
    mounted() {
        this.length = this.items.length;
        // clone first and second
        const [first, second] = this.items;
        // clone second last and last
        const secondLast = this.items.slice(-2)[0];
        const last = this.items.slice(-1)[0];
        this.items.push(first);
        this.items.push(second);
        this.items.unshift(last);
        this.items.unshift(secondLast);
        this.leftValue = -1 * this.sliderWidth;

    //     setInterval(() => {
    //    }, 5000);
   },
    computed: {
        sliderWidth() {
            return window.innerWidth / this.length;
        },
    }
}
</script>

<style lang="scss" scoped>
.slider--container {
    position: relative;
    width: calc(var(--width) * 3);
    margin: 0 auto;
    overflow: hidden;
    height: 200px;
    border: 1px dotted black;
    .slider--grid {
        position: absolute;
        list-style-type: none;
        display: flex;
        top: 0;
        margin: 0;
        padding: 0;
        white-space: nowrap;
        // transition: transform 1s linear;

        .slider--item {
            height:200px;
            width: var(--width);
            border: 2px solid red;
            box-sizing: border-box;
        }
    }
}
</style>