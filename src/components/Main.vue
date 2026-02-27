<script>
import Nav from './Nav.vue'
import Sermon from './Sermon.vue'
import Events from './Events.vue'
import Testimonies from './Testimonies.vue'
import Activities from './Activities.vue';

export default {
  name: 'Main',
  components: { Nav, Sermon, Events, Testimonies, Activities },

  data() {
    return {
      currentPage: 'home',
      activeHero: 0,
      heroInterval: null,

      heroImages: [
        {
          id: 1,
          title: "Welcome to Montevista Mission",
          subtitle: "Your spiritual home in the digital era",
          image: "stage.jpeg"
        },
        {
          id: 2,
          title: "Faith, Hope, and Innovation",
          subtitle: "Connecting souls in a modern world",
          image: "pic2.jpeg"
        },
        {
          id: 3,
          title: "Worship Together",
          subtitle: "Experience uplifting sermons and events",
          image: "pic3.jpeg"
        }
      ],

      stats: {
        members: "30+",
        years: "2+",
        events: "12+"
      },

      sermons: [
        {
          id: 1,
          title: "When Belief becomes Action",
          preacher: "Bro. Charles Verano",
          date: "Jan 25, 2026",
          image: "faith.jpg",
          link: "#"
        },
        {
          id: 2,
          title: "Life after Death",
          preacher: "Elder Adam Brendell",
          date: "Feb 22, 2026",
          image: "https://images.unsplash.com/photo-1504052434569-70ad5836ab65?q=80&w=800&auto=format&fit=crop",
          link: "#"
        },
        {
          id: 3,
          title: "Blessed beyond Measures",
          preacher: "Elder Isidro Alegre",
          date: "Dec 21, 2025",
          image: "bless.jpg",
          link: "#"
        },

      ],

      events: [
        {
          id: 1,
          name: "Sunday Worship",
          date: "Every Sunday",
          time: "9AM - 12AM",
          location: "Main Hall",
          description: "Join our worship and fellowship."
        },
        {
          id: 2,
          name: "Youth Bible Study",
          date: "Every Sunday Afternoon",
          time: "2PM - 4PM",
          location: "Youth Room",
          description: "Engaging Bible study for teens."
        },
        {
          id: 3,
          name: "Prayer Meeting",
          date: "Every Saturday Afternoon",
          time: "2PM - 4PM",
          location: "Main Hall",
          description: "Powerful prayer, worship, and intercession."
        },
        {
          id: 4,
          name: "Online Corporate Prayer",
          date: "Mon-Fri, Sunday",
          time: "8PM - 9PM",
          location: "Individual Homes",
          description: "A united time of prayer, worship, and intercession."
        },
        {
          id: 4,
          name: "Online Youth Devotion",
          date: "Every Tuesday & Friday",
          time: "7PM - 8PM",
          location: "Individual Homes",
          description: "A time set apart for devotion and spiritual growth."
        },
        {
          id: 5,
          name: "Encounter",
          date: "Always",
          time: "time vary",
          location: "Individual Homes",
          description: "An encounter that awakens faith and renews hearts."
        },
      ],

      contact: {
        name: "",
        email: "",
        message: ""
      }
    }
  },

  mounted() {
    this.heroInterval = setInterval(() => {
      this.activeHero =
        (this.activeHero + 1) % this.heroImages.length
    }, 5000)
  },

  beforeUnmount() {
    clearInterval(this.heroInterval)
  },

  methods: {
    gotoPage(page) {
      this.currentPage = page
      window.scrollTo({ top: 0, behavior: 'smooth' })
    },

    scrollToContact() {
      const el = document.getElementById('contact')
      if (el) {
        el.scrollIntoView({ behavior: 'smooth' })
      }
    },

    submitForm() {
      alert("Thank you! We will contact you shortly.")
      this.contact.name = ""
      this.contact.email = ""
      this.contact.message = ""
    },
    methods: {
      openModal(activity) {
        this.selectedActivity = activity;
        this.$emit('activity-selected', activity); // emit event
      }
    },
    methods: {
      handleActivitySelected(activity) {
        console.log('User clicked on activity:', activity.title);
        // You can trigger additional actions here
      }
    }
  }
}
</script>

