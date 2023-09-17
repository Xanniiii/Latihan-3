<template>
  <div>
    <h1>Pameran Seni</h1>
    
    <label for="sort-select">Urutkan berdasarkan:</label>
    <select id="sort-select" v-model="selectedSort">
      <option value="kategori">Kategori</option>
      <option value="tanggal">Tanggal</option>
    </select>

    <ul>
      <li v-for="event in sortedEvents" :key="event.id">
        <h2>{{ event.nama }}</h2>
        <p><strong>Tanggal:</strong> {{ event.tanggal }}</p>
        <p><strong>Kategori:</strong> {{ event.kategori }}</p>
        <p>{{ event.deskripsi }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {

  layout (contect) {
        return 'custom'
    },
  data() {
    return {
      selectedSort: 'kategori',
      events: [
        {
          id: 1,
          nama: 'Pameran Lukisan Abstrak',
          tanggal: '2023-10-15',
          kategori: 'Seni Lukis',
          deskripsi: 'Pameran lukisan abstrak oleh seniman lokal.',
        },
        {
          id: 2,
          nama: 'Pentas Tari Tradisional',
          tanggal: '2023-10-05',
          kategori: 'Tari Tradisional',
          deskripsi: 'Pentas tari tradisional dari berbagai daerah.',
        },
      ],
    };
  },
  computed: {
    sortedEvents() {
      if (this.selectedSort === 'kategori') {
        return this.events.slice().sort((a, b) => a.kategori.localeCompare(b.kategori));
      } else if (this.selectedSort === 'tanggal') {
        return this.events.slice().sort((a, b) => new Date(a.tanggal) - new Date(b.tanggal));
      }
      return this.events;
    },
  },
};
</script>
