<script>
export default {
    name: 'Events',
    props: {
        events: { type: Array, required: true }
    }
}
</script>

<template>
    <section id="events" class="py-20 bg-gray-800">
        <h2 class="text-4xl font-extrabold text-purple-400 text-center mb-12">Upcoming Events</h2>
        <div class="max-w-6xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-8">
            <div v-for="event in events" :key="event.id"
                class="bg-gray-900 rounded-3xl p-6 shadow-lg hover:scale-105 transition-transform duration-300 h-fit">
                <h3 class="text-xl font-bold text-cyan-400 mb-2">{{ event.name }}</h3>
                <p class="text-gray-400 mb-1">Date: {{ event.date }}</p>
                <p class="text-gray-400 mb-1">Time: {{ event.time }}</p>
                <p class="text-gray-400 mb-3">Location: {{ event.location }}</p>
                <p class="text-gray-300 mb-4">{{ event.description }}</p>
                <button
                    class="px-4 py-2 bg-linear-to-r from-purple-400 via-pink-500 to-red-500 text-gray-900 font-bold rounded-lg hover:scale-105 transition cursor-pointer">Join</button>
            </div>
        </div>
    </section>
</template>