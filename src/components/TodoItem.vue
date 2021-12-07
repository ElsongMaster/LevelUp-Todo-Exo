<template>
  <div v-if="dataObject.display" class="mainContent all">
    <div class="container-input">
      <input
        type="radio"
        :id="classNameItem"
        name="drone"
        value="huey"
        class="input-radio"
        @click="selectObject(dataObject.index, $event)"
      />
      <label
        v-if="dataObject.isSelected"
        :id="classNameItem"
        :for="classNameItem"
        ><i class="fas fa-check"></i
      ></label>
    </div>
    <div class="container-text">
      <p v-if="dataObject.textIsStrike" class="text-create textStrike">{{ dataObject.text }}</p>
      <p v-else class="text-create">{{ dataObject.text }}</p>
    </div>
    <div class="close-container">
      <img
        @click="deleteObject(dataObject.index)"
        src="../assets/icon-cross.svg"
        alt=""
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    dataObject: Object,
  },
  computed: {
    classNameItem() {
      return "Item-" + this.dataObject.index;
    },
  },

  methods: {
    deleteObject(index) {
      console.log(index);
      this.$emit("setIndexObject", index);
    },
    selectObject(index, event) {
      console.log(event.target);
      event.target.checked = false;
      console.log(index);
      this.$emit("checkRadio", index);
    },
  },
};
</script>

<style scoped lang="scss">
.mainContent {
  display: flex;
  border-bottom: 1px solid rgb(209, 209, 209);
  .container-input {
    width: 10%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;

    input {
      height: 17px;
      width: 17px;
    }
    label {
      height: 17px;
      width: 17px;
      background: linear-gradient(hsl(192, 100%, 67%), hsl(280, 87%, 65%));
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 50%;
      position: absolute;
      left: 15px;
      i {
        padding: 0;
      }
    }
    label:hover {
      cursor: url("data:image/x-icon;base64,AAACAAEAICACAAAAAAAwAQAAFgAAACgAAAAgAAAAQAAAAAEAAQAAAAAAgAAAAAAAAAAAAAAAAgAAAAAAAAAAAAAA////AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/gAAAf4AAAPVAAAH1QAAB9WAAA3VgAAd/4AAGbaAAAG2gAABtgAAAYAAAAGAAAABgAAAAYAAAAAAAAA//////////////////////////////////////////////////////////////////////////////////////gD///4A///8AP//+AB///AAf//wAD//4AA//8AAP//AAD//5AA///wAf//8Af///D////w////8P////n///8="),
        auto;
    }
    input:hover {
      cursor: url("data:image/x-icon;base64,AAACAAEAICACAAAAAAAwAQAAFgAAACgAAAAgAAAAQAAAAAEAAQAAAAAAgAAAAAAAAAAAAAAAAgAAAAAAAAAAAAAA////AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/gAAAf4AAAPVAAAH1QAAB9WAAA3VgAAd/4AAGbaAAAG2gAABtgAAAYAAAAGAAAABgAAAAYAAAAAAAAA//////////////////////////////////////////////////////////////////////////////////////gD///4A///8AP//+AB///AAf//wAD//4AA//8AAP//AAD//5AA///wAf//8Af///D////w////8P////n///8="),
        auto;
      border-color: linear-gradient(hsl(192, 100%, 67%), hsl(280, 87%, 65%));
      border-width: 4px;
    }
  }
  .container-text {
    width: 70%;
    padding-left: 10px;

    p {
      display: inline-block;
      text-align: left;
      padding: 0;
      justify-content: flex-end;
    }
  }
  .close-container {
    width: 10%;
    // border: 2px solid;
    display: flex;
    justify-content: center;
    align-items: center;
    img {
      display: none;
      color: rgb(228, 225, 225);
    }
  }
}
.mainContent:hover {
  cursor: url("data:image/x-icon;base64,AAACAAEAICACAAAAAAAwAQAAFgAAACgAAAAgAAAAQAAAAAEAAQAAAAAAgAAAAAAAAAAAAAAAAgAAAAAAAAAAAAAA////AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/gAAAf4AAAPVAAAH1QAAB9WAAA3VgAAd/4AAGbaAAAG2gAABtgAAAYAAAAGAAAABgAAAAYAAAAAAAAA//////////////////////////////////////////////////////////////////////////////////////gD///4A///8AP//+AB///AAf//wAD//4AA//8AAP//AAD//5AA///wAf//8Af///D////w////8P////n///8="),
    auto;
  img {
    display: flex;
  }
}

.mainContent{
  .textStrike{
    text-decoration: line-through;
    color: rgb(223, 217, 217) !important;
  }
}


</style>
