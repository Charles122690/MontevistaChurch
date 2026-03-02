<script>
export default {
    name: 'Sermons',
    props: {
        sermons: { type: Array, required: true }
    }
}
</script>

<template>
    <section id="sermons" class="py-20 bg-[#f8f7f4]">

        <!-- Section Title -->
        <h2 class="text-4xl font-bold text-[#4f6f52] text-center mb-12">
            Recent Sermons
        </h2>

        <div class="max-w-6xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-8">

            <div v-for="sermon in sermons" :key="sermon.id" class="bg-white rounded-3xl overflow-hidden border border-[#e5e5e5]
                       hover:shadow-md transition duration-300">

                <!-- Image -->
                <img :src="sermon.image" alt="" class="w-full h-48 object-cover">

                <!-- Content -->
                <div class="p-6">

                    <h3 class="text-xl font-semibold text-[#2f2f2f] mb-2">
                        {{ sermon.title }}
                    </h3>

                    <p class="text-[#5f5f5f] mb-1">
                        Preacher: {{ sermon.preacher }}
                    </p>

                    <p class="text-[#5f5f5f] mb-4">
                        Date: {{ sermon.date }}
                    </p>

                    <a :href="sermon.link" class="inline-block px-5 py-2
                              bg-[#4f6f52] text-white
                              rounded-lg font-medium
                              hover:bg-[#3f5a42]
                              transition duration-300">
                        Watch
                    </a>

                </div>
            </div>

        </div>
    </section>
</template>