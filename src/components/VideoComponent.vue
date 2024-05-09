<template>
  <el-card style="width: 70%; margin: 0 auto">
    <el-container>
      <el-main
        style="
          border-bottom: 1px solid var(--el-border-color);
          height: 400px;
          display: flex;
          justify-content: space-around;
        "
      >
        <iframe width="420" height="350" src="src\assets\16788282428822.mp4"> </iframe>
      </el-main>
      <el-footer style="height: 100px">
        <div>
          <span style="font-size: 24px">{{ videoName }}</span>
        </div>
        <div>
          <span style="font-size: 20px">{{ user }}</span>
        </div>
        <div>
          <span>{{ comment }}</span>
        </div>
      </el-footer>
    </el-container>
  </el-card>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const videoName = ref('SomeVideoName')
const user = ref('SomeUser')
const comment = ref(
  'someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment someComment '
)
</script>
