<script setup>
//导入需要的对象import
import { ref, onMounted, computed } from 'vue'

//定义给页面用的响应数据
const name = ref()
//computed定义计算属性 默认是不能被修改（只读）
const isLogii = computed(() => {
  return name.value !== undefined
})
//定义方法   localStorage是本地存储
const getName = () => {
  return localStorage.getItem('auth_token')
}
const onLogout = () => {
  localStorage.removeItem('auth_token')
  window.location.href = './logon'
}
//onMounted是生命周期挂载后执行
onMounted(() => {
  name.value = getName()
})
</script>

<template>
  <nav class="app-topnav">
    <div class="container">
      <ui>
        <template v-if="isLogii">
          <li>
            <a href="javascript:;"><i class="iconfont icon-user"></i>{{ name }}</a>
          </li>
          <li>
            <el-popconfirm title="确认退出吗？" confirm-button-text="确认" cancel-butt>
              <template #reference>
                <a href="javascript:;" @click="onLogout"
                  ><i class="iconfont icon-exit"></i>退出登录</a
                >
              </template>
            </el-popconfirm>
          </li>
          <li>
            <a href="javascript:;"><i class="iconfont icon-vip"></i>会员中心</a>
          </li>
          <li>
            <a href="javascript: icon-;"><i class="iconfont icon-set"></i>我的订单</a>
          </li>
        </template>
        <template v-else>
          <li><RouterLink to="/logon">请先登录</RouterLink></li>
          <li><a href="javascript:;">帮助中心</a></li>
          <li><a href="javascript:;">关于我们</a></li>
        </template>
      </ui>
    </div>
  </nav>
</template>

<style scoped lang="scss">
$xtxColor: red;
.app-topnav {
  background-color: #000;

  ui {
    display: flex;
    height: 53px;
    justify-content: flex-end;
    align-items: center;

    li {
      a {
        padding: 0 15px;
        color: #cdcdcd;
        line-height: 1;
        display: inline-block;

        i {
          font-size: 14px;
          margin-right: 2px;
        }

        &:hover {
          color: $xtxColor;
        }
      }

      ~ li {
        a {
          border-left: 2px solid #666;
        }
      }
    }
  }
}
</style>
