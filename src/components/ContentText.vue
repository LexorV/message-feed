<template>
    <span>
        <span v-if="isNotColorStart"> {{ startNotColorText }}</span>
        <span :style="{ background: colorFilter(tones.tone) }">{{ textColor }} </span>
        <span>{{ textNotcolor }}</span>
    </span>
</template>

<script>

export default {
    data() {
        return {
            countPosition: 0,
            textNotcolor: "",
            textColor: "",
            startNotColorText: '',
            isNotColorStart: (this.tonesIndex === 0 && this.tones.position !== 0) || false
        }
    },
    props: {
        tones: {
            type: Object,
            default: () => ({})
        },
        text: {
            type: String,
            default: ''
        },
        tonesIndex: {
            type: Number,
            default: 0
        },
        contentPostTones: {
            type: Array,
            default: () => []
        }

    },
    mounted() {
        this.filterPosition()
    },
    methods: {
        filterPosition() {
            this.countPosition = this.tones.position + this.tones.length
            let nextContent = (this.contentPostTones[this.tonesIndex + 1] ?
                this.contentPostTones[this.tonesIndex + 1].position : null) || this.contentPostTones[this.text.length]
            let startContent = this.tones.position + this.tones.length
            this.textNotcolor = this.text.slice(startContent, nextContent)
            if (this.isNotColorStart) {
                this.startNotColorText = this.text.slice(0, this.contentPostTones[0].position)
            }
            this.textColor = this.text.slice(this.tones.position, this.tones.position + this.tones.length)
        },
        colorFilter(tone) {
            let colorRed = 0;
            let colorGreen = 0;
            if (Math.sign(tone) === 1) {
                colorRed = Math.floor(255 - (255 * tone));
                colorGreen = 255
            }
            else if (Math.sign(tone) === 0) {
                colorRed = 255
                colorGreen = 255
            }
            else if (Math.sign(tone) === -1) {
                colorRed = 255
                colorGreen = Math.floor(255 - Math.abs(255 * tone));
            }

            return `rgba(${colorRed},${colorGreen},0, 0.5)`
        }


    }
}
</script>

<style scoped>
.test {}
</style>