<template>
    <ul class="progress">
        <div
            v-for="(counter, index) in loop"
            :key="index"
            :class="wrapperClass(index)"
        >
            <li :class="itemClass(index)">
                <img
                    v-if="score"
                    :src="require('@/assets/svg/' + iconClass(index) + '.svg')"
                />
                <span v-else>{{ counter }}</span>
            </li>

            <li v-if="counter !== loop" class="progress-line"></li>
        </div>
    </ul>
</template>

<script>
export default {
    name: "ProgressBar",

    props: {
        loop: Number,
        isActive: Number,
        score: {
            type: Array,
            required: false
        }
    },

    methods: {
        wrapperClass(index) {
            return {
                wrapper: true,
                active: this.isActive === index,
                "score-bar": !!this.score
            };
        },

        itemClass(index) {
            return ["progress-item", this.score ? this.isCorrect(index) : null];
        },

        isCorrect(index) {
            if (this.score[index] === undefined) return;
            return this.score[index] ? "correct" : "incorrect";
        },

        iconClass(index) {
            if (this.score[index] === undefined) return "question";
            return this.score[index] ? "check" : "times";
        }
    }
};
</script>

<style lang="scss" scoped>
ul.progress {
    div.wrapper {
        &.score-bar {
            li.progress-item {
                padding: 5px 4px;
            }
            li.progress-line {
                background-color: #dcdcdc;
                padding: 0 0.1em;
            }
            &.active {
                li.progress-item {
                    background-color: #dcdcdc;
                }
            }
        }
    }
}

/** Custom Classes **/
.incorrect {
    background-color: lightcoral !important;
}
.correct {
    background-color: lightgreen !important;
}
</style>
