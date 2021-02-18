<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container">
            <a class="navbar-brand" href="#">Questions</a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav"
                    aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                    <li class="nav-item">
                        <a class="nav-link text-success disabled" href="#">correct answer: {{ correct }}</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link text-danger disabled" href="#">wrong answer: {{ wrong }}</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link text-warning disabled" href="#">not answer: {{ notAnswerQuestion }}</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link text-info disabled" href="#">total: {{questionsNumber + 1}} / {{ total }}</a>
                    </li>
                </ul>
            </div>
        </div>

    </nav>
</template>

<script>
    export default {
        name: "Navbar",
        props: ['questionsNumber', 'correct', 'wrong', 'total'],
        computed: {
            notAnswerQuestion: function () {
                let answers = this.correct + this.wrong;
                console.log(answers)

                return (this.questionsNumber - answers + 1);
            }
        }
    }
</script>

<style scoped>

</style>