<template>
  <div class="bg-gray-900 text-gray-100 min-h-screen">

    <!-- NAVBAR -->
    <Nav @goto="gotoPage" />

    <!-- HOME PAGE -->
    <div v-if="currentPage === 'home'">

      <!-- HERO SECTION -->
      <section class="relative min-h-[85vh] flex items-center justify-center text-center overflow-hidden">

        <transition name="fade" mode="out-in">
          <div :key="heroImages[activeHero].id" class="absolute inset-0 w-full h-full">

            <!-- Background -->
            <img :src="heroImages[activeHero].image" class="absolute inset-0 w-full h-full object-cover"
              alt="Church Hero" />

            <!-- Overlay -->
            <div class="absolute inset-0 bg-linear-to-b from-black/60 via-black/50 to-black/80"></div>

            <!-- Content -->
            <div class="relative z-10 flex flex-col items-center justify-center h-full px-6">

              <h1 class="text-5xl md:text-6xl font-extrabold mb-6 text-cyan-400 drop-shadow-[0_0_20px_#22d3ee]">
                {{ heroImages[activeHero].title }}
              </h1>

              <p class="text-xl md:text-2xl text-gray-200 max-w-2xl">
                {{ heroImages[activeHero].subtitle }}
              </p>

              <button @click="scrollToContact" class="mt-8 bg-linear-to-r from-cyan-400 via-blue-500 to-purple-500
                       text-gray-900 font-bold px-10 py-3 rounded-full
                       shadow-lg hover:scale-105 transition duration-300 cursor-pointer">
                Contact Us
              </button>

            </div>
          </div>
        </transition>

      </section>

      <!-- STATS SECTION -->
      <section class="py-20 bg-gray-800">
        <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-10 text-center">

          <div>
            <h3 class="text-5xl font-extrabold text-cyan-400">
              {{ stats.members }}
            </h3>
            <p class="mt-2 text-gray-300">Happy Members</p>
          </div>

          <div>
            <h3 class="text-5xl font-extrabold text-cyan-400">
              {{ stats.years }}
            </h3>
            <p class="mt-2 text-gray-300">Years of Ministry</p>
          </div>

          <div>
            <h3 class="text-5xl font-extrabold text-cyan-400">
              {{ stats.events }}
            </h3>
            <p class="mt-2 text-gray-300">Events Held</p>
          </div>

        </div>
      </section>

    </div>

    <!-- SERMON PAGE -->
    <Sermon v-if="currentPage === 'sermons'" :sermons="sermons" />

    <!-- EVENTS PAGE -->
    <Events v-if="currentPage === 'events'" :events="events" />

    <!-- TESTIMONIES -->
    <Testimonies v-if="currentPage === 'testimonies'" />
    <!-- Activities -->
    <Activities @activity-selected="handleActivitySelected" />


    <!-- CONTACT -->
    <section id="contact" class="py-24 px-6 max-w-6xl mx-auto bg-gray-950 rounded-3xl relative overflow-hidden">
      <!-- Soft Gradient Background -->
      <div
        class="absolute inset-0 bg-linear-to-tr from-gray-900 via-gray-800 to-gray-950 opacity-40 pointer-events-none rounded-3xl">
      </div>

      <div class="grid md:grid-cols-2 gap-12 items-start relative z-10">

        <!-- Left Side: Contact Form -->
        <div>
          <h2 class="text-4xl font-extrabold text-cyan-400 mb-8">
            Contact Us
          </h2>

          <form @submit.prevent="submitForm" class="bg-gray-800 p-10 rounded-3xl shadow-xl space-y-6">
            <input v-model="contact.name" type="text" placeholder="Full Name"
              class="w-full px-4 py-3 rounded-lg bg-gray-700 text-white focus:outline-none focus:ring-2 focus:ring-cyan-400"
              required />

            <input v-model="contact.email" type="email" placeholder="Email"
              class="w-full px-4 py-3 rounded-lg bg-gray-700 text-white focus:outline-none focus:ring-2 focus:ring-cyan-400"
              required />

            <textarea v-model="contact.message" rows="5" placeholder="Your Message"
              class="w-full px-4 py-3 rounded-lg bg-gray-700 text-white focus:outline-none focus:ring-2 focus:ring-cyan-400"
              required></textarea>

            <button type="submit"
              class="w-full bg-linear-to-r from-cyan-400 via-blue-500 to-purple-500
               text-gray-900 font-bold py-3 rounded-lg hover:scale-105 transition-transform duration-300 cursor-pointer">
              Send Message
            </button>
          </form>
        </div>

        <!-- Right Side: Church Info / Engagement -->
        <div class="text-gray-200 space-y-8">
          <h3 class="text-3xl font-semibold text-purple-400">Get Connected</h3>
          <p class="text-gray-300">
            We'd love to hear from you! Whether you have questions, prayer requests, or want to join one of our
            ministries, reach out and we'll get back to you.
          </p>

          <div class="space-y-4">
            <div class="flex items-start gap-4">
              <span class="text-cyan-400 text-xl">📍</span>
              <div>
                <h4 class="font-semibold">Visit Us</h4>
                <p>Bankerohan, Montevista, Davao de Oro</p>
              </div>
            </div>

            <div class="flex items-start gap-4">
              <span class="text-cyan-400 text-xl">⏰</span>
              <div>
                <h4 class="font-semibold">Service Times</h4>
                <p>Sunday 9:00 AM & 11:00 AM | Saturday 3:00 PM</p>
              </div>
            </div>

            <div class="flex items-start gap-4">
              <span class="text-cyan-400 text-xl">🙏</span>
              <div>
                <h4 class="font-semibold">Prayer Requests</h4>
                <p>Send us your prayer needs and our prayer team will lift them up.</p>
              </div>
            </div>
          </div>

          <!-- Social Media & Gmail -->
          <div class="mt-6 space-y-4">
            <h4 class="font-semibold text-purple-400">Follow Us</h4>

            <!-- Facebook: Montevista Mission -->
            <a href="https://www.facebook.com/montevistamission" target="_blank"
              class="flex items-center gap-2 hover:scale-105 transition">
              <!-- SVG Facebook Logo -->
              <svg class="w-8 h-8" viewBox="0 0 24 24" fill="#00bcd4" xmlns="http://www.w3.org/2000/svg">
                <path
                  d="M22.675 0H1.325C0.593 0 0 0.593 0 1.325v21.351C0 23.407 0.593 24 1.325 24H12.82v-9.294H9.692V11.07h3.128V8.413c0-3.1 1.893-4.788 4.659-4.788 1.325 0 2.463 0.099 2.794 0.143v3.24l-1.918 0.001c-1.504 0-1.794 0.715-1.794 1.763v2.31h3.587l-0.467 3.636h-3.12V24h6.116c0.732 0 1.325-0.593 1.325-1.324V1.325C24 0.593 23.407 0 22.675 0z" />
              </svg>
              <span class="text-gray-300">Montevista Mission</span>
            </a>

            <!-- Gmail -->
            <div class="flex items-center gap-2 hover:scale-105 trnasition cursor-pointer">
              <!-- SVG Gmail Logo -->
              <svg class="w-8 h-8" viewBox="0 0 24 24" fill="#f44336" xmlns="http://www.w3.org/2000/svg">
                <path
                  d="M20 4H4C2.897 4 2 4.897 2 6v12c0 1.103 0.897 2 2 2h16c1.103 0 2-0.897 2-2V6c0-1.103-0.897-2-2-2zm0 2l-8 5-8-5h16zm-16 12V8l8 5 8-5v10H4z" />
              </svg>
              <span class="text-gray-300">cojmontevistamission@gmail.com</span>
            </div>

          </div>
        </div>

      </div>
    </section>

    <!-- FOOTER -->
    <footer class="bg-gray-950 text-gray-400 py-3 border-t border-gray-800 mt-10 opacity-50">
      <div class="max-w-6xl mx-auto flex flex-col md:flex-row items-center justify-between px-6 gap-6">

        <!-- About / Church Info -->
        <div class="flex-1 text-center md:text-left">
          <p class="font-semibold text-cyan-400">AAIM - THE CHURCH OF JESUS CHRIST RESTORATION, INC</p>
          <p>Montevista, Davao de Oro, Philippines</p>
        </div>

        <!-- Quick Links / Navigation -->
        <div class="flex-1 flex justify-center gap-4 flex-wrap">
          <a href="#home" class="hover:text-cyan-400 transition">Home</a>
          <a href="#about" class="hover:text-cyan-400 transition">About</a>
          <a href="#activities" class="hover:text-cyan-400 transition">Activities</a>
          <a href="#testimonials" class="hover:text-cyan-400 transition">Testimonials</a>
          <a href="#contact" class="hover:text-cyan-400 transition">Contact</a>
        </div>

        <!-- Connect / Social Media -->
        <div class="flex-1 flex justify-center md:justify-end items-center gap-4">
          <!-- Facebook -->
          <a href="https://www.facebook.com/montevistamission" target="_blank" class="hover:text-cyan-400 transition">
            <svg class="w-6 h-6" viewBox="0 0 24 24" fill="#00bcd4" xmlns="http://www.w3.org/2000/svg">
              <path
                d="M22.675 0H1.325C0.593 0 0 0.593 0 1.325v21.351C0 23.407 0.593 24 1.325 24H12.82v-9.294H9.692V11.07h3.128V8.413c0-3.1 1.893-4.788 4.659-4.788 1.325 0 2.463 0.099 2.794 0.143v3.24l-1.918 0.001c-1.504 0-1.794 0.715-1.794 1.763v2.31h3.587l-0.467 3.636h-3.12V24h6.116c0.732 0 1.325-0.593 1.325-1.324V1.325C24 0.593 23.407 0 22.675 0z" />
            </svg>
          </a>

          <!-- Gmail -->
          <a href="mailto:cojmontevistamission@gmail.com" class="hover:text-red-500 transition">
            <svg class="w-6 h-6" viewBox="0 0 24 24" fill="#f44336" xmlns="http://www.w3.org/2000/svg">
              <path
                d="M20 4H4C2.897 4 2 4.897 2 6v12c0 1.103 0.897 2 2 2h16c1.103 0 2-0.897 2-2V6c0-1.103-0.897-2-2-2zm0 2l-8 5-8-5h16zm-16 12V8l8 5 8-5v10H4z" />
            </svg>
          </a>
        </div>

      </div>

      <!-- Bottom copyright -->
      <div class="mt-4 text-center text-gray-500 text-sm">
        <p>© 2026 All Rights Reserved.</p>
        <p>Photos: <a href="https://unsplash.com/" target="_blank" class="hover:text-cyan-400">Unsplash</a>,
          <a href="https://images.google.com/" target="_blank" class="hover:text-cyan-400">Google Images</a>
        </p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.8s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>