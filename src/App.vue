<template>
  <div id="app">
    <div class="container">
      <Heading/>
      <EnterTask/>
      <TaskList/>
      <div class="textDrag">Drag and drop to reorder list</div>
    </div>
  </div>
</template>

<script>
import Heading from './components/heading.vue'
import EnterTask from './components/enterTask.vue'
import TaskList from './components/taskList.vue'

export default {
  components: {
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
  --bg-url: url("assets/img/promo_light.jpg");
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
  min-height: 100vh;
  background: var(--bg-url) top center / 100% 300px no-repeat var(--bg-color);
}
.textDrag {
  position: relative;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 14px;
  margin-top: 49px;
  text-align: center;
  color: var(--color-text_btn);
}
.container {
  position: relative;
  margin: 0 auto;
  max-width: 540px;
}

@media (max-width: 768px) {
  #app {
    background-size: 100% 230px;
  }
}

@media (max-width: 576px) {
  #app {
    background-size: 100% 200px;
    padding: 48px 0 50px 0;
    // height: 100%;
  }
  .container {
    position: relative;
    margin: 0 auto;
    max-width: calc(100% - 52px);
  }
  .textDrag {
    margin-top: 104px;
  }
}
</style>
