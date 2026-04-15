<script setup lang="ts">
import { ref, reactive, computed } from 'vue'
import { ALL_ITEMS } from '@/data/items.ts'

const items = ref([
  {
    id: 101,
    count: 1,
    checked: false,
  },
  {
    id: 100,
    count: 1,
    checked: true,
  },
  {
    id: 102,
    count: 3,
    checked: false,
  },
])

const toggleItem = (id: number) => {
  const item = items.value.find((x) => x.id === id)
  if (item) {
    item.checked = !item.checked
  }
}
</script>

<template>
  <ul class="list">
    <li class="line" v-for="item in items" :key="item.id" :class="{ checked: item.checked }">
      <label class="item">
        <span class="checkbox">
          <input
            class="checkbox-input"
            type="checkbox"
            :checked="item.checked"
            v-on:change="() => toggleItem(item.id)"
          />
          <span class="checkmark">
            <svg
              v-show="item.checked"
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <polyline points="20 6 9 17 4 12" />
            </svg>
          </span>
        </span>

        <span class="name"> {{ ALL_ITEMS[item.id].name }} – {{ item.count }}</span>
      </label>
    </li>
  </ul>

  <!--  <input />-->
  <!--  <button v-on:click="update">Add</button>-->
</template>

<style scoped>
.list {
  padding: 12px 24px;
  font-size: 16px;
  line-height: 1.2;
}
.line {
  all: unset;
  padding: 12px;
  display: block;
}
.item {
  all: unset;
  cursor: pointer;
  display: flex;
  gap: 2px;
  align-items: center;
  width: 100%;
}
.checkbox {
  position: relative;
  width: 14px;
  height: 14px;
  box-sizing: border-box;
  border-radius: 50%;
  border: 1px solid gray;
}
.checkbox-input {
  all: unset;
  display: block;
  width: 100%;
  height: 100%;
}
.checkmark {
  position: absolute;
  bottom: 2px;
  left: 2px;
  transform: translate(-25%, 25%);
  width: 24px;
  height: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.name {
  user-select: none;
}
.checked .name {
  font-style: italic;
  text-decoration: line-through;
}
</style>
