<template>
  <div>
    <el-container>
      <el-header class="p-0">
        <HeaderComponent />
      </el-header>
      <el-container style="height: 850px">
        <el-aside width="20em" style="border: 1px solid var(--el-border-color)">
          <el-menu default-active="1" class="el-menu-vertical-demo" @select="loadSomething">
            <el-menu-item index="1">
              <template #title>
                <el-icon><TrophyBase /></el-icon>
                <span>Лучшее</span>
              </template>
            </el-menu-item>
            <el-menu-item index="2">
              <el-icon><View /></el-icon>
              <span>Новое</span>
            </el-menu-item>
            <el-menu-item index="3">
              <el-icon><VideoPlay /></el-icon>
              <span>Рекомендации</span>
            </el-menu-item>
            <el-menu-item index="4">
              <el-icon><Star /></el-icon>
              <span>Понравившееся</span>
            </el-menu-item>
            <el-menu-item index="5">
              <el-icon><Collection /></el-icon>
              <span>Сохраненное</span>
            </el-menu-item>
            <el-menu-item index="6">
              <el-icon><Film /></el-icon>
              <span>Мои видео</span>
            </el-menu-item>
          </el-menu>
        </el-aside>

        <el-main v-loading="isDataLoading" style="border: 1px solid var(--el-border-color)">
          <ul
            v-if="!isDataLoading"
            v-infinite-scroll="load"
            class="infinite-list"
            style="overflow: auto"
          >
            <VideoComponent
              v-for="i in count"
              :key="i"
              class="infinite-list-item"
              style="margin-bottom: 30px"
            />
          </ul>
        </el-main>
        <el-aside width="25em" style="border: 1px solid var(--el-border-color)">
          <el-check-tag
            v-for="category in categories"
            :key="category"
            :label="category"
            class="ms-2 mt-2"
            type="success"
            size="large"
            v-model="checkedTags"
            :checked="checkedTags.includes(category)"
            @change="toggleTag(category)"
            round
            >{{ category }}</el-check-tag
          >
        </el-aside>
      </el-container>
    </el-container>
  </div>
</template>

<script setup lang="ts">
import { VideoPlay } from '@element-plus/icons-vue'
import 'element-plus/es/components/message/style/css'
import { ref, onMounted } from 'vue'
import VideoComponent from '@/components/VideoComponent.vue'
import HeaderComponent from '@/components/HeaderComponent.vue'

const categories = ref([
  'Спорт',
  'Искусство',
  'Анимация',
  'Фильмы',
  'Мемы',
  'Животные',
  'Мода и красота'
])

function delay(ms: number) {
  return new Promise((resolve) => setTimeout(resolve, ms))
}

const isDataLoading = ref(false)
const loadSomething = async () => {
  console.log('loading')
  isDataLoading.value = true
  await delay(2000)
  isDataLoading.value = false
  console.log('done loading')
}

const checkedTags = ref(new Array() as Array<string>)

const toggleTag = (category: any) => {
  checkedTags.value.includes(category)
    ? checkedTags.value.splice(checkedTags.value.indexOf(category), 1)
    : checkedTags.value.push(category)
}

const count = ref(0)
const load = () => {
  count.value += 2
}

onMounted(() => {
  console.log(categories.value)
})
</script>

<style scoped>
.infinite-list {
  height: 100%;
  padding: 0;
  margin: 0;
  list-style: none;
}
</style>
