<template>
  <div>
    <header
      class="relative z-10 flex items-center justify-between bg-gradient-to-b from-primary"
    >
      <span class="flex-1" />
      <nuxt-link to="/" class="flex-1 flex justify-center">
        <img src="/chessboxingdb-logo.svg" alt="logo" class="h-20" />
      </nuxt-link>

      <div v-if="checkTokenExists()" class="flex-1 flex justify-end">
        <Icon
          icon="material-symbols:logout"
          class="mr-4 mb-2 cursor-pointer"
          @click="removeToken()"
          width="2rem"
        />
      </div>

      <NuxtLink v-else to="/login" class="flex-1 flex justify-end">
        <Icon icon="material-symbols:login" class="mr-4 mb-2" width="2rem" />
      </NuxtLink>
    </header>
    <NavigationMenu class="mx-auto">
      <NavigationMenuList>
        <NuxtLink to="/events">
          <NavigationMenuLink :class="navigationMenuTriggerStyle()">
            Events
          </NavigationMenuLink>
        </NuxtLink>
        <NuxtLink to="/results">
          <NavigationMenuLink :class="navigationMenuTriggerStyle()">
            Results
          </NavigationMenuLink>
        </NuxtLink>
        <NuxtLink to="/fighters">
          <NavigationMenuLink :class="navigationMenuTriggerStyle()">
            Fighters
          </NavigationMenuLink>
        </NuxtLink>
        <NuxtLink to="/compare">
          <NavigationMenuLink :class="navigationMenuTriggerStyle()">
            <div class="relative">
              <span> Compare </span>
              <Crown class="w-4 stroke-yellow-400 absolute -right-2.5 -top-3 rotate-[25deg]" />
            </div>
          </NavigationMenuLink>
        </NuxtLink>
      </NavigationMenuList>
    </NavigationMenu>
    <slot />
  </div>
</template>

<script setup>
import { Icon } from "@iconify/vue";
import { Crown } from "lucide-vue-next";
import { navigationMenuTriggerStyle } from "@/components/ui/navigation-menu";

const config = useRuntimeConfig();

console.log(config.public.baseUrl);

function checkTokenExists() {
  const token = localStorage.getItem("token");
  return !!token;
}

function removeToken() {
  localStorage.removeItem("token");
  window.location.reload();
}
</script>
