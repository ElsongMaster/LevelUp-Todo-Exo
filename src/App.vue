<template>
  <div id="app">
    <div class="main-container">
      <div class="header">
        <div class="container-todo"><span>todo</span></div>
        <div class="containerDay-Night">
          <img src="./assets/icon-moon.svg" alt="" />
        </div>
      </div>
      <div class="newTodo">
        <input
          type="radio"
          id="huey"
          name="drone"
          value="huey"
          class="input-radio"
        />
        <input
          type="text"
          placeholder="Create a new todo.."
          v-on:keyup.enter="createDataItemTodo()"
          class="input-text"
        />
      </div>
      <div class="container-todolist">
        <TodoItem
          v-for="(item, index) in tabTodoItem"
          :dataObject="item"
          :key="index"
          @setIndexObject="getIndexObj"
          @checkRadio="updateData"
        />
      </div>
      <div class="container-options">
        <div class="item-left">
          <span>{{ numberItem }} items left</span>
        </div>
        <div class="option-filters">
          <span class="tag" @click="filterTodoItem('all',$event)">All</span
          ><span class="tag" @click="filterTodoItem('active',$event)"
            >Active</span
          ><span class="tag" @click="filterTodoItem('completed',$event)"
            >Completed</span
          >
        </div>
        <div class="clear-container" ><span @click="clearCompleted()">Clear Completed</span></div>
      </div>
    </div>
    <p>Drag and drop to reorder list</p>
  </div>
</template>

<script>
import TodoItem from "./components/TodoItem.vue";
export default {
  name: "App",
  components: {
    TodoItem,
  },
  data() {
    return {
      tabTodoItem: [
        {
          text: "Complete online Javascript-course",
          completed: false,
          active: false,
          index: 0,
          isSelected: false,
          tabTag: ["all", "active"],
          display: true,
          textIsStrike:false
        },
      ],
    };
  },

  methods: {
    createDataItemTodo() {
      let textItem = document.getElementsByClassName("input-text")[0].value;

      let itemObejct = {
        text: textItem,
        completed: false,
        active: false,
        index: this.tabTodoItem.length,
        isSelected: false,
        tabTag: ["all", "active"],
        display: true,
        textIsStrike:false
      };

      this.tabTodoItem.push(itemObejct);
    },

    deleteObject(index) {
      this.tabTodoItem.splice(index, 1);
    },

    getIndexObj(index) {
      this.deleteObject(index);
    },
    updateData(index) {
      let dataObjectTmp = this.tabTodoItem[index];
      if (dataObjectTmp.isSelected) {
        dataObjectTmp.isSelected = false;
        dataObjectTmp.textIsStrike =false

        dataObjectTmp.tabTag.splice(
          dataObjectTmp.tabTag.indexOf("completed"),
          1
        );

        dataObjectTmp.tabTag.push("active");
      } else {
        this.tabTodoItem[index].isSelected = true;
        dataObjectTmp.textIsStrike =true
        dataObjectTmp.tabTag.splice(dataObjectTmp.tabTag.indexOf("active"), 1);

        dataObjectTmp.tabTag.push("completed");
      }
    },
    filterTodoItem(tag,event) {
      this.tabTodoItem.forEach((elt) => {
        if (!elt.tabTag.includes(tag)) {
          elt.display = false;
        }else{
          elt.display = true;
        }
      });
      let tabSpan = Array.from(document.getElementsByClassName('tag'));

      tabSpan.forEach(elt=>{
        if(elt != event.target){
          if(elt.classList.contains('blueTag')){
            elt.classList.remove('blueTag')
          }
        }else{
          if(!elt.classList.contains('blueTag'))
          elt.classList.add('blueTag')
        }
      })
    },
    clearCompleted(){
      for(let i = this.tabTodoItem.length-1;i>=0;i--){
        if(this.tabTodoItem[i].tabTag.includes('completed')){

          this.tabTodoItem.splice(i,1);
        }
      }
    }
  },
  computed: {
    numberItem() {
      return this.tabTodoItem.length;
    },
  },
};
</script>

