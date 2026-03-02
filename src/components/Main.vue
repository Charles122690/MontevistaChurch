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
        { id: 1, name: "Sunday Worship", date: "Every Sunday", time: "9AM - 12AM", location: "Main Hall", description: "Join our worship and fellowship." },
        { id: 2, name: "Youth Bible Study", date: "Every Sunday Afternoon", time: "2PM - 4PM", location: "Youth Room", description: "Engaging Bible study for teens." },
        { id: 3, name: "Prayer Meeting", date: "Every Saturday Afternoon", time: "2PM - 4PM", location: "Main Hall", description: "Powerful prayer, worship, and intercession." },
        { id: 4, name: "Online Corporate Prayer", date: "Mon-Fri, Sunday", time: "8PM - 9PM", location: "Individual Homes", description: "A united time of prayer, worship, and intercession." },
        { id: 5, name: "Youth Devotion", date: "Every Tue & Thur", time: "7PM - 7:30PM", location: "Individual Homes", description: "An encounter that awakens faith and renews hearts." },
        { id: 5, name: "Visitation", date: "as needed", time: "time may vary", location: "Individual Homes", description: "A heartfelt visit that strengthens bonds and nurtures faith." }
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
      this.activeHero = (this.activeHero + 1) % this.heroImages.length
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
      if (el) el.scrollIntoView({ behavior: 'smooth' })
    },

    submitForm() {
      alert("Thank you! We will contact you shortly.")
      this.contact.name = ""
      this.contact.email = ""
      this.contact.message = ""
    },

    handleActivitySelected(activity) {
      console.log('User clicked on activity:', activity.title);
    }
  }
}
</script>

