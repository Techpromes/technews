<template>
  <div>
    <header class="site-header">
      <h1 class="site-title">TechCrunch News</h1>
      <!-- Add navigation links or other relevant content as needed -->
    </header>

    <div class="tech-crunch-news">
      <h2 class="page-title">Latest News</h2>
      <ul class="article-list">
        <li v-for="article in articles" :key="article.title" class="article-item">
          <div class="article-content">
            <h3 class="article-title">
              <a :href="article.link" target="_blank">{{ article.title.rendered }}</a>
            </h3>
               <div v-html="article.excerpt.rendered"></div>
            <img :src="article.yoast_head_json.og_image[0].url"/>
          </div>
        </li>
      </ul>
    </div>
    <!-- og_image[0].url -->

    <section class="follow-our-news">
      <div class="container">
        <h2>Follow Our News</h2>
        <div class="social-icons">
        <a href="https://twitter.com/Tommymaks123" target="_blank">  <img src=".././assets/twitter.png" alt="Twitter" width="50px" height="50px"></a>
		<a href="https://www.instagram.com/tommymaks123" target="_blank"> <img src=".././assets/instagram.png" alt="Instagram" width="20px" height="20px"></a>
          <!-- Add more social media icons as needed -->
        </div>
      </div>
    </section>

    <section class="subscribe-newsletter">
      <div class="container">
        <h2>Subscribe to Our Newsletter</h2>
        <form>
          <input type="email" placeholder="Enter your email" required>
          <button type="submit">Subscribe</button>
        </form>
      </div>
    </section>

    <footer class="site-footer">
      <p>&copy; 2023 TechCrunch News. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      articles: [],
    };
  },
  mounted() {
    const apiUrl = 'https://techcrunch.com/wp-json/wp/v2/posts';

    axios.get(apiUrl)
      .then(response => {
        console.log(response)
         this.articles = response.data;
      })
      .catch(error => {
        console.error('Error fetching TechCrunch news:', error);
      });
  },
};
</script>

<style scoped>
/* Your existing styles */

.site-header {
  background-color: #333;
  color: #fff;
  padding: 10px;
  text-align: center;
}

.site-title {
  font-size: 2em;
}

.follow-our-news,
.subscribe-newsletter {
  background-color: #f8f8f8;
  padding: 40px 0;
  text-align: center;
}

social-icons {
  display: flex;
  justify-content: center;
  align-items: center;
}

.social-icons a {
  margin: 0 10px;
}

.social-icons img {
  border-radius: 50%;
   width: 30px; /* Adjust the width as needed */
  height: 30px; /* Adjust the height as needed */
  margin: 0 5px; /* Add margin for spacing between icons */
}

.subscribe-newsletter form {
  margin-top: 20px;
}
.subscribe-newsletter {
  margin-bottom: 40px; /* Adjust as needed */
}

.site-footer {
  background-color: #333;
  color: #fff;
  text-align: center;
  padding: 10px;
  position: fixed;
  bottom: 0;
  width: 100%;
}
.subscribe-newsletter .container {
  text-align: center;
}

.subscribe-newsletter h2 {
  font-size: 1.8em;
  margin-bottom: 15px;
  color: #333;
}

.form-group {
  display: flex;
  justify-content: center;
  align-items: center;
}

input[type="email"] {
  padding: 10px;
  width: 250px;
  border: 1px solid #ddd;
  border-radius: 5px;
  margin-right: 10px;
}

button {
  background-color: #333;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
.article-content img {
  max-width: 100%; /* Set a maximum width for responsiveness */
  max-height: 200px; /* Set a maximum height to limit the size */
  width: auto; /* Maintain aspect ratio */
  border-radius: 10px; /* Add a rounded border */
  margin-top: 10px; /* Add space above the image */
}
</style>
