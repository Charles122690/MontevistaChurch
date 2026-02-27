<script>
export default {
    name: "Testimonies",
    data() {
        return {
            activeIndex: 0,
            interval: null,
            testimonies: [
                {
                    id: 1,
                    name: "Honey Biotumas",
                    image: "honey.png",
                    testimony:
                        "I struggled before. but when I put God first, He changed my life and filled it with joy.",
                    video: ""
                },
                {
                    id: 2,
                    name: "Edwin David",
                    image: "edwin.jpeg",
                    testimony:
                        "Through prayer meetings and gatherings, my faith became stronger than ever.",
                    video: ""
                },
                {
                    id: 3,
                    name: "Mizraem Bastasa",
                    image: "arem.png",
                    testimony:
                        "Montevista Mission helped restore my faith during a difficult season in my life.",
                    video: ""
                }
            ]
        };
    },
    mounted() {
        this.startCarousel();
    },
    beforeUnmount() {
        clearInterval(this.interval);
    },
    methods: {
        startCarousel() {
            this.interval = setInterval(() => {
                this.activeIndex =
                    (this.activeIndex + 1) % this.testimonies.length;
            }, 7000); // rotate every 7 seconds
        },
        selectIndex(index) {
            this.activeIndex = index;
        }
    }
};
</script>

<template>
    <section class="relative min-h-screen pt-32 pb-24 px-6 bg-gray-950 text-white overflow-hidden">

        <!-- Particle Background -->
        <div class="absolute inset-0">
            <canvas id="particle-bg" class="w-full h-full"></canvas>
        </div>

        <!-- Container -->
        <div class="relative max-w-6xl mx-auto text-center">

            <!-- Title -->
            <h2 class="text-4xl md:text-5xl font-extrabold text-transparent bg-clip-text 
                 bg-linear-to-r from-cyan-400 via-purple-400 to-blue-400 mb-16 tracking-wide">
                Life-Changing Testimonies
            </h2>

            <!-- Testimonial Cards -->
            <div class="flex flex-col md:flex-row items-center justify-center mt-20 gap-8">
                <div v-for="(item, index) in testimonies" :key="item.id" v-show="activeIndex === index" class="group relative w-full md:w-80 bg-white/5 backdrop-blur-xl
                    border border-white/10 rounded-3xl p-8
                    transform transition-all duration-700
                    hover:-translate-y-4 hover:scale-105
                    shadow-[0_0_40px_#22d3ee]">

                    <!-- Avatar with Glow Ring -->
                    <div class="flex justify-center mb-6 relative">
                        <div class="relative">
                            <img :src="item.image" alt="Profile" class="w-24 h-24 rounded-full object-cover
                          border-2 border-cyan-400
                          shadow-[0_0_20px_#22d3ee] animate-pulse" />
                            <div class="absolute inset-0 rounded-full border-2 border-purple-500
                          animate-ping opacity-20"></div>
                        </div>
                    </div>

                    <!-- Testimony Text -->
                    <p class="italic text-gray-300 mb-6 leading-relaxed">
                        "{{ item.testimony }}"
                    </p>

                    <!-- Name -->
                    <h4 class="text-lg font-semibold
                     text-transparent bg-clip-text 
                     bg-linear-to-r from-purple-400 to-cyan-400">
                        — {{ item.name }}
                    </h4>
                </div>
            </div>

            <!-- Carousel Indicators -->
            <div class="flex justify-center mt-12 space-x-4">
                <span v-for="(item, index) in testimonies" :key="item.id" @click="selectIndex(index)" class="w-4 h-4 rounded-full cursor-pointer
                     transition-all duration-300"
                    :class="activeIndex === index ? 'bg-cyan-400 shadow-[0_0_10px_#22d3ee]' : 'bg-white/30'"></span>
            </div>

        </div>
    </section>
</template>

<style scoped>
/* Optional floating animation */
@keyframes float {

    0%,
    100% {
        transform: translateY(0px);
    }

    50% {
        transform: translateY(-10px);
    }
}

/* Canvas particle background placeholder (can integrate tsparticles or custom) */
#particle-bg {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 0;
}

/* Fade transition for carousel */
[v-cloak]>* {
    display: none
}

[v-cloak]::before {
    content: "loading…";
}
</style>