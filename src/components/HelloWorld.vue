<!-- eslint-disable vue/no-export-in-script-setup -->
<template>
  <div>
    <card class="card-section" style="width: 650px; margin: auto">
      <h1>
        Manage your Task
        <span class="k-icon k-i-track-changes" id="icon"></span>
      </h1>
      <hr />
      <div class="list">
        <li
          v-for="(task, index) in todoTask"
          :key="index"
          :class="{ removed: task.checked }"
        >
          <div class="form-box">
            <input type="checkbox" v-model="task.checked" class="check-box" />
            <label class="heading">
              {{ task.text }}
            </label>
            <br />
            <label class="paragraph">
              {{ task.description }}
            </label>
            <div class="icon-wrapper">
              <KButton
                :icon="'trash'"
                :fill-mode="'outline'"
                class="btn-func"
                v-on:click="removeSingleTask(index)"
                >Delete
              </KButton>
            </div>
          </div>
        </li>
      </div>
    </card>

    <card class="container-card" style="width: 650px; margin: auto">
      <div class="form-group">
        <KInput
          class="form-input"
          :style="{ width: '490px' }"
          v-model="newTaskList"
          name="task name"
          :icon="'plus'"
          :fill-mode="'outline'"
          placeholder="Write a new task"
        >
        </KInput>
      </div>
      <div class="form-group">
        <KInput
          class="form-input"
          :style="{ width: '490px' }"
          v-model="desTaskList"
          name="description"
          placeholder="Description"
        ></KInput>
      </div>
      <div class="col-xs-12 col-sm-6 example-col">
        <div class="btn-func">
          <KButton
            :icon="'plus'"
            :fill-mode="'outline'"
            class="btn-func"
            id="btn-func"
            @click="addNewTask"
          >
            Add Task</KButton
          >
        </div>
      </div>
    </card>
  </div>
</template>

<script>
import { Card } from "@progress/kendo-vue-layout";
// ES2015 module syntax
import { Input } from "@progress/kendo-vue-inputs";
import "@progress/kendo-theme-default";
import { Button } from "@progress/kendo-vue-buttons";
export default {
  name: "CardComponent",
  components: {
    card: Card,
    KInput: Input,
    KButton: Button,
  },
  data() {
    return {
      todoTask: [],
      newTaskList: "",
      desTaskList: "",
    };
  },
  methods: {
    addNewTask() {
      this.todoTask.push({
        text: this.newTaskList,
        description: this.desTaskList,
        checked: false,
      });
      this.newTaskList = "";
      this.desTaskList = "";
    },
    removeSingleTask(index) {
      this.todoTask.splice(index, 1);
    },
  },
};
</script>

<style>
.form-input {
  margin: 10px 15px;
  border-radius: 0px;
  padding: 10px 0px;
}

#icon {
  font-size: 15px !important;
}

.container-card {
  margin-top: 40px;
}

.btn-func {
  margin: 10px 20px;
  padding: 10px 15px;
}

#btn-func {
  background-color: #424242;
  color: white;
}

.removed label {
  text-decoration: line-through;
}

.form-box {
  text-align: left;
  padding: 10px 20px;
  border: 1px solid #424242;
  width: 500px;
  margin: 30px 60px;
}

li {
  list-style-type: none;
}

.heading {
  font-size: 20px;
  font-weight: bold;
}

.paragraph {
  font-size: 15px;
  padding-left: 25px;
}

.icon {
  font-size: 25px;
}

.check-box {
  /* position: absolute;
top: 0;
left: 0; */
  height: 20px;
  width: 20px;
  background-color: #eee;
  margin: 10px 0px;
}
</style>
