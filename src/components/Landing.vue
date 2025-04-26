<template>
  <div class="container">
    <!-- Header -->
    <header class="header">
      <h1 class="logo">InvoiceHero</h1>
      <button class="cta-button">Start</button>
    </header>

    <!-- Hero Section -->
    <section class="hero">
      <h2>Create Professional Invoices in Minutes</h2>
      <p>Fast, easy, and customizable invoicing for your business needs.</p>
      <button class="start-button">Start Now</button>
    </section>

    <!-- Features -->
    <section class="features">
      <div class="feature">
        <h3>Simple & Fast</h3>
        <p>Create invoices without any complexity or long forms.</p>
      </div>
      <div class="feature">
        <h3>Customizable</h3>
        <p>Personalize your invoices with your logo and branding.</p>
      </div>
      <div class="feature">
        <h3>Instant Download</h3>
        <p>Get your invoices in PDF format instantly.</p>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <p>© 2025 InvoiceHero. All rights reserved.</p>
    </footer>
  </div>
</template>

<script setup>
// You can later link the buttons to navigate to other pages
</script>

<style scoped>
/* General Styles */
body {
  margin: 0;
  font-family: 'Poppins', sans-serif;
  background: linear-gradient(to right, #667eea, #764ba2);
  color: white;
}

/* Container */
.container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

/* Header */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 40px;
}

.logo {
  font-size: 2rem;
  font-weight: bold;
}

.cta-button {
  background-color: white;
  color: #667eea;
  border: none;
  padding: 10px 25px;
  border-radius: 30px;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.3s ease;
}

.cta-button:hover {
  background-color: #f1f1f1;
}

/* Hero Section */
.hero {
  flex: 1;
  text-align: center;
  padding: 80px 20px;
}

.hero h2 {
  font-size: 3rem;
  margin-bottom: 20px;
}

.hero p {
  font-size: 1.2rem;
  margin-bottom: 40px;
}

.start-button {
  background-color: white;
  color: #667eea;
  border: none;
  padding: 15px 40px;
  border-radius: 30px;
  font-size: 1.2rem;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.3s ease;
}

.start-button:hover {
  background-color: #f1f1f1;
}

/* Features */
.features {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 60px 20px;
  background-color: rgba(0, 0, 0, 0.1);
}

.feature {
  flex: 1;
  min-width: 250px;
  max-width: 300px;
  margin: 20px;
  text-align: center;
}

.feature h3 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

.feature p {
  font-size: 1rem;
}

/* Footer */
.footer {
  text-align: center;
  padding: 20px;
  background-color: rgba(0, 0, 0, 0.2);
  font-size: 0.9rem;
}
</style>
