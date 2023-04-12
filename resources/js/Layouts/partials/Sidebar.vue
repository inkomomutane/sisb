<template>
  <div>
    <!-- Sidebar backdrop (mobile only) -->
    <div class="fixed inset-0 bg-slate-900 bg-opacity-30 z-40 lg:hidden lg:z-auto transition-opacity duration-200" :class="sidebarOpen ? 'opacity-100' : 'opacity-0 pointer-events-none'" aria-hidden="true"></div>

    <!-- Sidebar -->
    <div id="sidebar" ref="sidebar"
    class="flex flex-col absolute z-40 left-0 top-0 lg:static lg:left-auto lg:top-auto lg:translate-x-0 h-screen overflow-y-scroll lg:overflow-y-auto no-scrollbar w-64 lg:w-20 lg:sidebar-expanded:!w-64 2xl:!w-64 shrink-0 bg-slate-800 p-4 transition-all duration-200 ease-in-out"
    :class="sidebarOpen ? 'translate-x-0' : '-translate-x-64'">
      <!-- Sidebar header -->
      <div class="flex justify-between mb-10 pr-3 sm:px-2 align-middle">
        <!-- Close button -->
        <button ref="trigger" class="lg:hidden text-slate-500 hover:text-slate-400" @click.stop="$emit('close-sidebar')" aria-controls="sidebar" :aria-expanded="sidebarOpen">
          <span class="sr-only">Close sidebar</span>
          <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path d="M10.7 18.7l1.4-1.4L7.8 13H20v-2H7.8l4.3-4.3-1.4-1.4L4 12z" />
          </svg>
        </button>
        <!-- Logo -->
        <div :class="`${sidebarExpanded ? 'block' : 'md:hidden'}`">
           <img src="@/images/logo/logo.svg" alt="Logo" width="32" height="32">
        </div>
        <!-- Expand / collapse button -->
      <div class="hidden lg:inline-flex 2xl:hidden justify-end mt-auto">
        <div class="px-3 py-2">
          <button @click.prevent="sidebarExpanded = !sidebarExpanded">
            <span class="sr-only">Expand / collapse sidebar</span>

            <svg   class="w-6 h-6 fill-current sidebar-expanded:-rotate-180" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none">
              <path   class="text-gray-400"   opacity="0.3" d="M12.9 10.7L3 5V19L12.9 13.3C13.9 12.7 13.9 11.3 12.9 10.7Z" />
              <path   class="text-slate-400"   d="M21 10.7L11.1 5V19L21 13.3C22 12.7 22 11.3 21 10.7Z" />
              </svg>
          </button>
        </div>
      </div>
      </div>

      <!-- Links -->
      <div class="space-y-8">
        <!-- Pages group -->
        <div>
          <h3 class="text-xs uppercase text-slate-500 font-semibold pl-3">
            <span class="hidden lg:block lg:sidebar-expanded:hidden 2xl:hidden text-center w-6" aria-hidden="true">•••</span>
            <span class="lg:hidden lg:sidebar-expanded:block 2xl:block">Pages</span>
          </h3>
          <ul class="mt-3">
            <!-- Dashboard -->

            <li class="px-3 py-2 rounded mb-0.5 last:mb-0 bg-slate-950" >
                <a class="block text-slate-200 truncate transition duration-150"  >
                  <div class="flex items-center justify-between">
                    <div class="grow flex items-center">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" >
                      <rect class="fill-current text-gray-100"  x="2" y="2" width="9" height="9" rx="2" />
                      <rect class="fill-current text-indigo-300" opacity="0.3" x="13" y="2" width="9" height="9" rx="2" />
                      <rect class="fill-current text-indigo-300" opacity="0.3" x="13" y="13" width="9" height="9" rx="2" />
                      <rect class="fill-current text-indigo-300" opacity="0.3" x="2" y="13" width="9" height="9" rx="2" />
                    </svg>
                      <span class="text-sm font-medium ml-3 lg:opacity-0 lg:sidebar-expanded:opacity-100 2xl:opacity-100 duration-200">Dashboard</span>
                    </div>
                  </div>
                </a>
            </li>

            <li class="px-3 py-2 rounded-md mb-0.5 last:mb-0" >
                <a class="block text-slate-200 truncate transition duration-150" >
                  <div class="flex items-center justify-between">
                    <div class="grow flex items-center">
                      <svg class="shrink-0 h-6 w-6" viewBox="0 0 24 24">
                        <path class="fill-current text-slate-500 " d="M14.5 7c4.695 0 8.5 3.184 8.5 7.111 0 1.597-.638 3.067-1.7 4.253V23l-4.108-2.148a10 10 0 01-2.692.37c-4.695 0-8.5-3.184-8.5-7.11C6 10.183 9.805 7 14.5 7z" />
                        <path class="fill-current text-slate-400" d="M11 1C5.477 1 1 4.582 1 9c0 1.797.75 3.45 2 4.785V19l4.833-2.416C8.829 16.85 9.892 17 11 17c5.523 0 10-3.582 10-8s-4.477-8-10-8z" />
                      </svg>
                      <span class="text-sm font-medium ml-3 lg:opacity-0 lg:sidebar-expanded:opacity-100 2xl:opacity-100 duration-200">Messages</span>
                    </div>
                    <!-- Badge -->
                    <div class="flex flex-shrink-0 ml-2">
                      <span class="inline-flex items-center justify-center h-5 text-xs font-medium text-white bg-indigo-500 px-2 rounded">4</span>
                    </div>
                  </div>
                </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" >
import { ref, onMounted, onUnmounted, watch } from 'vue'
import SidebarLinkGroup from './SidebarLinkGroup.vue'

export default {
  name: 'Sidebar',
  props: ['sidebarOpen'],
  components: {
    SidebarLinkGroup,
  },
  setup(props, { emit }) {

    const trigger = ref<any>(null)
    const sidebar = ref<any>(null)
    const sidebarExpanded = ref(true)

    // close on click outside
    const clickHandler = ({ target }:{target:any}) => {
      if (!sidebar.value || !trigger.value) return
      if (
        !props.sidebarOpen ||
        sidebar.value.contains(target) ||
        trigger.value.contains(target)
      ) return new Event('close-sidebar')
    }

    // close if the esc key is pressed
    const keyHandler = ({ keyCode }:{keyCode:any}) => {
      if (!props.sidebarOpen || keyCode !== 27) return
      new Event('close-sidebar')
    }

    onMounted(() => {
      document.addEventListener('click', clickHandler)
      document.addEventListener('keydown', keyHandler)
      document.querySelector('body')?.classList.add('sidebar-expanded')

    })

    onUnmounted(() => {
      document.removeEventListener('click', clickHandler)
      document.removeEventListener('keydown', keyHandler)
    })

    watch(sidebarExpanded, () => {

      if (sidebarExpanded.value) {
        document.querySelector('body')?.classList.add('sidebar-expanded')
      } else {
        document.querySelector('body')?.classList.remove('sidebar-expanded')
      }
    })

    return {
      trigger,
      sidebar,
      sidebarExpanded,
    }
  },
}
</script>
