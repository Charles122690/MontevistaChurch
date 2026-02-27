<script>
export default {
    name: "Activities",
    data() {
        return {
            activities: [
                {
                    id: 1,
                    title: "Sunday Service",
                    images: [
                        "/Sunday/S1.jpeg",
                        "/Sunday/S2.jpeg",
                        "/Sunday/S3.jpeg",
                        "/Sunday/S4.jpeg",
                        "/Sunday/S5.jpeg",
                        "/Sunday/S6.jpeg",
                        "/Sunday/S7.jpeg",
                        "/Sunday/S8.jpeg",
                        "/Sunday/S9.jpeg",
                        "/Sunday/S10.jpeg",
                        "/Sunday/S11.jpeg",
                        "/Sunday/S12.jpeg",
                        "/Sunday/S13.jpeg",
                        "/Sunday/S14.jpeg",
                        "/Sunday/S15.jpeg",
                        "/Sunday/S16.jpeg",
                        "/Sunday/S17.jpeg",


                    ],
                    description: "Join our Sunday services every week for worship and teaching."
                },
                {
                    id: 2,
                    title: "Youth Fellowship",
                    images: [
                        "/YF/yf1.jpeg",
                        "/YF/yf2.jpeg",
                        "/YF/yf3.jpeg",
                        "/YF/yf4.jpeg"
                    ],
                    description: "Fun and inspiring activities for the youth to grow in faith."
                },
                {
                    id: 3,
                    title: "Prayer Meeting",
                    images: [
                        "/PM/pm1.jpeg",
                        "/PM/pm2.jpeg",
                        "/PM/pm3.jpeg",
                        "/PM/pm4.jpeg",
                        "/PM/pm5.jpeg"
                    ],
                    description: "Weekly prayer gatherings to lift our community in prayer."
                },
                {
                    id: 4,
                    title: "Outreach Program",
                    images: [
                        "/OP/op1.jpeg",
                        "/OP/op2.jpeg",
                        "/OP/op3.jpeg",
                    ],
                    description: "Spreading love and helping our local community in need."
                }
            ],
            selectedActivity: null,
            currentImageIndex: 0
        };
    },
    methods: {
        openModal(activity) {
            this.selectedActivity = activity;
            this.currentImageIndex = 0; // reset to first image
        },
        closeModal() {
            this.selectedActivity = null;
            this.currentImageIndex = 0;
        },
        prevImage() {
            if (this.currentImageIndex > 0) {
                this.currentImageIndex--;
            }
        },
        nextImage() {
            if (this.selectedActivity && this.currentImageIndex < this.selectedActivity.images.length - 1) {
                this.currentImageIndex++;
            }
        }
    }
};
</script>

<template>
    <section class="py-24 px-6 max-w-7xl mx-auto">
        <h2 class="text-4xl md:text-5xl font-extrabold text-cyan-400 text-center mb-16">
            Our Activities
        </h2>

        <!-- Activity Grid -->
        <div class="grid sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-8">
            <div v-for="activity in activities" :key="activity.id"
                class="relative group cursor-pointer rounded-xl overflow-hidden shadow-lg transform transition duration-500 hover:scale-105 hover:shadow-2xl"
                @click="openModal(activity)">
                <img :src="activity.images[0]" :alt="activity.title"
                    class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110" />
                <div
                    class="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center opacity-0 group-hover:opacity-100 transition duration-500">
                    <h3 class="text-white text-lg font-semibold text-center px-2">{{ activity.title }}</h3>
                </div>
            </div>
        </div>

        <!-- Modal -->
        <div v-if="selectedActivity"
            class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-70 p-6">
            <div class="bg-gray-900 rounded-2xl max-w-3xl w-full relative overflow-hidden shadow-2xl">
                <button @click="closeModal"
                    class="absolute top-4 right-4 text-white text-2xl font-bold hover:text-cyan-400 transition">&times;</button>

                <!-- Carousel Image -->
                <div class="relative">
                    <img :src="selectedActivity.images[currentImageIndex]" :alt="selectedActivity.title"
                        class="w-full h-full object-cover rounded-t-2xl" />

                    <!-- Prev Button -->
                    <button v-if="currentImageIndex > 0" @click="prevImage"
                        class="absolute left-4 top-1/2 transform -translate-y-1/2 bg-gray-700 bg-opacity-50 hover:bg-opacity-80 text-white rounded-full p-2 transition">&larr;</button>

                    <!-- Next Button -->
                    <button v-if="currentImageIndex < selectedActivity.images.length - 1" @click="nextImage"
                        class="absolute right-4 top-1/2 transform -translate-y-1/2 bg-gray-700 bg-opacity-50 hover:bg-opacity-80 text-white rounded-full p-2 transition">&rarr;</button>
                </div>

                <div class="p-4 text-gray-200">
                    <h3 class="text-2xl font-bold text-cyan-400 mb-4">{{ selectedActivity.title }}</h3>
                    <p class="text-gray-300 h-5">{{ selectedActivity.description }}</p>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
/* Smooth fade-in for modal */
[v-cloak]>* {
    display: none;
}
</style>




