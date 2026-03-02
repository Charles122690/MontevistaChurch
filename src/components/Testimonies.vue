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
            }, 7000);
        },
        selectIndex(index) {
            this.activeIndex = index;
        }
    }
};
</script>

<template>
    <section class="relative min-h-screen pt-32 pb-24 px-6 bg-[#f8f7f4] overflow-hidden">

        <!-- Container -->
        <div class="relative max-w-6xl mx-auto text-center">

            <!-- Title -->
            <h2 class="text-4xl md:text-5xl font-bold text-[#4f6f52] mb-16">
                Life-Changing Testimonies
            </h2>

            <!-- Testimonial Cards -->
            <div class="flex flex-col md:flex-row items-center justify-center mt-20 gap-8">

                <div v-for="(item, index) in testimonies" :key="item.id" v-show="activeIndex === index" class="w-full md:w-80 bg-white
                           border border-[#e5e5e5]
                           rounded-3xl p-8
                           transition duration-500
                           hover:shadow-md">

                    <!-- Avatar -->
                    <div class="flex justify-center mb-6">
                        <img :src="item.image" alt="Profile" class="w-24 h-24 rounded-full object-cover
                                    border border-[#e5e5e5]" />
                    </div>

                    <!-- Testimony Text -->
                    <p class="italic text-[#5f5f5f] mb-6 leading-relaxed">
                        "{{ item.testimony }}"
                    </p>

                    <!-- Name -->
                    <h4 class="text-lg font-semibold text-[#2f2f2f]">
                        — {{ item.name }}
                    </h4>
                </div>

            </div>

            <!-- Carousel Indicators -->
            <div class="flex justify-center mt-12 space-x-4">
                <span v-for="(item, index) in testimonies" :key="item.id" @click="selectIndex(index)"
                    class="w-4 h-4 rounded-full cursor-pointer transition-all duration-300" :class="activeIndex === index
                        ? 'bg-[#4f6f52]'
                        : 'bg-[#d6d6d6]'">
                </span>
            </div>

        </div>
    </section>
</template>

<style scoped>
[v-cloak]>* {
    display: none
}

[v-cloak]::before {
    content: "loading…";
}
</style>