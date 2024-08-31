<template>
  <div class="items-start p-8">
    <!-- Search and filter components -->
    <div class="w-full mt-4 md:justify-end md:flex">
      <input type="search" class="w-full border-2 border-indigo-600 rounded-full md:w-64" placeholder="Search Events here...">
    </div>

    <div class="flex items-center gap-4 py-6">
      <span class="px-4 py-1 text-white bg-indigo-600 rounded-full cursor-pointer hover:bg-indigo-700">All</span>
      <span class="px-4 py-1 border-2 border-indigo-600 rounded-full cursor-pointer hover:text-white hover:bg-indigo-700">Comedy</span>
      <span class="px-4 py-1 border-2 border-indigo-600 rounded-full cursor-pointer hover:text-white hover:bg-indigo-700">Music</span>
    </div>

    <!-- Upcoming Events -->
    <div>
      <h1 class="text-lg font-bold text-gray-700">Upcoming Events</h1>
      <div class="grid grid-cols-1 gap-4 mt-4 sm:grid-cols-2 lg:grid-cols-3">
        <div v-for="event in events" :key="event.id" class="p-5 overflow-hidden bg-white rounded-lg shadow">
          <img :src="event.image" :alt="event.title" class="rounded-lg shadow-lg">
          <div class="py-4">
            <h2 class="text-lg font-bold text-gray-800">{{ event.title }}</h2>
            <div class="flex items-center justify-between mt-1">
              <div class="flex items-center gap-2 font-semibold text-gray-500">
                <i class="bi bi-calendar"></i>
                <span>{{ event.date }}</span>
              </div>
              <div class="flex items-center gap-2 font-semibold text-gray-500">
                <i class="bi bi-clock"></i>
                <span>{{ event.time }}</span>
              </div>
            </div>
            <div class="flex justify-end mt-4">
              <span class="text-indigo-600 cursor-pointer" @click="openModal(event)">
                Buy Ticket
                <i class="bi bi-chevron-right"></i>
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal -->
    <Modal :show="showModal" @close="closeModal">
      <div v-if="selectedEvent" class="relative p-6">
        <!-- Close button -->
        <button @click="closeModal" class="absolute text-gray-500 top-2 right-2 hover:text-gray-700">
          <i class="bi bi-x-lg"></i>
        </button>

        <h1 class="mb-4 text-2xl font-bold">{{ selectedEvent.title }}</h1>
        <div class="flex items-center justify-between mt-1 mb-4">
          <div class="flex items-center gap-2 font-semibold text-gray-500">
            <i class="bi bi-geo-alt"></i>
            <span>{{ selectedEvent.location }}</span>
          </div>
          <div class="flex items-center gap-2 font-semibold text-gray-500">
            <i class="bi bi-calendar"></i>
            <span>{{ selectedEvent.date }}</span>
          </div>
        </div>
        <h2 class="mb-2 text-xl font-semibold">About Event</h2>
        <p>{{ selectedEvent.description }}</p>
        <div class="flex justify-end mt-6">
          <button class="px-4 py-2 text-white bg-indigo-600 rounded hover:bg-indigo-700">
            Buy Ticket - M30.00
          </button>
        </div>
      </div>
    </Modal>
  </div>
</template>

<script>
import { Link } from '@inertiajs/vue3';
import Modal from '../../Components/Modal.vue';

export default {
  components: {
    Link,
    Modal
  },
  data() {
    return {
      showModal: false,
      selectedEvent: null,
      events: [
        {
          id: 1,
          title: "Lecholi Annual Event",
          date: "Nov 10 2024",
          time: "10:00 AM",
          location: "Semonkong",
          image: "assets/images/3.jpg",
          description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Facere nobis, quos ea deserunt suscipit saepe exercitationem laboriosam eius vel in! Hic, animi dolorem dolores voluptatem cupiditate labore neque perspiciatis laudantium."
        },
        // you can add more events as here kapa get them from the database
      ]
    };
  },
  methods: {
    openModal(event) {
      this.selectedEvent = event;
      this.showModal = true;
    },
    closeModal() {
      this.showModal = false;
    }
  }
};
</script>