<style lang="scss">
#app {
  min-height: 100vh;
  min-width: 100vw;
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: url("./assets/bg-desktop-light.jpg") no-repeat;
  background-color: rgb(236, 234, 234);
  background-blend-mode: multiply;
  background-size: contain;
  margin: 0;
  padding: 0;
  * {
    font-family: "Commissioner", sans-serif;
  }
  .main-container {
    width: 35vw;
    height: fit-content;
    min-height: 70vh;
    border: 2px solid;
    .header {
      display: flex;
      margin-bottom: 30px;
      > * {
        width: 50%;
      }

      .container-todo {
        span {
          letter-spacing: 0.6rem;
          color: white;
          text-transform: uppercase;
          font-weight: bold;
          font-size: 40px;
        }
      }
      .containerDay-Night {
        display: flex;
        justify-content: flex-end;
        align-items: center;
        img {
          height: 25px;
          width: 25px;
        }
        img:hover {
          cursor: url("data:image/x-icon;base64,AAACAAEAICACAAAAAAAwAQAAFgAAACgAAAAgAAAAQAAAAAEAAQAAAAAAgAAAAAAAAAAAAAAAAgAAAAAAAAAAAAAA////AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/gAAAf4AAAPVAAAH1QAAB9WAAA3VgAAd/4AAGbaAAAG2gAABtgAAAYAAAAGAAAABgAAAAYAAAAAAAAA//////////////////////////////////////////////////////////////////////////////////////gD///4A///8AP//+AB///AAf//wAD//4AA//8AAP//AAD//5AA///wAf//8Af///D////w////8P////n///8="),
            auto;
        }
      }
    }
    .newTodo {
      background-color: white;
      min-height: 40px;
      display: flex;
      align-items: center;
      padding-left: 20px;
      border-radius: 5px;
      margin: 20px 0;

      .input-text {
        border: none;
        outline: none;
        display: flex;
        margin-left: 5px;
      }
      .input-radio {
        height: 17px;
        width: 17px;
      }
    }
    .container-todolist {
      background-color: white;
      min-height: 50px;
      border-radius: 5px;
    }
    .container-options {
      display: flex;
      align-items: center;
      background-color: white;
      min-height: 40px;
      * {
        color: gray;
        font-size: 11px;
        font-weight: bold;
      }
      .item-left {
        width: 30%;
        display: flex;
        justify-content: center;
        align-items: center;
      }
      .option-filters {
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        width: 60%;

        span:hover {
          cursor: url("data:image/x-icon;base64,AAACAAEAICACAAAAAAAwAQAAFgAAACgAAAAgAAAAQAAAAAEAAQAAAAAAgAAAAAAAAAAAAAAAAgAAAAAAAAAAAAAA////AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/gAAAf4AAAPVAAAH1QAAB9WAAA3VgAAd/4AAGbaAAAG2gAABtgAAAYAAAAGAAAABgAAAAYAAAAAAAAA//////////////////////////////////////////////////////////////////////////////////////gD///4A///8AP//+AB///AAf//wAD//4AA//8AAP//AAD//5AA///wAf//8Af///D////w////8P////n///8="),
            auto;
          color: rgb(56, 56, 218);
        }
        .blueTag{
          color: rgb(56, 56, 218);
        }
      }
      .clear-container {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 30%;
        span:hover {
          cursor: url("data:image/x-icon;base64,AAACAAEAICACAAAAAAAwAQAAFgAAACgAAAAgAAAAQAAAAAEAAQAAAAAAgAAAAAAAAAAAAAAAAgAAAAAAAAAAAAAA////AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/gAAAf4AAAPVAAAH1QAAB9WAAA3VgAAd/4AAGbaAAAG2gAABtgAAAYAAAAGAAAABgAAAAYAAAAAAAAA//////////////////////////////////////////////////////////////////////////////////////gD///4A///8AP//+AB///AAf//wAD//4AA//8AAP//AAD//5AA///wAf//8Af///D////w////8P////n///8="),
            auto;
          color: rgb(56, 56, 218);
        }
      }
    }
  }
  p {
    text-align: center;
    font-size: 12px;
    color: gray;
    font-weight: bold;
  }
}

</style>
