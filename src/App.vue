<template>
  <div id="app">
    <el-card class="login-card">
      <lottie class="login-lottie" :options="welcomeLottie" :height="300" :width="300" :animCreated="handleAnimation"/>
      <div class="login-title">ログイン</div>
      <el-form :model="loginForm">
          <el-form-item label="メールアドレス" prop="email">
              <el-input type="text" v-model="loginForm.email" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="パスワード" prop="password">
              <el-input type="password" v-model="loginForm.password" autocomplete="off"></el-input>
          </el-form-item>
          <el-button type="primary" :loading="checking" @click="handleLogin">ログイン</el-button>
      </el-form>
    </el-card>
    <!-- ダイアログ追加 -->
    <el-dialog :visible.sync="dialogTableVisible">
      <div class="login-title">Welcome</div>
      <!-- 花火のアニメーション -->
      <lottie :options="fireworksLottie" :height="300" :width="300" :animCreated="handleAnimation"/>
    </el-dialog>
  <sample/>
  </div>

</template>

<script>
import Lottie from "@/components/Lottie.vue"
import * as welcome from "@/assets/welcome.json"
// 花火のアニメーション
import * as fireworks from "@/assets/fireworks.json"
import Sample from "@/components/Sample.vue"

export default {
  name: 'app',
  components: {
    Lottie,
    Sample
  },
  data () {
    return {
      checking: false,
      dialogTableVisible: false,
      loginForm: {
        email: '',
        password: '',
      }
    }
  },
  computed: {
    welcomeLottie () {
      return { animationData: welcome }
    },
    fireworksLottie () {
      return { animationData: fireworks }
    }
  },
  methods: {
    handleAnimation (anim) {
      this.anim = anim
    },
    handleLogin() {
      this.checking = true
      // 演出のためです...。追加しました。
      setTimeout(() => {
        this.checking = false
        this.dialogTableVisible = true
      }, 1000)
    }
  }
}
</script>

<style>
  body {
    text-align: center;
    background-color: #E0EAF6;
  }

  .login-title {
    font-size: 32px;
    font-weight: 600;
    margin-bottom: 20px;
  }

  .login-card {
    max-width: 800px;
    margin: 200px auto 0;
    padding: 120px 0 20px;
  }

  .login-lottie {
    position: absolute;
    top: 32px;
    right: 0;
    bottom: 0;
    left: 0;
    margin: 0 auto;
  }
</style>
