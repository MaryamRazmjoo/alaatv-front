<template>
  <div class="header-container">
<!--    TODO => change bellow element's class name!-->
   <div class="idn">
     <div class="logo-header">
       <q-img src="img/logo/logo-image.png"/>
     </div>

     <div class="header-tabs">
       <q-btn-dropdown
         class="header-button-group"
         label="فیلم های پایه و کنکور آلاء"
         color="transparent"
         dropdown-icon="isax:arrow-down-1"
         text-color="dark"
         flat
       >
       </q-btn-dropdown>
       <q-btn-dropdown
         class="header-button-group"
         label="همایش کنکوری آلاء"
         color="transparent"
         dropdown-icon="isax:arrow-down-1"
         text-color="dark"
         flat
       >
       </q-btn-dropdown>
       <q-btn-dropdown
         class="header-button-group"
         label="متوسطه اول"
         color="transparent"
         dropdown-icon="isax:arrow-down-1"
         text-color="dark"
         flat
       >
       </q-btn-dropdown>
       <q-btn
         class="header-button-group"
         label="المپیاد"
         color="transparent"
         text-color="dark"
         flat
       >
       </q-btn>
     </div>
   </div>

    <div class="header-user-actions">
        <q-btn
          class="header-button-group cart-button"
          icon="isax:shopping-cart"
          color="transparent"
          text-color="dark"
          flat
        />
        <q-btn
          v-if="!isUserLogin"
          class="header-button-group login-button"
          label="ورود/ثبت نام"
          color="primary"
          text-color="accent"
          unelevated
        />
      <q-btn-dropdown
        class="header-button-group profile-button"
        color="transparent"
        icon="https://cdn.quasar.dev/img/avatar1.jpg"
        dropdown-icon="isax:arrow-down-1"
        text-color="dark"
        flat
      >
        <template v-slot:label>
          <div class="row items-center no-wrap">
            <q-icon left name="map" />
            <div class="text-center">
              Custom<br>Content
            </div>
          </div>
        </template>
      </q-btn-dropdown>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex'

export default {
  name: 'templateHeader',
  data() {
    return {
      user: {}
    }
  },
  mounted() {
    this.$store.commit('AppLayout/updateBreadcrumbLoading', false)
    this.$store.commit('AppLayout/updateVisibilityBreadcrumb', true)
    this.user = this.$store.getters['Auth/user']
    console.log(this.user)
  },
  computed: {
    isUserLogin () {
      return this.$store.getters['Auth/isUserLogin']
    }
  },
  methods: {

  }
}
</script>

<style lang="scss" scoped >
.header-container {
  display: flex;
  height: 72px;
  width: 100%;
  justify-content: space-between;
  .idn {
    display: flex;
    .logo-header {
      display: flex;
      align-items: center;
      width: 40px;
      margin-right: 40px;
    }

    .header-tabs {
      display: flex;
    }
  }

  .header-button-group {
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 24px;
    letter-spacing: -0.03em;
    margin-right: 24px;

    &:deep(.q-icon) {
      font-size: 10px;
    }

    &:deep(.q-btn-dropdown__arrow) {
      margin-left: 6px;
    }
  }

  .header-user-actions {
    display: flex;
   .cart-button {
     display: flex;
     margin-right: 48px;
     &:deep(.q-icon) {
       font-size: 21px;
     }
   }

    .login-button {
      margin: auto 0;
      height: 40px;
    }
  }

}
</style>
