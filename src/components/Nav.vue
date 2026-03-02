<script>
export default {
    name: 'Nav',
    data() {
        return {
            mobileOpen: false, // Track mobile menu state
        };
    },
    methods: {
        goto(page) {
            this.$emit('goto', page);
            this.mobileOpen = false; // Close menu when navigating
        },
        toggleMobile() {
            this.mobileOpen = !this.mobileOpen;
        },
    },
};
</script>

<template>
    <nav class="fixed top-0 left-0 w-full z-50
              bg-white/10
              backdrop-blur-xl
              border-b border-white/20
              shadow-[0_8px_32px_rgba(0,0,0,0.35)]
              py-4 px-6 md:px-12
              flex justify-between items-center
              transition-all duration-300">

        <!-- Logo -->
        <div class="text-2xl font-bold text-[#4f6f52] font-display tracking-wider drop-shadow-[0_0_8px_#22d3ee]">
            Montevista Mission
        </div>

        <!-- Desktop Menu -->
        <ul class="hidden md:flex space-x-8 text-[#4f6f52] font-medium">
            <li><button @click="goto('home')"
                    class="hover:text-purple-400 hover:drop-shadow-[0_0_8px_#a855f7] transition duration-300 cursor-pointer">Home</button>
            </li>
            <li><button @click="goto('sermons')"
                    class="hover:text-purple-400 hover:drop-shadow-[0_0_8px_#a855f7] transition duration-300 cursor-pointer">Sermons</button>
            </li>
            <li><button @click="goto('events')"
                    class="hover:text-purple-400 hover:drop-shadow-[0_0_8px_#a855f7] transition duration-300 cursor-pointer">Events</button>
            </li>
            <li><button @click="goto('testimonies')"
                    class="hover:text-purple-400 hover:drop-shadow-[0_0_8px_#a855f7] transition duration-300 cursor-pointer">Testimonies</button>
            </li>
            <li><button @click="goto('Activities')"
                    class="hover:text-purple-400 hover:drop-shadow-[0_0_8px_#a855f7] transition duration-300 cursor-pointer">Activities</button>
            </li>
            <li><a href="#contact"
                    class="hover:text-purple-400 hover:drop-shadow-[0_0_8px_#a855f7] transition duration-300 cursor-pointer">Contact</a>
            </li>
        </ul>

        <!-- Mobile Icon -->
        <button @click="toggleMobile" class="md:hidden text-gray-100">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path v-if="!mobileOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M4 6h16M4 12h16M4 18h16" />
                <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
        </button>

        <!-- Mobile Menu -->
        <ul v-show="mobileOpen"
            class="absolute top-full left-0 w-full bg-white/90 backdrop-blur-xl border-t border-white/20 md:hidden flex flex-col text-gray-800 font-medium">
            <li class="border-b border-gray-200"><button @click="goto('home')"
                    class="w-full text-left py-3 px-6 hover:bg-purple-100">Home</button></li>
            <li class="border-b border-gray-200"><button @click="goto('sermons')"
                    class="w-full text-left py-3 px-6 hover:bg-purple-100">Sermons</button></li>
            <li class="border-b border-gray-200"><button @click="goto('events')"
                    class="w-full text-left py-3 px-6 hover:bg-purple-100">Events</button></li>
            <li class="border-b border-gray-200"><button @click="goto('testimonies')"
                    class="w-full text-left py-3 px-6 hover:bg-purple-100">Testimonies</button></li>
            <li class="border-b border-gray-200"><button @click="goto('Activities')"
                    class="w-full text-left py-3 px-6 hover:bg-purple-100">Activities</button></li>
            <li class="border-b border-gray-200"><a href="#contact"
                    class="w-full block py-3 px-6 hover:bg-purple-100">Contact</a></li>
        </ul>

    </nav>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Rajdhani:wght@500;700&display=swap');

.font-display {
    font-family: 'Rajdhani', sans-serif;
}
</style>