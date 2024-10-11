<template>
  <div class="container">
    <div class="content">
      <p class="title">Are you ready to take the challenge?</p>
      <p>Download the Harlem Wizards App</p>
      <div class="app-icons">
        <img :src="googleImage" alt="Google Store" class="app-image" />
        <img :src="appleImage" alt="Apple Store" class="app-image" />
      </div>

      <div class="signup-border">
        <p>or you can sign up right now</p>
      </div>

      <input v-model="searchQuery" @input="fetchSchools" placeholder="Search for schools..." class="search-box" />
      <div v-if="error" class="error">
        <p>Error: {{ errorMessage }}</p>
      </div>

      <div v-if="schools.length === 0 && !error && searchQuery" class="no-results">
        <p>No schools found for "{{ searchQuery }}". Please try a different search.</p>
      </div>

      <div class="school-list">
        <div v-for="school in schools.school_list" :key="school.id" class="school-item">
          <div class="school-info">
            <img v-if="school.logo_url" :src="school.logo_url" alt="School Logo" class="school-logo" />
            <h4>{{ school.school_name }}</h4>
          </div>
          <button class="join-button">Join Campaign</button>
        </div>
      </div>

      <div v-if="schools.length === 0 && !error && !searchQuery" class="no-results">
        <p>Please start typing to search for schools.</p> 
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      schools: [],
      searchQuery: '',
      error: false,
      errorMessage: '',
      googleImage: require('@/assets/goolge-store.png'), 
      appleImage: require('@/assets/apple-store.png'),
    };
  },
  mounted() {
    this.fetchSchools();
  },
  methods: {
    async fetchSchools() {
      this.error = false;
      this.errorMessage = '';

      try {
        const query = this.searchQuery.trim();
        const response = await fetch(
          `http://api.devharlemwizardsinabox.com/campaign/campaign_school_list/${query ? `?search=${query}` : ''}`
        );

        if (!response.ok) {
          throw new Error("Failed to fetch data from the server.");
        }

        const data = await response.json();
        this.schools = data;

        if (!data.school_list || data.school_list.length === 0) {
          this.error = false;
        }
      } catch (error) {
        this.error = true;
        this.errorMessage = error.message;
        console.error("Error fetching schools:", error);
      }
    }
  }
};
</script>

<style scoped>
.title {
  color: rgb(208, 4, 4);
  font-size: 28px;
  font-weight: 600;
}

.container {
  padding: 20px;
  max-width: 800px;
  margin: 0 auto 40px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  background-color: white;
  border-radius: 8px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.content {
  text-align: center;
  width: 100%;
}

.app-icons {
  display: flex;
  justify-content: center;
  margin: 1rem 0;
}

.app-image {
  height: 5rem;
  margin: 0 10px;
}

.search-box {
  width: 80%;
  padding: 10px;
  margin-bottom: 20px;
}

.school-logo {
  height: 40px;
  margin-right: 10px;
}

.error,
.no-results {
  text-align: center;
  color: rgb(208, 4, 4);
}

.signup-border {
  display: flex;
  align-items: center;
  text-align: center;
  margin: 20px 0;
}

.signup-border::before,
.signup-border::after {
  content: "";
  flex: 1;
  border-top: 1px solid rgb(176, 172, 172);
  margin: 0 40px;
}

.school-list {
  display: flex;
  flex-direction: column;
  width: 84%;
  margin: auto;
}

.school-item {
  background-color: #f0f0f0;
  padding: 0px 16px;
  margin-bottom: 10px;
  border-radius: 8px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.school-info {
  display: flex;
  align-items: center;
}

.join-button {
  border: 1px solid rgb(208, 4, 4);
  color: rgb(208, 4, 4);
  border-radius: 4px;
  padding: 10px;
  font-size: 14px;
  font-weight: 600;
}
</style>
