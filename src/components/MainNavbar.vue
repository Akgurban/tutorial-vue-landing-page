<template>
    <div class="flex justify-between ">
        <!-- desctop -->
        <div
            class="md:flex hidden flex-1 bg-red-500 py-[20px] px-[30px] gap-[50px] text-[#dae677] items-center justify-center">
            <router-link :to="item.path" v-for="(item, index) in links" :key="index"
                exact-active-class="underline bg-black">
                {{ item.name }}
            </router-link>
        </div>
        <!-- mobile -->
        <Transition name="fade">
            <div v-if="isNavbarOpen"
                class="md:hidden flex-1 flex flex-col w-screen h-screen bg-blue-500 py-[20px] px-[30px] gap-[50px] text-[#dae677] items-center justify-center">
                <router-link :to="item.path" v-for="(item, index) in links" :key="index" class="text-[46px]"
                    exact-active-class="underline bg-black">
                    {{ item.name }}
                </router-link>
            </div>
        </Transition>
        <div @click="toggleNavbar" class="md:hidden  block absolute top-10 right-10 w-10 h-10 bg-[#18e718]"></div>
    </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { useRoute, useRouter } from 'vue-router';
const isNavbarOpen = ref(false)

const route = useRoute()
const links = ref([
    { name: 'Home', path: "/" },
    { name: 'News', path: "/news" },
    { name: 'About', path: "/about" },
])
const toggleNavbar = () => {
    isNavbarOpen.value = !isNavbarOpen.value
}
watch(() => route.path, () => {
    isNavbarOpen.value = false
    console.log(route);

})

</script>

<style lang="scss" scoped></style>