<template>
  <div class="bg-[#f8f7f4] text-[#2f2f2f] min-h-screen">

    <Nav @goto="gotoPage" />

    <div v-if="currentPage === 'home'">

      <!-- HERO -->
      <section class="relative min-h-[85vh] flex items-center justify-center text-center overflow-hidden">
        <transition name="fade" mode="out-in">
          <div :key="heroImages[activeHero].id" class="absolute inset-0 w-full h-full">

            <img :src="heroImages[activeHero].image" class="absolute inset-0 w-full h-full object-cover"
              alt="Church Hero" />

            <div class="absolute inset-0 bg-white/20"></div>

            <div class="relative z-10 flex flex-col items-center justify-center h-full px-6">

              <h1 class="text-5xl md:text-6xl font-extrabold mb-6 text-[#4f6f52] bg-white/50 px-4 py-4 rounded-2xl">
                {{ heroImages[activeHero].title }}
              </h1>

              <p class="text-xl md:text-2xl text-[#4b5563] max-w-2xl bg-white/50 px-4 py-4 rounded-2xl">
                {{ heroImages[activeHero].subtitle }}
              </p>

              <button @click="scrollToContact" class="mt-8 bg-[#4f6f52] text-white font-semibold px-10 py-3 rounded-full
                       hover:bg-[#3f5a42] transition duration-300 opacity-80 border-2 border-white cursor-pointer">
                Contact Us
              </button>

            </div>
          </div>
        </transition>
      </section>

      <!-- STATS -->
      <section class="py-20 bg-white">
        <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-10 text-center">

          <div>
            <h3 class="text-5xl font-bold text-[#4f6f52]">{{ stats.members }}</h3>
            <p class="mt-2 text-[#5f5f5f]">Happy Members</p>
          </div>

          <div>
            <h3 class="text-5xl font-bold text-[#4f6f52]">{{ stats.years }}</h3>
            <p class="mt-2 text-[#5f5f5f]">Years of Ministry</p>
          </div>

          <div>
            <h3 class="text-5xl font-bold text-[#4f6f52]">{{ stats.events }}</h3>
            <p class="mt-2 text-[#5f5f5f]">Events Held</p>
          </div>

        </div>
      </section>

    </div>

    <Sermon v-if="currentPage === 'sermons'" :sermons="sermons" />
    <Events v-if="currentPage === 'events'" :events="events" />
    <Testimonies v-if="currentPage === 'testimonies'" />
    <Activities @activity-selected="handleActivitySelected" />

    <!-- CONTACT -->
    <section id="contact" class="py-24 px-6 max-w-6xl mx-auto bg-white rounded-3xl border border-[#e5e5e5]">

      <div class="grid md:grid-cols-2 gap-12 items-start">

        <div>
          <h2 class="text-4xl font-bold text-[#4f6f52] mb-8">Contact Us</h2>

          <form @submit.prevent="submitForm" class="bg-[#f1efe9] p-10 rounded-3xl space-y-6">

            <input v-model="contact.name" type="text" placeholder="Full Name" class="w-full px-4 py-3 rounded-lg bg-white border border-[#dcdcdc]
                     text-[#2f2f2f] focus:outline-none focus:ring-2 focus:ring-[#4f6f52]" required />

            <input v-model="contact.email" type="email" placeholder="Email" class="w-full px-4 py-3 rounded-lg bg-white border border-[#dcdcdc]
                     text-[#2f2f2f] focus:outline-none focus:ring-2 focus:ring-[#4f6f52]" required />

            <textarea v-model="contact.message" rows="5" placeholder="Your Message" class="w-full px-4 py-3 rounded-lg bg-white border border-[#dcdcdc]
                     text-[#2f2f2f] focus:outline-none focus:ring-2 focus:ring-[#4f6f52]" required></textarea>

            <button type="submit" class="w-full bg-[#4f6f52] text-white font-semibold py-3 rounded-lg
                     hover:bg-[#3f5a42] transition">
              Send Message
            </button>
          </form>
        </div>

        <div class="text-[#5f5f5f] space-y-8">
          <h3 class="text-3xl font-semibold text-[#7c6f64]">Get Connected</h3>

          <p>We'd love to hear from you! Reach out and we'll get back to you.</p>

          <div class="space-y-4">
            <div>
              <h4 class="font-semibold text-[#2f2f2f]">Visit Us</h4>
              <p>Bankerohan, Montevista, Davao de Oro</p>
            </div>

            <div>
              <h4 class="font-semibold text-[#2f2f2f]">Service Times</h4>
              <p>Sunday 9:00 AM & 11:00 AM | Saturday 3:00 PM</p>
            </div>

            <div>
              <h4 class="font-semibold text-[#2f2f2f]">Prayer Requests</h4>
              <p>Send us your prayer needs and our prayer team will lift them up.</p>
            </div>
          </div>

        </div>
      </div>
    </section>

    <!-- FOOTER -->
    <footer class="bg-[#f1efe9] text-[#5f5f5f] border-t border-[#e5e5e5] mt-5 opacity-75">

      <!-- Main Footer Content -->
      <div class="max-w-6xl mx-auto px-6 py-2 grid grid-cols-1 md:grid-cols-4 gap-10">

        <!-- Church Info -->
        <div>
          <h3 class="text-lg font-semibold text-[#4f6f52] mb-4">
            AAIM - The Church of Jesus Christ Restoration, Inc.
          </h3>
          <p class="text-sm leading-relaxed">
            Montevista, Davao de Oro, Philippines
          </p>
          <p class="text-sm mt-2">
            A community rooted in faith, fellowship, and service.
          </p>
        </div>

        <!-- Quick Links -->
        <div>
          <h4 class="text-md font-semibold text-[#2f2f2f] mb-4">
            Quick Links
          </h4>
          <ul class="space-y-2 text-sm ">
            <li>
              <button @click="gotoPage('home')" class="hover:text-[#4f6f52] transition cursor-pointer">Home</button>
            </li>
            <li>
              <button @click="gotoPage('sermons')" class="hover:text-[#4f6f52] transition cursor-pointer">Sermons</button>
            </li>
            <li>
              <button @click="gotoPage('events')" class="hover:text-[#4f6f52] transition cursor-pointer">Events</button>
            </li>
            <li>
              <button @click="gotoPage('activities')" class="hover:text-[#4f6f52] transition cursor-pointer">Activities</button>
            </li>
            <li>
              <button @click="gotoPage('testimonies')" class="hover:text-[#4f6f52] transition cursor-pointer">Testimonies</button>
            </li>
            <li>
              <button @click="gotoPage('contact')" class="hover:text-[#4f6f52] transition cursor-pointer">Contact</button>
            </li>
          </ul>
        </div>

        <!-- Service Times -->
        <div>
          <h4 class="text-md font-semibold text-[#2f2f2f] mb-4">
            Service Times
          </h4>
          <ul class="space-y-2 text-sm">
            <li>Sunday Worship – 9:00 AM</li>
            <li>Sunday Afternoon – 2:00 PM</li>
            <li>Saturday Prayer – 3:00 PM</li>
          </ul>
        </div>

        <!-- Connect -->
        <div>
          <h4 class="text-md font-semibold text-[#2f2f2f] mb-4">
            Connect With Us
          </h4>

          <div class="space-y-2 text-sm">
            <p>Email:
              <a href="mailto:cojmontevistamission@gmail.com" class="hover:text-[#4f6f52] transition">
                cojmontevistamission@gmail.com
              </a>
            </p>
            <p>
              <a href="https://www.facebook.com/montevistamission" target="_blank"
                class="hover:text-[#4f6f52] transition">
                Facebook: Montevista Mission
              </a>
            </p>
          </div>
        </div>

      </div>

      <!-- Divider -->
      <div class="border-t border-[#e5e5e5]"></div>

      <!-- Bottom Bar -->
      <div class="max-w-6xl mx-auto px-6 py-2 text-center text-sm text-[#7a7a7a]">
        <p>© 2026 AAIM - The Church of Jesus Christ Restoration, Inc. All rights reserved.</p>
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