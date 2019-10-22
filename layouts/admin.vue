<template>
  <div class="admin-loyout">
    <el-container :style="{height: '100%'}">
      <el-aside>
        <app-aside />
      </el-aside>
      <el-main>
        <nuxt />
      </el-main>
    </el-container>
  </div>
</template>

<script>
import AppAside from '@/components/admin/Aside'
export default {
  components: {AppAside}
};
</script>

<style lang="scss" scoped>
.admin-loyout {
  height: 100vh;
  width: 100%;
}
</style>