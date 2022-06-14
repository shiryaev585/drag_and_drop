<template>
  <div class="wrapper">
    <div
      v-for="category in categories"
      :key="category.id"
      @drop="onDrop($event, category.id)"
      class="droppable"
      @dragover.prevent
      @dragenter.prevent
    >
      <h4>{{ category.title }}</h4>
      <div
        v-for="item in items.filter((x) => x.categoryId === category.id)"
        @dragstart="onDragStart($event, item)"
        class="draggable"
        draggable="true"
      >
        <h5>{{ item.title }}</h5>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { ref } from "vue";

export default {
  name: "App",
  setup() {
    const items = ref([
      {
        id: 0,
        title: "Vue",
        categoryId: 1,
      },
      {
        id: 1,
        title: "React",
        categoryId: 1,
      },
      {
        id: 2,
        title: "Angular",
        categoryId: 1,
      },
      {
        id: 3,
        title: "Laravel",
        categoryId: 1,
      },
      {
        id: 4,
        title: "JavaScript",
        categoryId: 0,
      },
      {
        id: 5,
        title: "PHP",
        categoryId: 0,
      },
      {
        id: 6,
        title: "C#",
        categoryId: 0,
      },
      {
        id: 7,
        title: "C++",
        categoryId: 0,
      },
      {
        id: 8,
        title: "Python",
        categoryId: 0,
      },
      {
        id: 9,
        title: "HTML",
        categoryId: 2,
      },
      {
        id: 10,
        title: "CSS",
        categoryId: 2,
      },
    ]);
    const categories = ref([
      {
        id: 0,
        title: "Programming language",
      },
      {
        id: 1,
        title: "Framework",
      },
      {
        id: 2,
        title: "Web",
      },
    ]);

    function onDragStart(e: DragEvent, item) {
      e.dataTransfer.dropEffect = "move";
      e.dataTransfer.effectAllowed = "move";
      e.dataTransfer.setData("itemId", item.id.toString());
    }

    function onDrop(e: DragEvent, categoryId) {
      const itemId = parseInt(e.dataTransfer.getData("itemId"));
      items.value = items.value.map((x) => {
        if (x.id == itemId) x.categoryId = categoryId;
        return x;
      });
    }

    return {
      items,
      categories,
      onDragStart,
      onDrop,
    };
  },
};
</script>

<style>
.wrapper {
  width: 100%;
  padding: 30px;
  display: flex;
  flex-wrap: wrap;
  background-color: #34495e;
}
.droppable {
  width: 200px;
  margin: 30px auto;
  padding: 15px;
  border-radius: 5px;
  background: #41b883;
}

.droppable h4 {
  color: #34495e;
}

.draggable {
  background: white;
  padding: 5px;
  border-radius: 5px;
  margin-bottom: 5px;
  cursor: pointer;
}

.draggable h5 {
  margin: 0;
}
</style>