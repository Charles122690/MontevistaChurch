<script>
export default {
    name: 'Sermons',
    props: {
        sermons: { type: Array, required: true }
    }
}
</script>

<template>
    <section id="sermons" class="py-20 bg-gray-900">
        <h2 class="text-4xl font-extrabold text-cyan-400 text-center mb-12">Recent Sermons</h2>
        <div class="max-w-6xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-8">
            <div v-for="sermon in sermons" :key="sermon.id"
                class="bg-gray-800 rounded-3xl overflow-hidden shadow-lg hover:scale-105 transition-transform duration-300">
                <img :src="sermon.image" alt="" class="w-full h-48 object-cover">
                <div class="p-6">
                    <h3 class="text-xl font-bold text-gray-100 mb-2">{{ sermon.title }}</h3>
                    <p class="text-gray-400 mb-1">Preacher: {{ sermon.preacher }}</p>
                    <p class="text-gray-400 mb-4">Date: {{ sermon.date }}</p>
                    <a :href="sermon.link"
                        class="inline-block px-4 py-2 bg-linear-to-r from-cyan-400 via-blue-500 to-purple-500 text-gray-900 rounded-lg font-bold hover:scale-105 transition">Watch</a>
                </div>
            </div>
        </div>
    </section>
</template>