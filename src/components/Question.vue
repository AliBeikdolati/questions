<template>
    <div class="jumbotron bg-white">
        <div class="">
            <!--  this head tag show question  -->
            <h1 class="display-5">{{ question.question }}</h1>

            <!--      this tag show the answer options      -->
            <div class="list-group mt-5 mx-auto p-0 col-md-7">
                <p class="list-group-item list-group-item-action mb-0"
                   v-for="(option, key) in options"
                   :key="key"
                   @click="setAnswer(option)"
                   :class="setColor(option, submited, key)"
                >
                    {{ option }}
                </p>
            </div>
            <div class="mt-5 mx-auto col-md-7">
                <div class="row">
                    <button
                            class="btn btn-success col mx-2 mb-2"
                            id="submitOption"
                            disabled
                            @click="submitAnswer"
                    >
                        submit
                    </button>
                    <button class="btn btn-outline-primary col mx-2 mb-2" @click="next">next</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Question",
        props: ['question', 'next', 'correct', 'wrong'],
        data() {
            return {
                options: [],  // this variable show the options of the question
                selectOption: null,  // this variable show the option that client selected
                submited: false,  // this variable show the client submit the question or not
            }
        },
        created() {

            // in this section we generate question options and randomize the sort of them

            let totalOptions = [];
            totalOptions = this.question.incorrect_answers;
            totalOptions.push(this.question.correct_answer);
            this.options = totalOptions.sort(() => Math.random() - 0.5);
            // console.log(this.question.correct_answer);
            // console.log(this.options);
        },
        updated() {

            // in this section we check for disabling the submit button

            document.getElementById('submitOption').disabled = this.submited;
        },
        computed: {},
        methods: {

            // this method set the answer of client choose
            setAnswer(option) {
                if (!this.submited) {
                    this.selectOption = option;
                    // console.log(this.selectOption);
                    this.submited = false;
                }

            },

            // this method set the background color of the question options for selected & correct & wrong answers
            setColor(option, submited, key) {
                // selected option before submit have grey bg-color
                if (!(submited) && this.selectOption === option) {
                    return 'grey'

                    //    after submit the correct answer have green bg-color
                } else if (submited && this.options[key] === this.question.correct_answer) {
                    return 'green'

                    //    after submit the wrong answer have red bg-color
                } else if (submited && this.options[key] === this.selectOption) {
                    return 'red'
                } else {
                    return ''
                }
            },

            submitAnswer() {
                this.submited = true;
                // console.log("submit");
                if (this.selectOption === this.question.correct_answer) {
                    this.correct();
                } else if (this.selectOption !== this.question.correct_answer) {
                    this.wrong();
                }

            }
        }
    }
</script>

<style scoped>

    .red {
        background-color: red;
    }

    .green {
        background-color: lightgreen;
    }

    .grey {
        background-color: lightgray;
    }

    .list-group-item:hover {
        cursor: pointer;
    }

    .btn {
        /*min-width: 200px;*/
    }

</style>