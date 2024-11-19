<script setup>
import { ref } from "vue";

// 1. For at kunne POSTE data til vores rest api skal vi logges ind - authenticates. Vi anvender typisk jwt (json web tokens til det. Ka' I huske det fra headless cms 2. sem?). Læs om det her: https://en-gb.wordpress.org/plugins/jwt-auth/ særligt under "configuration", "NAMESPACE AND ENDPOINTS" og "REQUESTING/ GENERATING TOKEN". Skriv så en funktion getToken() der gemmer token i sessionstorage

// 2. Next up - nu skal vi kunne LAVE en ny post!
//  - Overvej i grupper i 5 minutter HVAD der skal til for at løse denne udfordring. I behøver ikke have komplette svar, men hvilke byggesten skal der til
//  - Undervejs skal I sikkert google hvilke data der skal sendes for at lave en ny post, hvad søger I på for at finde et fungerende svar?
//  - Skriv så metoden addPost() og send data med POST metoden - overvåg trafikken i network tab og se hvordan det fungerer

// stuff we need here from the secret file!
import { baseEndpoint, postsUrl, verifyUserEndpoint, username, password } from "./login_and_urls.js";

// State
const posts = ref();

// getToken();
fetchPosts()

function getToken() {
  const userLoginInfo = {
    // Når key og value er det samme kan man bare skriev det en gang...smart, hva?
    username: username,
    password,
  };

  fetch(baseEndpoint + verifyUserEndpoint, {})
    .then()
    .then()
    .catch();
}

function fetchPosts() {
  fetch(baseEndpoint + postsUrl)
    .then((res) => res.json())
    .then((data) => {
      posts.value = data;
    })
    .catch((err) => console.log(err));
}
</script>

<template>
  <h1>Marks opskrifter</h1>
  <div class="container">
    <article v-for="post in posts" :key="post.id">
      <h2>{{ post.title.rendered }}</h2>
      <div v-html="post.content.rendered"></div>
    </article>
  </div>
</template>

<style scoped>
.container {
  max-width: 1024px;
  margin: 0 auto;
  padding: 2rem;
  box-shadow: 0 0 3px 3px rgba(0, 0, 0, 0.3);
  border-radius: 6px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

.container img {
  max-width: 100%;
}

article {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

form {
  width: 500px;
  background: #eee;
  padding: 1rem;
  margin: 1rem auto;
}

form div {
  padding: 0.5rem;
  display: flex;
  width: 400px;
  justify-content: space-between;
}

form button {
  padding: 1rem 2rem;
  text-align: center;
  border: none;
  background: orange;
  color: white;
  font-weight: bold;
  border-radius: 6px;
  margin: 1rem auto;
  transition: 0.3s all;
}

form button:hover {
  background: rgb(219, 149, 19);
}
</style>
