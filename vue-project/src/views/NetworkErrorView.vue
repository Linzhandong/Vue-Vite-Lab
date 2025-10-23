<template>
  <div class="network-error">
    <h1>Uh-Oh!</h1>
    <h3>
      It looks like you're experiencing some network issues, please take a breath and
      <a href="#" @click="$router.go(-1)">click here</a> to try again.
    </h3>
    <p>If the problem persists, please check your internet connection and try again later.</p>
    <RouterLink :to="{ name: 'event-list-view' }" class="home-link">Go to Home Page</RouterLink>
  </div>
</template>

<style scoped>
.network-error {
  padding: 40px;
  text-align: center;
}

.network-error h1 {
  font-size: 48px;
  color: #e67e22;
  margin-bottom: 20px;
}

.network-error h3 {
  font-size: 20px;
  color: #2c3e50;
  margin-bottom: 15px;
  line-height: 1.5;
}

.network-error p {
  font-size: 16px;
  color: #7f8c8d;
  margin-bottom: 25px;
}

.network-error a {
  color: #3498db;
  text-decoration: none;
}

.network-error a:hover {
  text-decoration: underline;
}

.home-link {
  display: inline-block;
  padding: 10px 20px;
  background-color: #3498db;
  color: white;
  text-decoration: none;
  border-radius: 4px;
  font-weight: bold;
  margin-top: 10px;
}

.home-link:hover {
  background-color: #2980b9;
}
</style>