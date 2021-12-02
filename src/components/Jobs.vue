<template>
  <main class="container">
    <div class="filter-block" v-show="filters.length">
      <ul class="filters">
        <li v-for="filter in filters" :key="filter">
          <span class="filter">{{ filter }}</span>
          <span class="remove-filters-btn" @click="removeFilter(filter)"
            ><svg xmlns="http://www.w3.org/2000/svg" width="14" height="14">
              <path
                fill="#FFF"
                fill-rule="evenodd"
                d="M11.314 0l2.121 2.121-4.596 4.596 4.596 4.597-2.121 2.121-4.597-4.596-4.596 4.596L0 11.314l4.596-4.597L0 2.121 2.121 0l4.596 4.596L11.314 0z"
              /></svg
          ></span>
        </li>
      </ul>
      <button class="clear-btn" @click="clearFilters">Clear</button>
    </div>
    <div
      v-for="job in jobs"
      class="job-card"
      :key="job.id"
      :class="{ featured_border: job.featured }"
    >
      <div class="job-info">
        <div class="logo-container">
          <img :src="job.logo" alt="" />
        </div>
        <div class="job-company-info">
          <section>
            <div class="company-new-featured">
              <p class="company">{{ job.company }}</p>
              <p v-if="job.new" class="new">NEW!</p>
              <p v-if="job.featured" class="featured">FEATURED</p>
            </div>

            <h2 class="position">{{ job.position }}</h2>
            <div class="extra-info">
              {{ job.postedAt }} <span>•</span> {{ job.contract }}
              <span>•</span>
              {{ job.location }}
            </div>
          </section>
        </div>

        <section class="languages">
          <p class="skills" @click="filterRole(job.role)">
            {{ job.role }}
          </p>
          <p class="skills" @click="filterRole(job.level)">
            {{ job.level }}
          </p>
          <p
            v-for="tool in job.tools"
            :key="tool"
            class="skills"
            @click="filterRole(tool)"
          >
            {{ tool }}
          </p>
          <p
            v-for="lang in job.languages"
            :key="lang"
            class="skills"
            @click="filterRole(lang)"
          >
            {{ lang }}
          </p>
        </section>
      </div>
    </div>
  </main>
</template>

<script>
import allJobs from '../data.json';

export default {
  data() {
    return {
      jobs: allJobs,
      filters: [],
    };
  },
  methods: {
    filterRole(skill) {
      if (!this.filters.includes(skill)) {
        this.filters.push(skill);
      }

      this.jobs = this.jobs.filter((job) => {
        return (
          job.role.includes(skill) ||
          job.level.includes(skill) ||
          job.languages.includes(skill) ||
          job.tools.includes(skill)
        );
      });
      window.scrollTo(0, 0);
    },
    removeFilter(skill) {
      this.filters = this.filters.filter((item) => {
        return skill !== item;
      });

      this.jobs = allJobs;

      for (let i = 0; i < this.filters.length; i++) {
        // console.log(this.filters[i]);
        this.filterRole(this.filters[i]);
      }
    },
    clearFilters() {
      this.filters.length = 0;
      this.jobs = allJobs;
    },
  },
};
</script>

<style>
.container {
  max-width: 80vw;
  margin-inline: auto;
  padding-bottom: 6rem;
}

@media (max-width: 420px) {
  .container {
    max-width: 90vw;
  }
}
.job-card,
.filter-block {
  margin-bottom: 1.5rem;
  background-color: #fff;
  padding: 1.5rem;
  border-radius: 0.3rem;
  box-shadow: 0px 15px 15px -3px hsla(180, 8%, 52%, 0.2);
  position: relative;
}

@media (max-width: 650px) {
  .job-card {
    margin-bottom: 3rem;
  }
}

