<template>
  <div id="app">
    <Container>
      <Heading/>
      <EnterTask/>
      <TaskList/>
      <div class="textDrag">Drag and drop to reorder list</div>
    </Container>
  </div>
</template>

<script>
import Container from './components/container.vue'
import Heading from './components/heading.vue'
import EnterTask from './components/enterTask.vue'
import TaskList from './components/taskList.vue'

export default {
  components: {
    Container,
    Heading,
    EnterTask,
    TaskList
  }
}
</script>

<style lang="scss" scope>
@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@400;700&display=swap');
@import url('https://unpkg.com/reset-css/reset.css');

:root {
  --color-text_main: #494C6B;
  --color-text_done:#D1D2DA;
  --color-text_btn:#9495A5;
  --color-input: #fff;
  --bg-color: #FAFAFA;
  --bg-url: url("/assets/img/promo_light.jpg");
  --shadow: rgba(194, 195, 214, 0.5);
  --color-line: #E3E4F1;
  --text-through:#D1D2DA;
}

* {
  box-sizing: border-box;
  font-family:'Josefin Sans', sans-serif;
}

#app {
  position: relative;
  padding: 70px 0 52px 0;
  height: 100vh;
  background: var(--bg-color) var(--bg-url) top center / contain no-repeat;
  .bg_promo {
    width: 100vw;
    img {
      width: 100%;
    }
  }
}
.textDrag {
  position: absolute;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 14px;
  text-align: center;
  margin-top: 49px;
  color: var(--color-text_btn);
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
}
</style>
