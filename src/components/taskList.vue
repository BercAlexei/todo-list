<template>
  <div class="task-list">
    <draggable class="tasks" v-model="tasks" :move="onMove" @start="drag=true" @end="drag=false">
      <Task 
        v-for='item in tasksSort'
        :done='item.done' 
        :key="item.id" 
        :id="item.id" 
        :title='item.title'
        @changeDone='checkUpdate($event)'
        @deleteItem='deleteItem($event)'
      />
    </draggable>
    <div class="task-list__footer">
      <div>
        {{tasksSort.length}} items left
      </div>
      <div class="filter">
        <input type="radio" id="all" value="all" v-model="filter">
        <label for="all">All</label>

        <input type="radio" id="active" value="active" v-model="filter">
        <label for="active">Active</label>

        <input type="radio" id="completed" value="completed" v-model="filter">
        <label for="completed">Completed</label>
      </div>
      <div>
        <button class="btn clear" @click="deleteCompleted">Clear Completed</button>
      </div>
    </div>
    <div class="filter filter_mob">
        <input type="radio" id="all" value="all" v-model="filter">
        <label for="all">All</label>

        <input type="radio" id="active" value="active" v-model="filter">
        <label for="active">Active</label>

        <input type="radio" id="completed" value="completed" v-model="filter">
        <label for="completed">Completed</label>
      </div>
  </div>
  
</template>

<script>
import Task from './task.vue'
import draggable from 'vuedraggable'

class Item{
  constructor(id, title) {
    this.id =id
    this.title = title,
    this.done = false
  }
}

export default {
  data() {
    return {
      filter: 'all',
      tasks: [
        {
          id:1,
          title: 'Первый',
          done: false
        },
        {
          id:2,
          title: 'Второй',
          done: false
        },
        {
          id:3,
          title: 'Третий',
          done: false
        },
        {
          id:4,
          title: 'Четвертый',
          done: false
        },
        {
          id:5,
          title: 'Пятый',
          done: false
        }
      ]
    }
  },
  components: {
    Task,
    draggable
  },
  computed: {
    tasksSort() {
      switch(true) {
        case(this.filter === 'all'): 
          return this.tasks.sort((a, b) => {
            return Number(b.done) - Number(a.done)
          })
        case(this.filter === 'active'):
          return this.tasks.filter(element => !element.done)
        case(this.filter === 'completed') :
          return this.tasks.filter(element => element.done)
      }
    }
  },
  mounted() {
    this.$root.$on('getTask', event => {
      let newTask = new Item(this.tasks.length + 1, event)
      this.tasks.push(newTask)
    })
  },
  methods: {
    onMove({ relatedContext, draggedContext }) {
      const relatedElement = relatedContext.element;
      const draggedElement = draggedContext.element;
      return (
        (!relatedElement || !relatedElement.done) && !draggedElement.done
      );
    },
    checkUpdate(e) {
      this.tasks.filter(element => {
        if(e.id == element.id) {
          element.done = e.checked
        }
      })
    },
    deleteItem(item) {
      this.tasks = this.tasks.filter(element => element.id !== item)
    },
    deleteCompleted() {
      this.tasks = this.tasks.filter(element => !element.done)
    }
  }
}
</script>

<style lang='scss' scope>

.task-list {
  margin-top: 24px;
  width: 100%;
  background: var(--color-input);
  box-shadow: 0px 35px 50px -15px var(--shadow);
  border-radius: 5px;
  &__footer {
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 20px 24px;
    font-style: normal;
    font-weight: normal;
    font-size: 14px;
    line-height: 14px;
    color: var(--color-text_btn);
    .btn {
      cursor: pointer;
      font-style: normal;
      font-weight: bold;
      font-size: 14px;
      line-height: 14px;
      color: var(--color-text_btn);
      background: initial; 
      border: none;
      padding: 0;
    }
    .btn.clear {
        font-weight: normal;
    }
  }
}
.filter {
  input {
    display: none;
    appearance: none;
    &:checked + label {
      color: #3A7CFD;
    }

  }
  label {
    margin-right: 19px;
    cursor: pointer;
    font-style: normal;
    font-weight: bold;
    font-size: 14px;
    line-height: 14px;
    color: var(--color-text_btn);
    background: initial; 
    border: none;
    padding: 0;
    &:last-child {
      margin-right: 0;
    }
  }
  &_mob {
    display: none;
    position: absolute;
    width: 100%;
    margin-top: 16px;
    text-align: center;
    padding: 15px 0;
    background: var(--color-input);
    box-shadow: 0px 35px 50px -15px var(--shadow);
    border-radius: 5px;
  }
}

@media (max-width: 768px) {}

@media (max-width: 576px) {
  .filter {
    display: none;
    &_mob {
      display: block;
    }
  }
  .task-list {
    margin-top: 16px;
  }
}
</style>