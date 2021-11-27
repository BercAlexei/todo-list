<template>
  <div class="task">
      <input @click='change' type="checkbox" :id="id" :value="title" :checked='done'> 
      <label :for="id">{{ title }}</label>
      <div class="del" @click="clickDel">
        <svg width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path fill-rule="evenodd" clip-rule="evenodd" d="M17.6777 0.707107L16.9706 0L8.83883 8.13173L0.707107 0L0 0.707107L8.13173 8.83883L0 16.9706L0.707106 17.6777L8.83883 9.54594L16.9706 17.6777L17.6777 16.9706L9.54594 8.83883L17.6777 0.707107Z" fill="#5B5E7E"/>
        </svg>
    </div>
  </div>
</template>

<script>
export default {
    props: {
        title: String,
        id: Number,
        done: Boolean
    },
    methods: {
        clickDel() {
            this.$emit('deleteItem', this.id)
        },
        change(e) {
            this.$emit('changeDone', e.target)
        }
    }
}
</script>

<style lang="scss" scope>
    .task {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 20px 24px;
        width: 100%;
        height: 63px;
        font-style: normal;
        font-weight: normal;
        font-size: 18px;
        line-height: 18px;
        letter-spacing: -0.25px;
        color: var(--color-text_main);
        border-bottom: 1px solid var(--color-line);
        cursor: move;
        input {
            display: none;
            appearance: none;
            &:checked + label {
                text-decoration: line-through;
                color: var(--text-through);
                &:after {
                    content: url("../assets/icons/check.svg");
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    position: absolute;
                    left: 0.5px;
                    top: 0.5px;
                    width: 24px;
                    height: 24px;
                    border: none;
                    border-radius: 100%;
                    margin-right: 24px;
                    background: linear-gradient(135deg, #55DDFF 0%, #C058F3 100%);
                }
            }
        }
        label {
            position: relative;
            cursor: pointer;
            display: flex;
            align-items: center;
            &:before {
                content: '';
                display: block;
                width: 23px;
                height: 23px;
                border: 1px solid var(--color-line);
                border-radius: 100%;
                margin-right: 24px;
            }
          
        }
        span {
            cursor: pointer;
        }
        .del {
            cursor: pointer;
            display: none;
            &:hover {
                path {
                    filter: drop-shadow(1px 1px 2px red);
                    fill: red;
                }
            }
        }
        &:hover {
            .del {
                display: block;
            }
        }
    }
    
</style>