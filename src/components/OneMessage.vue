<template>
    <li class="message">
        <div class="flex-box">
            <div>Дата: {{ new Date(messageData.date) }}</div>
            <div :style="{ color: 'red' }">Автор: {{ messageData.authorName }}</div>
        </div>
        <div class="flex-box">Сайт: {{ messageData.authorUrl }}</div>
        <div> Содержимое: <ContentText v-for="(tones, index) in messageData.contentPostTones"
                :key="Math.random() + tones.position" :tones-index="index" :contentPostTones="messageData.contentPostTones"
                :tones="tones" :text="messageData.content">
            </ContentText>
        </div>
    </li>
</template>

<script>
import ContentText from "@/components/ContentText.vue"
export default {
    components: {
        ContentText
    },
    props: {
        messageData: {
            type: Object,
            default: () => ({})
        }
    },
    data() {
        return {
            countPosition: 0
        }
    },
    methods: {
        colorText(text, postTones) {
            const textArr = text.split('');
            let count = 0;
            postTones.forEach((el) => {
                console.log(el.position + el.length)
                textArr.splice(el.position + count, 0, `<span :style="{color:'red'}">`)
                textArr.splice(el.position + (count + 1) + el.length, 0, `</span>`)
                count += 2

            })
            return textArr.join('')
        },
        filterPosition(text) {
            this.countPosition = text.position + text.length
            return this.messageData.content.slice(text.position, text.position + text.length)
        }

    },
    mounted() {
        ///console.log(this.colorText( this.messageData.content, this.messageData.contentPostTones ))
    }
}
</script>

<style scoped>
.message {
    display: flex;
    flex-direction: column;
    border-bottom: 1px solid black;
}

.flex-box {
    display: flex;
    justify-content: start;
    gap: 15px;
    box-sizing: border-box;
    padding: 10px;
}
</style>