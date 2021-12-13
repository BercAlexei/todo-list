<template>
    <input type="text" v-model="title" placeholder="Create a new todo…" @keyup.enter="addTask">
</template>

<script>

export default {
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTask() {
            if(this.title !== '') {
                this.$root.$emit('getTask', this.title)
                this.title = ''
            }
        }
    }
}
</script>

<style lang='scss' scope>
input {
    margin-top: 70px;
    width: 100%;
    height: 64px;
    background: var(--color-input);
    box-shadow: 0px 35px 50px -15px var(--shadow);
    border-radius: 5px;
    border: none;
    padding: 20px 24px;
    font-style: normal;
    font-weight: normal;
    font-size: 18px;
    line-height: 18px;
    letter-spacing: -0.25px;
    color: #9495A5;
    outline: none;
}

@media (max-width: 576px) {
    input {
        margin-top: 40px;
        height: 48px;
        font-size: 12px;
    }
}
</style>