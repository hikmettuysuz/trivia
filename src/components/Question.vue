<template>

    <div class="question-box-container">
        <b-jumbotron>
            <template v-slot:lead>
                 {{currentQuestion.question}}
            </template>
            <b-list-group>
                <b-list-group-item v-for="(answer,index) in answers" :key="index" @click="selectAnswer(index)" :class="[selectedIndex===index ? 'selected':'']">
                    {{answer}}
                </b-list-group-item>
            </b-list-group>
            <b-button @click="previous" variant="primary" href="#">Previous</b-button>
            <b-button @click="next" variant="success" href="#">Next</b-button>
            <b-button @click="submitAnswer" variant="xss" href="#">Submit</b-button>

        </b-jumbotron>
    </div>
</template>

<script>

    export default {
        props:{
            currentQuestion: Object,
            next: Function,
            previous: Function
        },
        data() {
            return {
                selectedIndex: null,
                correctIndex: null
            }
        },
        watch:{
            currentQuestion: {
                immediate: true,
                handler(){
                    {
                        this.selectedIndex = null
                        this.shuffleMethod()
                    }
                }
            }
        },
        computed: {
            answers(){
                let answers = [];
                answers.push(this.currentQuestion.correct_answer);
                for(let i = 0 ; i < this.currentQuestion.incorrect_answers.length  ; i++){
                    answers.push(this.currentQuestion.incorrect_answers[i])
                }
                return answers;
            }
        },
        mounted() {
            console.log(this.currentQuestion)
        },
        methods: {
            selectAnswer(index){
                this.selectedIndex = index;

            },
            shuffleMethod(){
                this.correctIndex = this.answers.indexOf(this.currentQuestion.correct_answer)
            },
            submitAnswer(){
                if(this.selectedIndex === this.correctIndex){
                    console.log('dogru')
                }
            }
        }
    }
</script>

<style scoped>

    .selected{
        background-color: cadetblue;
    }
</style>