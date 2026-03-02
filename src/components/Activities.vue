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
            selectedActivityIndex: null,
            currentImageIndex: 0
        };
    },
    computed: {
        selectedActivity() {
            return this.selectedActivityIndex !== null ? this.activities[this.selectedActivityIndex] : null;
        }
    },
    methods: {
        openModal(index) {
            this.selectedActivityIndex = index;
            this.currentImageIndex = 0;
        },
        closeModal() {
            this.selectedActivityIndex = null;
            this.currentImageIndex = 0;
        },
        prevImage() {
            if (this.currentImageIndex > 0) this.currentImageIndex--;
        },
        nextImage() {
            if (this.currentImageIndex < this.selectedActivity.images.length - 1) this.currentImageIndex++;
        },
        prevActivity() {
            if (this.selectedActivityIndex > 0) {
                this.selectedActivityIndex--;
                this.currentImageIndex = 0;
            }
        },
        nextActivity() {
            if (this.selectedActivityIndex < this.activities.length - 1) {
                this.selectedActivityIndex++;
                this.currentImageIndex = 0;
            }
        },
        clickOutside(e) {
            if (e.target.classList.contains("modal-overlay")) {
                this.closeModal();
            }
        }
    }
};
</script>

<template>
    <section class="py-24 px-6 max-w-7xl mx-auto">
        <!-- Activity Grid -->
        <div class="grid sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-8">
            <div v-for="(activity, index) in activities" :key="activity.id"
                class="relative group cursor-pointer rounded-xl overflow-hidden shadow-lg transform transition duration-500 hover:scale-105 hover:shadow-2xl"
                @click="openModal(index)">
                <img :src="activity.images[0]" :alt="activity.title"
                    class="w-full h-full object-cover transition duration-500 group-hover:blur-sm" />
                <div
                    class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition duration-500">
                    <h3 class="text-white text-lg font-semibold text-center px-2 drop-shadow-lg">{{ activity.title }}
                    </h3>
                </div>
            </div>
        </div>

        <!-- Modal -->
        <div v-if="selectedActivity"
            class="fixed inset-0 z-50 flex items-center justify-center modal-overlay bg-black bg-opacity-70 p-6 cursor-pointer"
            @click="clickOutside">
            <div class="bg-gray-900 rounded-2xl max-w-3xl w-full relative overflow-hidden shadow-2xl">

                <!-- Close Modal Button -->
                <button @click="closeModal"
                    class="absolute top-4 right-4 text-white text-2xl font-bold hover:text-cyan-400 transition">&times;</button>

                <!-- Navigate to Home Button (X on image) -->
                <button @click="$emit('goto', 'home')"
                    class="absolute top-4 left-4 text-white text-2xl font-bold bg-red-600 hover:bg-red-700 rounded-full w-10 h-10 flex items-center justify-center transition">
                    X
                </button>

                <!-- Activity Navigation -->
                <button v-if="selectedActivityIndex > 0" @click="prevActivity"
                    class="absolute left-4 top-16 bg-gray-700 bg-opacity-50 hover:bg-opacity-80 text-white rounded-full px-3 py-1 font-semibold transition">&larr;
                    Back</button>
                <button v-if="selectedActivityIndex < activities.length - 1" @click="nextActivity"
                    class="absolute right-4 top-16 bg-gray-700 bg-opacity-50 hover:bg-opacity-80 text-white rounded-full px-3 py-1 font-semibold transition">Next
                    &rarr;</button>

                <!-- Carousel Image -->
                <div class="relative">
                    <img :src="selectedActivity.images[currentImageIndex]" :alt="selectedActivity.title"
                        class="w-full h-full object-cover rounded-t-2xl" />

                    <!-- Image Prev/Next -->
                    <button v-if="currentImageIndex > 0" @click="prevImage"
                        class="cursor-pointer absolute left-4 top-1/2 transform -translate-y-1/2 bg-gray-700 bg-opacity-50 hover:bg-opacity-80 text-white rounded-full p-2 transition">&larr;</button>
                    <button v-if="currentImageIndex < selectedActivity.images.length - 1" @click="nextImage"
                        class="cursor-pointer absolute right-4 top-1/2 transform -translate-y-1/2 bg-gray-700 bg-opacity-50 hover:bg-opacity-80 text-white rounded-full p-2 transition">&rarr;</button>
                </div>

                <div class="p-4 text-gray-200">
                    <h3 class="text-2xl font-bold text-cyan-400 mb-4">{{ selectedActivity.title }}</h3>
                    <p class="text-gray-300">{{ selectedActivity.description }}</p>
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

/* Image blur on hover */
.group-hover\:blur-sm:hover {
    filter: blur(4px);
}
</style>