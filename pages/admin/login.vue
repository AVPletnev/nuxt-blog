<template>
  <el-card shadow="always" :style="{width: '500px'}">
    <el-form :model="controls" :rules="rules" ref="form" @submit.native.prevent="onSubmit">
      <h1>Добавить комментарий</h1>
      <el-form-item label="Логин" prop="login">
        <el-input v-model.trim="controls.login" />
      </el-form-item>
      <div class="mb-2">
        <el-form-item label="пароль" prop="password">
          <el-input v-model.trim="controls.password" type="password" />
        </el-form-item>
      </div>
      <el-form-item>
        <el-button type="primary" :loading="loading" native-type="submit" round>Войти</el-button>
      </el-form-item>
    </el-form>
  </el-card>
</template>

<script>
export default {
  layout: "empty",
  data() {
    return {
      loading: false,
      controls: {
        login: "",
        password: ""
      },
      rules: {
        login: [
          {
            required: true,
            message: "Введите логин",
            trigger: "blur"
          }
        ],
        password: [
          {
            required: true,
            message: "Введите пароль",
            trigger: "blur"
          },
          {
            min: 6,
            message: "Пароль должен быть не менее 6 символов",
            trigger: "blue"
          }
        ]
      }
    };
  },
  methods: {
    onSubmit() {
      this.$refs.form.validate(async valid => {
        if (valid) {
          this.loading = true;
          try {
            const formData = {
              login: this.controls.login,
              password: this.controls.password
            };

            await this.$store.dispatch('auth/login', formData)
            this.$router.push('/admin')

          } catch (e) {
             this.loading = false;
          }
        }
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.mb {
  margin-bottom: 1rem;
}
.mb-2 {
  margin-bottom: 2rem;
}
</style>