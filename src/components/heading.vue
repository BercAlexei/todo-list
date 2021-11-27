<template>
    <div class="heading">
        <h1>
            TODO
        </h1>
        <div>
            <label for="theme">
                <img :src="url_icon" alt="change_theme">
            </label>
            <input type="checkbox" id="theme" v-model='dark'>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            dark: false,
            url_icon: './assets/icons/moon.svg'
        }
    },
    mounted: function() {
        this.root = document.documentElement;
        if(localStorage.getItem('theme') === 'dark') {
            this.root.style.setProperty("--bg-color", "#171823")
            this.root.style.setProperty("--color-text_main", "#C8CBE7")
            this.root.style.setProperty("--color-text_btn", "#5B5E7E")
            this.root.style.setProperty("--shadow", "rgba(0, 0, 0, 0.5)")
            this.root.style.setProperty("--color-input", "#25273D")
            this.root.style.setProperty("--bg-url", `url('../assets/img/promo_dark.jpg')`)
            this.root.style.setProperty("--color-line", "#393A4B")
            this.root.style.setProperty("--text-through", "#4D5067")
            this.url_icon = './assets/icons/sun.svg'
            this.dark = true
        }
    },
    watch: {
        dark: {
            handler: function () {
                this.$nextTick(() => {
                    if(this.dark) {
                        this.root.style.setProperty("--bg-color", "#171823")
                        this.root.style.setProperty("--color-text_main", "#C8CBE7")
                        this.root.style.setProperty("--color-text_btn", "#5B5E7E")
                        this.root.style.setProperty("--shadow", "rgba(0, 0, 0, 0.5)")
                        this.root.style.setProperty("--bg-url", `url('../assets/img/promo_dark.jpg')`)
                        this.root.style.setProperty("--color-input", "#25273D")
                        this.root.style.setProperty("--color-line", "#393A4B")
                        this.root.style.setProperty("--text-through", "#4D5067")
                        this.url_icon = './assets/icons/sun.svg'
                        localStorage.setItem('theme', 'dark')
                        this.dark = true
                    }else {
                        this.root.style.setProperty("--bg-color", "#FAFAFA")
                        this.root.style.setProperty("--color-text_main", "#494C6B")
                        this.root.style.setProperty("--color-text_btn", "#9495A5")
                        this.root.style.setProperty("--shadow", "rgba(194, 195, 214, 0.5)")
                        this.root.style.setProperty("--color-input", "#ffffff")
                        this.root.style.setProperty("--bg-url", `url('../assets/img/promo_light.jpg')`)
                        this.root.style.setProperty("--color-line", "#E3E4F1")
                        this.root.style.setProperty("--text-through", "#D1D2DA")
                        this.url_icon = './assets/icons/moon.svg'
                        localStorage.setItem('theme', 'light')
                        this.dark = false
                    }
                })
            }
        }
    }

}
</script>

<style lang='scss' scope>
    .heading {
        display: flex;
        align-items: center;
        justify-content: space-between;
        h1 {
            font-family: Josefin Sans;
            font-style: normal;
            font-weight: bold;
            font-size: 40px;
            line-height: 40px;
            letter-spacing: 15px;
            color: #FFFFFF;
        }
        input {
            display: none;
            appearance: none;
        }
        label {
            cursor: pointer;
        }
    }
</style>