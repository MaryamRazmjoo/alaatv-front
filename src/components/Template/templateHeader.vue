<template>
  <div class="header-container">
    <!--    TODO => change bellow element's class name!-->
    <div class="idn">
      <router-link
        to="/"
        class="logo-header"
      >
        <q-img src="img/logo/logo-image.png" />
      </router-link>

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
        @click="login"
      />
      <q-btn-dropdown
        v-else
        v-model="userMenu"
        class="header-button-group profile-button"
        color="transparent"
        dropdown-icon="isax:arrow-down-1"
        text-color="dark"
        dir="ltr"
        flat
      >
        <template v-slot:label>
          <q-avatar>
            <img src="https://nodes.alaatv.com/upload/images/profile/default_avatar.jpg">
          </q-avatar>
        </template>
        <q-list>
          <q-item
            :to="{name: 'User.Dashboard.purchases', params: {id: user.id}}"
            clickable
            v-close-popup
          >
            <q-item-section>فیلم ها و جزوه های من</q-item-section>
          </q-item>
          <q-item
            clickable
            v-close-popup
            @click="logout"
          >
            <q-item-section>خروج</q-item-section>
          </q-item>
        </q-list>
      </q-btn-dropdown>
    </div>
  </div>
</template>

<script>
export default {
  name: 'templateHeader',
  data () {
    return {
      user: {},
      userMenu: false
    }
  },
  mounted () {
    this.$store.commit('AppLayout/updateBreadcrumbLoading', false)
    this.$store.commit('AppLayout/updateVisibilityBreadcrumb', true)
    this.user = this.$store.getters['Auth/user']
  },
  computed: {
    isUserLogin () {
      return this.$store.getters['Auth/isUserLogin']
    }
  },
  methods: {
    login () {
      this.$router.push({ name: 'login' })
    },

    logout () {
      this.$store.dispatch('Auth/logOut')
    }
  }
}
</script>

<style lang="scss" scoped>
.header-container {
  display: flex;
  margin: auto;
  max-width: 1360px;
  height: 72px;
  width: 100%;
  justify-content: space-between;

  @media only screen and (max-width: 1439px) {
    padding: 0 30px;

  }

  .idn {
    display: flex;

    .logo-header {
      display: flex;
      align-items: center;
      width: 40px;
      margin-right: 40px;
    }

    @media only screen and (max-width: 1439px) {
      margin-right: 20px;
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

    @media only screen and (max-width: 1439px) {
      margin-right: 12px;
    }

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

    .profile-button {
      &:deep(.q-icon) {
        font-size: 14px;
      }

      &:deep(.q-btn-dropdown__arrow) {
        margin-right: 12px;
      }
    }
  }

}
</style>
