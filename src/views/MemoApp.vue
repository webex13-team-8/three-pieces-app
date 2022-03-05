<template>
  <h1>Vue メモ</h1>
  <div class="memo-list">
    <ul class="memo-list__container">
      <li v-for="(todo, index) in allMemos" :key="index" class="memo">
        <input type="checkbox" v-model="todo.isDone" />
        <span v-bind:class="{ Done: todo.isDone }">
          <div class="memo__text">{{ todo.item }}</div>
        </span>
        <button class="memo__delete" v-on:click="deleteMemo(index)">
          削除
        </button>
      </li>
    </ul>
    <div class="add-memo-field">
      <input
        class="add-memo-field__input"
        v-model="text"
        type="text"
        @input="onInput"
      />
      <button
        class="add-memo-field__button"
        v-on:click="addMemo"
        :disabled="activateSubmit"
      >
        追加
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: "",
      allMemos: [],
      isDone: false,
      activateSubmit: true,
    }
  },
  methods: {
    addMemo: function () {
      var todo = {
        item: this.text,
        isDone: false,
      }
      this.allMemos.push(todo)
      this.text = ""
      this.activateSubmit = true
      console.log(this.allMemos)
    },

    deleteMemo: function (index) {
      this.allMemos.splice(index, 1)
    },

    swichisDone: function () {
      this.isDone = !this.isDone
    },

    onInput(e) {
      console.log(e.target.value)
      if (e.target.value.length === 0) {
        this.activateSubmit = true
      } else if (e.target.value.length !== 0) {
        this.activateSubmit = false
      }
    },
  },
}
</script>

<style scoped>
.memo-list {
  padding-left: 5rem;
  padding-right: 5rem;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  max-width: 512px;
  margin-left: auto;
  margin-right: auto;
}

.memo-list__container {
  padding: 0;
}

.memo {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem;
  border-radius: 5px;
}

.memo:hover {
  color: white;
  background-color: #b23b61;
}

.memo__text {
  margin-left: 2rem;
  text-align: left;
}

li > span.Done {
  text-decoration-line: line-through;
}

.memo__delete {
  margin-left: 1rem;
  padding: 0.5rem 0.5rem;
  border: solid 1px black;
  border-radius: 5px;
  background-color: white;
}

.memo__delete:hover {
  background-color: #b2ae3b;
  border-radius: 5px;
}

.add-memo-field {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.add-memo-field__input {
  padding: 10px;
}
.add-memo-field__button {
  padding: 0.5rem 0.5rem;
  border: solid 1px black;
  border-radius: 5px;
  background-color: white;
}

.add-memo-field__button:hover {
  background-color: #b2ae3b;
  border-radius: 5px;
}
</style>
