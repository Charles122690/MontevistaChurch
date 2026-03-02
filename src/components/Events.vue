<script>
export default {
    name: 'Events',
    props: {
        events: { type: Array, required: true }
    }
}
</script>

<template>
    <section id="events" class="py-20 bg-[#f8f7f4]">

        <!-- Section Title -->
        <h2 class="text-4xl font-bold text-[#4f6f52] text-center mb-12">
            Upcoming Events
        </h2>

        <div class="max-w-6xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-8">

            <div v-for="event in events" :key="event.id" class="bg-white rounded-3xl p-6 border border-[#e5e5e5]
                       hover:shadow-md transition duration-300 h-fit">

                <!-- Event Name -->
                <h3 class="text-xl font-semibold text-[#2f2f2f] mb-2">
                    {{ event.name }}
                </h3>

                <!-- Event Details -->
                <p class="text-[#5f5f5f] mb-1">
                    Date: {{ event.date }}
                </p>

                <p class="text-[#5f5f5f] mb-1">
                    Time: {{ event.time }}
                </p>

                <p class="text-[#5f5f5f] mb-3">
                    Location: {{ event.location }}
                </p>

                <p class="text-[#5f5f5f] mb-4">
                    {{ event.description }}
                </p>

                <!-- Button -->
                <button class="px-5 py-2 bg-[#4f6f52] text-white font-medium
                           rounded-lg hover:bg-[#3f5a42]
                           transition duration-300 cursor-pointer">
                    Join
                </button>

            </div>

        </div>
    </section>
</template>