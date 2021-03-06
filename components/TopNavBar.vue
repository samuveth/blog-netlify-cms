<template>
  <div class="relative w-full px-4 lg:px-10 py-4 md:py-8 flex justify-between">
    <transition
      enter-active-class="transition ease-out duration-100 transform"
      enter-class="opacity-0 scale-98"
      enter-to-class="opacity-100 scale-100"
      leave-active-class="transition ease-in duration-500 transform"
      leave-class="opacity-100 scale-100"
      leave-to-class="opacity-0 scale-98"
    >
      <nav v-if="openNav" class="absolute w-full h-screen bg-white z-40">
        <div class="mt-20 space-y-4">
          <nuxt-link
            class="flex"
            v-for="page in pages"
            :key="page.length"
            :to="page.link"
          >
            <button
              @click="openNav = !openNav"
              class="font-medium px-3 py-1 hover:bg-gray-200 rounded-md focus:outline-none"
              :class="isSelected(page)"
            >
              {{ page.name }}
            </button>
          </nuxt-link>
        </div>
      </nav>
    </transition>
    <div class="flex items-center z-50">
      <topNavMenu
        :isOpen="openNav"
        @open-nav="openNav = !openNav"
        class="lg:hidden z-50"
      />
      <nuxt-link to="/">
        <h1 class="uppercase text-xl font-medium tracking-wider">Vallon</h1>
      </nuxt-link>
    </div>
    <div class="space-x-8 hidden lg:block">
      <nuxt-link v-for="(page, i) in pages" :key="i" :to="page.link">
        <button
          class="font-medium text-sm px-3 py-1 hover:bg-gray-200 rounded-md focus:outline-none"
          :class="isSelected(page)"
        >
          {{ page.name }}
        </button>
      </nuxt-link>
    </div>
    <div class="flex items-center space-x-5">
      <button
        v-for="(item, index) in social"
        :key="index"
        class="focus:outline-none text-xs font-medium"
        :class="item.color"
        @click="openSocial(item.link)"
      >
        {{ item.icon }}
      </button>
    </div>
  </div>
</template>

<script>
import TopNavMenu from './TopNavMenu.vue'
export default {
  components: {
    TopNavMenu,
  },
  data() {
    return {
      openNav: false,
      pages: [
        { name: 'Home', link: '/' },
        { name: 'Portraits', link: '/portraits' },
        { name: 'Nature', link: '/nature' },
      ],
      social: [
        {
          name: 'Github',
          link: 'https://github.com/pywei088',
          icon: 'GH',
          color: 'text-gray-800',
        },
        {
          name: 'Facebook',
          link: 'https://facebook.com',
          icon: 'FB',
          color: 'text-blue-600',
        },
        {
          name: 'Twitter',
          link: 'https://twitter.com',
          icon: 'TW',
          color: 'text-blue-400',
        },
      ],
    }
  },
  methods: {
    isSelected(page) {
      return {
        'bg-gray-200': this.$nuxt.$route.path === page.link,
      }
    },
    openSocial(link) {
      window.open(link, '_blank')
    },
  },
}
</script>
