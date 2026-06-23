<template>
  <div class="page">
    <header class="hero">
      <p class="festival-tag">Cape Town Food Fest</p>
      <h1>Cape Town Food Fest 2026</h1>
      <p class="hero-subtitle">Good food. Good music. Good vibes.</p>
      <p class="hero-text">
        Join us for a weekend of flavour, music and fun. Explore our ticket
        options and choose the Food Fest experience that suits you best.
      </p>

      <div class="favourite-summary">
        ♡ Favourite tickets: <strong>{{ favouriteCount }}</strong>
      </div>
    </header>

    <section class="tickets-section">
      <h2>Choose Your Ticket</h2>

      <div class="ticket-grid">
        <div
          v-for="ticket in tickets"
          :key="ticket.id"
          class="ticket-card"
          :class="{ featured: ticket.featured }"
        >
          <div class="ticket-top">
            <span v-if="ticket.featured" class="featured-badge">Featured</span>

            <button class="favourite-btn" @click="toggleFavourite(ticket.id)">
              {{ ticket.favourited ? "♥ Saved" : "♡ Save" }}
            </button>
          </div>

          <div class="ticket-icon">{{ ticket.icon }}</div>

          <h3>{{ ticket.name }}</h3>
          <p class="ticket-tagline">{{ ticket.tagline }}</p>
          <p class="price">R{{ ticket.price }}</p>

          <ul class="benefits-list">
            <li v-for="(benefit, index) in ticket.benefits" :key="index">
              {{ benefit }}
            </li>
          </ul>

          <button class="cta-btn">Notify Me</button>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "TicketLanding",
  data() {
    return {
      tickets: [
        {
          id: 1,
          name: "Bronze",
          tagline: "A simple festival ticket.",
          icon: "✿",
          price: 150,
          benefits: [
            "General festival entry",
            "Access to food vendors",
            "Live music area access",
          ],
          featured: false,
          favourited: false,
        },
        {
          id: 2,
          name: "Silver",
          tagline: "A little extra for food lovers.",
          icon: "❀",
          price: 300,
          benefits: [
            "Everything in Bronze",
            "Priority entry",
            "1 complimentary drink voucher",
            "Reserved seating zone",
          ],
          featured: true,
          favourited: false,
        },
        {
          id: 3,
          name: "Gold",
          tagline: "The full VIP festival experience.",
          icon: "✧",
          price: 500,
          benefits: [
            "Everything in Silver",
            "VIP lounge access",
            "Meet-and-greet with chefs",
            "2 premium tasting vouchers",
          ],
          featured: false,
          favourited: false,
        },
      ],
    };
  },
  computed: {
    favouriteCount() {
      return this.tickets.filter((ticket) => ticket.favourited).length;
    },
  },
  methods: {
    toggleFavourite(id) {
      const selectedTicket = this.tickets.find((ticket) => ticket.id === id);
      if (selectedTicket) {
        selectedTicket.favourited = !selectedTicket.favourited;
      }
    },
  },
};
</script>

<style scoped>
.page {
  min-height: 100vh;
  background: #f7efe5;
  color: #2f2a24;
  font-family: Arial, Helvetica, sans-serif;
}

/* HERO */
.hero {
  background: #3d312a;
  color: #fff7ef;
  text-align: center;
  padding: 4rem 1.5rem 3.5rem;
  border-bottom-left-radius: 30px;
  border-bottom-right-radius: 30px;
}

.festival-tag {
  text-transform: uppercase;
  letter-spacing: 2px;
  font-size: 0.85rem;
  margin-bottom: 1rem;
  color: #e7d8c7;
}

.hero h1 {
  font-size: 2.6rem;
  margin-bottom: 0.7rem;
}

.hero h1 span {
  color: #d46d43;
  font-style: italic;
}

.hero-subtitle {
  color: #d4c16c;
  font-weight: bold;
  margin-bottom: 1rem;
  letter-spacing: 1px;
}

.hero-text {
  max-width: 700px;
  margin: 0 auto 1.5rem;
  line-height: 1.6;
  font-size: 1rem;
}

.favourite-summary {
  display: inline-block;
  background: #6d7140;
  padding: 0.8rem 1.2rem;
  border-radius: 999px;
  font-size: 1rem;
}

/* SECTION */
.tickets-section {
  max-width: 1150px;
  margin: 0 auto;
  padding: 3rem 1.5rem 4rem;
}

.tickets-section h2 {
  text-align: center;
  font-size: 2rem;
  margin-bottom: 2rem;
  color: #3b312a;
}

/* GRID */
.ticket-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.5rem;
  align-items: stretch;
}

.ticket-card {
  background: #fffaf4;
  border: 1px solid #e2d4c4;
  border-radius: 20px;
  padding: 1.5rem;
  box-shadow: 0 8px 18px rgba(0, 0, 0, 0.06);
  transition: 0.25s ease;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 420px;
}

.ticket-card:hover {
  transform: translateY(-4px);
}

.ticket-card.featured {
  border: 2px solid #6d7140;
}

.ticket-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  min-height: 35px;
  margin-bottom: 1rem;
}

.featured-badge {
  background: #6d7140;
  color: white;
  font-size: 0.8rem;
  font-weight: bold;
  padding: 0.35rem 0.8rem;
  border-radius: 999px;
}

.favourite-btn {
  border: 1px solid #d8c7b5;
  background: #fff;
  color: #8f4e31;
  padding: 0.45rem 0.85rem;
  border-radius: 999px;
  cursor: pointer;
  font-size: 0.9rem;
}

.favourite-btn:hover {
  background: #f7f1ea;
}

.ticket-icon {
  width: 60px;
  height: 60px;
  margin: 0 auto 1rem;
  border-radius: 50%;
  background: #d46d43;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
}

.featured .ticket-icon {
  background: #6d7140;
}

.ticket-card h3 {
  text-align: center;
  font-size: 1.9rem;
  margin-bottom: 0.4rem;
  color: #b4572f;
}

.featured h3 {
  color: #5d6136;
}

.ticket-tagline {
  text-align: center;
  color: #5b5249;
  margin-bottom: 1rem;
  font-size: 0.95rem;
}

.price {
  text-align: center;
  font-size: 2.2rem;
  font-weight: bold;
  color: #c28725;
  margin-bottom: 1.2rem;
}

.benefits-list {
  list-style: none;
  padding: 0;
  margin: 0 0 1.5rem;
  flex-grow: 1;
}

.benefits-list li {
  background: #f9f3eb;
  padding: 0.75rem;
  border-radius: 10px;
  margin-bottom: 0.6rem;
  color: #3d352d;
  font-size: 0.95rem;
}

.cta-btn {
  width: 100%;
  border: none;
  background: #c85d33;
  color: white;
  padding: 0.9rem 1rem;
  border-radius: 12px;
  font-size: 1rem;
  font-weight: bold;
  cursor: pointer;
}

.featured .cta-btn {
  background: #6d7140;
}

.cta-btn:hover {
  opacity: 0.95;
}

/* RESPONSIVE */
@media (max-width: 950px) {
  .ticket-grid {
    grid-template-columns: 1fr;
  }

  .hero h1 {
    font-size: 2.1rem;
  }
}
</style>
