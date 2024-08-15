<template>
  <q-layout view="lHh lpR fFf">
    <q-header>
      <q-toolbar :class="headerClass">
        <q-toolbar-title :class="textClass">
          LLaMa
          <q-btn
            @click="showing = true"
            flat
            icon="expand_more"
            style="margin-left: -19px"
          />
          <q-menu style="border-radius: 15px">
            <q-list dense style="min-width: 400px; height: 220px"> </q-list>
          </q-menu>
        </q-toolbar-title>
        <div>
          <q-toolbar-title
            size="5px"
            :class="textClass + ' absolute-center'"
            style="font-size: 15px"
          >
            Память заполнена
            <q-btn
              flat
              icon="error_outline"
              :class="textClass"
              style="margin-left: -15px; font-size: 10px"
            />
          </q-toolbar-title>
        </div>
        <div :class="textClass">
          <q-btn
            flat
            :style="{ color: isDarkMode ? 'white' : 'black', fontSize: '20px' }"
            rounded
            icon="brightness_6"
            @click="darkMode"
          />
          <q-btn
            no-caps
            dense
            :color="isDarkMode ? 'white' : 'black'"
            round
            icon="person"
            class="q-ml-md"
            @click="registerPage"
          />
        </div>
      </q-toolbar>
    </q-header>
    <q-drawer
      v-model="leftDrawerOpen"
      width="270"
      :breakpoint="1400"
      show-if-above
      bordered
      :class="drawerClass"
    >
      <q-scroll-area style="height: 100vh; max-width: 300px">
        <q-list>
          <q-item-label header> Something </q-item-label>

          <EssentialLink
            v-for="link in linksList"
            :key="link.title"
            v-bind="link"
          />
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { onMounted, ref, computed } from "vue";
import EssentialLink from "components/EssentialLink.vue";
import { useRouter } from "vue-router";
import { Dark } from "quasar";

const isDarkMode = ref(Dark.isActive);

const darkMode = () => {
  Dark.set(!Dark.isActive);
  isDarkMode.value = Dark.isActive;
};

onMounted(() => {
  isDarkMode.value = Dark.isActive;
});

const router = useRouter();
const registerPage = () => {
  router.push("/");
};

const showing = ref(false);

const headerClass = computed(() => (isDarkMode.value ? "bg-dark" : "bg-white"));
const textClass = computed(() =>
  isDarkMode.value ? "text-white" : "text-grey"
);
const drawerClass = computed(() => (isDarkMode.value ? "bg-dark" : ""));
</script>

<style scoped>
.bg-dark {
  background-color: #333;
}
.text-white {
  color: white;
}
</style>
