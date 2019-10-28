<template>
  <Layout>
    <section class="heroarea">
      <h1>My name is George Williams.</h1>
    </section>
    <hr />
    <section class="heroarea">
      <p>I'm a music producer currently based in Norfolk, UK.</p>
    </section>
    <section class="projects">
      <g-image
        class="project-thumbnail"
        src="~/george4.jpg"
        alt="George Williams - Georna Sound, Norfolk, UK, Music Production"
      ></g-image>
    </section>
    <section class="contactstyle">
      <h1>I specialise in helping singer/songwriters transform their song ideas into complete Pop/Electronic music productions.</h1>
      <hr />
    </section>
    <section class="heroarea">
      <p></p>
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
    <section class="contactstyle">
      <a class="link" href="https://instagram.com/geornasound">Instagram.</a>
    </section>
    <section>
      <p></p>
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

.heroarea {
  margin: 0 2rem;
  margin-top: 1rem;
  margin-bottom: 4rem;
  width: 90%;
}
.heroarea h1 {
  font-size: 5.5rem;
}

.heroarea a {
  font-size: 5rem;
}

.heroarea p {
  font-size: 2rem;
}

.contactstyle {
  margin: 0 2rem;
  width: 90%;
}
.contactstyle h1 {
  font-size: 4.5vh;
}

.contactstyle a {
  font-size: 4vh;
}

.contactstyle p {
  font-size: 2vh;
}
</style>
