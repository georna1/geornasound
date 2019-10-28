<template>
  <Layout>
    <section class="heroarea">
      <h1>My name is George Williams.</h1>
    </section>
    <section class="heroarea">
      <p>I'm a music producer currently based in Norfolk, UK.</p>
    </section>
    <section class="heroarea_b">
      <g-image
        class="project-thumbnail2"
        src="~/george2.jpg"
        alt="George Williams - Georna Sound, Norfolk, UK, Music Production"
      ></g-image>
    </section>
    <section class="projects">
      <article
        @click="goTo($event, project.node.path)"
        class="project"
        v-for="project in $page.projects.edges"
        :key="project.node.id"
      >
        <g-image
          class="project-thumbnail"
          :src="project.node.thumbnail.src"
          :alt="project.node.title"
        ></g-image>
        <ProjectMeta
          :title="project.node.title"
          :categories="project.node.categories"
          :year="project.node.year"
        />
      </article>
    </section>
    <section class="contactstyle">
      <h1>Let's Talk About Your Music Project.</h1>
    </section>
    <section class="contactstyle">
      <a class="link" :href="`mailto:${data.email}`">Email.</a>
    </section>
    <section class="contactstyle">
      <p>Or reach out on Facebook or Instagram:</p>
    </section>
    <section class="contactstyle">
      <a class="link" href="https://facebook.com/geornasound">Facebook.</a>
    </section>
    <section class="contactstyle2">
      <a class="link" href="https://instagram.com/geornasound">Instagram.</a>
    </section>
  </Layout>
</template>

<page-query>
query Projects {
  projects: allProject {
    edges {
      node { 
        id
        path
        title
        year
        thumbnail
        categories
      }
    }
  }
}
</page-query>

<script>
import ProjectMeta from "@/components/ProjectMeta";
import data from "@/data/theme.json";

export default {
  name: "Header",
  data() {
    return {
      data
    };
  },
  computed: {
    siteName() {
      return data.header_title.split(" ");
    },
    multiLine() {
      return this.siteName.length >= 1;
    }
  },
  components: {
    ProjectMeta
  },
  metaInfo: {
    titleTemplate: require("../data/theme.json").site_name
  },
  methods: {
    goTo(event, route) {
      const distanceScrolled = window.pageYOffset;
      const elementPosition = event.target.getBoundingClientRect().top;
      const totalOffset = distanceScrolled + elementPosition;
      const finalPosition = totalOffset - 167;

      // Scroll window so that the thumbnail is 12rem from the
      // top of the browser window, this will make a seamless transition.
      window.scrollTo({ top: finalPosition, behavior: "smooth" });

      // Now, navigate to the project page
      setTimeout(() => {
        this.$router.push(route);
      }, 450);
    }
  }
};
</script>

<style lang="scss" scoped>
.projects {
  margin: 0 2rem;
}
.project {
  width: 100%;
  margin-bottom: 4rem;
  cursor: pointer;
}
.project-thumbnail {
  display: block;
  width: 100%;
}

.project-thumbnail2 {
  width: 100%;
}

.heroarea {
  margin: 0 3rem;
  margin-top: 4rem;
  margin-bottom: 4rem;
  width: 100%;
}
.heroarea h1 {
  font-size: 6rem;
  width: 100%;
  margin: 0 1rem;
}

.heroarea a {
  font-size: 5rem;
  margin: 0 2rem;
}

.heroarea p {
  font-size: 2rem;
  margin: 0 1rem;
}

.contactstyle {
  margin: 0 4rem;
  width: 100%;
}
.contactstyle h1 {
  font-size: 4.5vh;
  width: 100%;
  margin: 3 0rem;
}

.contactstyle a {
  font-size: 4vh;
  margin: 3 8rem;
}

.contactstyle2 a {
  font-size: 4vh;
  margin: 3 8rem;
  margin-bottom: 4rem;
}

.contactstyle p {
  font-size: 2vh;
  margin: 3 0rem;
}
</style>