.filter-block {
  top: unset;
  bottom: 5rem;
  display: flex;
  margin-bottom: -2rem;
  padding: 0 1.5rem;
  align-items: center;
  justify-content: space-between;
}
@media (max-width: 465px) {
  .filter-block,
  .job-card {
    padding: 1rem;
  }
}
@media (max-width: 375px) {
  .filter-block {
    padding-block: 0.5rem;
  }
}
.clear-btn {
  color: hsl(180, 29%, 50%);
  font-weight: 700;
  font-size: clamp(0.7rem, 1vw, 1.5rem);
  font-family: inherit;
  border: none;
  background: none;
  cursor: pointer;
}
.clear-btn:hover {
  text-decoration: underline;
}
.filters {
  list-style-type: none;
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  padding-left: 0;
}
.filters li {
  font-size: clamp(0.6rem, 1vw, 1rem);
  font-weight: 700;
  padding-left: 0.4rem;
  border-radius: 5px;
  background-color: hsl(180, 52%, 96%);
  color: hsl(180, 29%, 50%);
  display: flex;
  align-items: center;
}
.filter {
  margin: 0.4rem;
  margin-left: 0;
}
.remove-filters-btn {
  background-color: hsl(180, 29%, 50%);
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  height: 100%;
  padding: 0.5rem;
  display: flex;
  align-items: center;
  cursor: pointer;
  transition: 300ms all;
}
.remove-filters-btn:hover {
  background-color: #000;
}
.featured_border {
  border-left: 5px solid hsl(180, 29%, 50%);
}
.job-info > section * {
  margin-bottom: 0.4rem;
}
.job-info {
  display: flex;
  gap: 15%;
  justify-content: space-between;
}

.job-company-info {
  display: flex;
  align-items: center;
  gap: 5%;
  width: 40%;
}

.logo-container {
  margin-right: -12%;
  min-width: 80px;
}

img {
  min-width: 100%;
}
@media (max-width: 790px) {
  .logo-container {
    min-width: 50px;
  }
}

@media (max-width: 650px) {
  .logo-container {
    position: relative;
    bottom: 3rem;
    width: 10%;
    margin: 0;
  }
  .job-info {
    flex-direction: column;
  }
  .job-company-info {
    border-bottom: 1px solid hsla(180, 8%, 52%, 0.5);
    margin-bottom: 1rem;
    padding-bottom: 1rem;
    width: 100%;
  }
  .job-company-info section {
    margin-top: -2rem;
  }
}

@media (max-width: 475px) {
  .logo-container {
    bottom: 2.5rem;
  }
}

.company-new-featured {
  display: flex;
  gap: 1rem;
  align-items: center;
}
.company {
  color: hsl(180, 29%, 50%);
  font-size: clamp(0.7rem, 1vw, 1.5rem);
  font-weight: 700;
  margin-bottom: 0.5rem;
}
.new,
.featured {
  position: relative;
  bottom: 4px;
  padding: 8px 8px;
  padding-bottom: 4px;
  font-size: clamp(0.4rem, 0.8vw, 1rem);
  font-weight: 700;
  color: #fff;
  border-radius: 18px;
}
.new {
  background-color: hsl(180, 29%, 50%);
}
.featured {
  background-color: #000;
}
.position {
  color: hsl(180, 14%, 20%);
  font-size: clamp(1rem, 1.3vw, 3rem);
  font-weight: 700;
  cursor: pointer;
  margin-bottom: 0.5rem;
}
.position:hover {
  color: hsl(180, 29%, 50%);
}
.extra-info {
  color: hsl(180, 8%, 52%);
  font-size: clamp(0.6rem, 1vw, 1rem);
}
.extra-info span {
  margin-inline: 0.3rem;
}
.languages {
  display: flex;
  gap: 0.8rem;
  align-items: center;
  flex-wrap: wrap;
}

@media (max-width: 1050px) {
  .languages {
    gap: 0.7rem;
  }
}

.skills {
  font-size: clamp(0.6rem, 0.8vw, 1rem);
  font-weight: 700;
  padding: 0.5rem 0.8rem;
  padding-bottom: 0.3rem;
  border-radius: 5px;
  background-color: hsl(180, 52%, 96%);
  color: hsl(180, 29%, 50%);
  cursor: pointer;
  transition: 400ms all;
}
.skills:hover {
  color: hsl(180, 52%, 96%);
  background-color: hsl(180, 29%, 50%);
}
</style>
