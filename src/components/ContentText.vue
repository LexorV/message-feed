<template>
    <span>
        <span v-if="isNotColorStart" > {{ startNotColorText }}</span>
        <span :style="{background:'red'}">{{ textColor }} </span>
        <span>{{ textNotcolor }}</span>
    </span>
</template>

<script>

export default {
    data () {
        return {
            countPosition: 0,
            textNotcolor: "",
            textColor: "",
            startNotColorText:'',
            isNotColorStart:  (this.tonesIndex === 0 && this.tones.position !== 0) || false
        }
    },
    props: {
        tones: {
            type: Object,
            default: () => ({})
        },
        text: {
            type:String,
            default: ''
        },
        tonesIndex: {
            type:Number,
            default:0
        },
        contentPostTones: {
            type: Array,
            default: () => []
        }

    },
    mounted(){
        this.filterPosition()
    },
    methods: {
        filterPosition() {
        this.countPosition = this.tones.position + this.tones.length
        let nextContent = (this.contentPostTones[this.tonesIndex + 1]?
        this.contentPostTones[this.tonesIndex + 1].position : null) ||  this.contentPostTones[this.text.length]
        let startContent =  this.tones.position + this.tones.length
            this.textNotcolor =  this.text.slice(startContent, nextContent)
            if(this.isNotColorStart) {
                this.startNotColorText = this.text.slice(0, this.contentPostTones[0].position)
            }
                this.textColor =  this.text.slice(this.tones.position, this.tones.position + this.tones.length)   
    },
    notColorText() {
        console.log(this.countPosition,  this.contentPostTones[this.tonesIndex + 1].position)
       return this.text.slice(this.countPosition,  this.contentPostTones[this.tonesIndex + 1].position)
    }
    }
}
</script>

<style scoped>
.test {
}


</style>