<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GhostWorker - Software & Consulting Services</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    body {
      font-family: 'Arial', sans-serif;
      background-color: #000000;
      color: #e5e7eb;
      line-height: 1.6;
    }
    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 1rem;
    }
    header {
      background-color: #000000;
      color: #A67B00;
      padding: 1rem 0;
      position: sticky;
      top: 0;
      z-index: 1000;
      border-bottom: 2px solid #A67B00;
    }
    .header-content {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .logo {
      height: 50px;
    }
    nav ul {
      list-style: none;
      display: flex;
      gap: 1.5rem;
    }
    nav a {
      color: #A67B00;
      text-decoration: none;
      font-size: 1.1rem;
      padding: 0.5rem;
      transition: color 0.3s;
    }
    nav a:hover, nav a.active {
      color: #D4A017; /* Lighter gold for hover/active */
    }
    .cart-button {
      background: none;
      border: 2px solid #A67B00;
      color: #A67B00;
      font-size: 1.1rem;
      cursor: pointer;
      padding: 0.5rem 1rem;
      border-radius: 4px;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
    .cart-button:hover {
      background-color: #A67B00;
      color: #000000;
    }
    .cart-count {
      background-color: #D4A017;
      color: #000000;
      border-radius: 50%;
      padding: 0.2rem 0.5rem;
      font-size: 0.9rem;
    }
    section {
      padding: 3rem 0;
    }
    #home {
      position: relative;
      height: 70vh;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      color: #e5e7eb;
      background: url('https://cdn.vecteezy.com/packs/media/videos/preview/1103/hi-tech-digital-circuit-board-abstract-background-4k-video_s-v1.mp4') no-repeat center center/cover;
    }
    #home::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.7);
      z-index: 1;
    }
    #home .container {
      position: relative;
      z-index: 2;
    }
    #home h2 {
      font-size: 2.5rem;
      margin-bottom: 1rem;
      color: #A67B00;
    }
    #home p {
      font-size: 1.2rem;
      max-width: 600px;
      margin: 0 auto;
      color: #e5e7eb;
    }
    #products h2 {
      font-size: 2rem;
      margin-bottom: 1rem;
      text-align: center;
      color: #A67B00;
    }
    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 1.5rem;
      padding: 2rem 0;
    }
    .product-card {
      background-color: #1a1a1a;
      border-radius: 8px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.5);
      overflow: hidden;
      transition: transform 0.3s;
    }
    .product-card:hover {
      transform: scale(1.05);
    }
    .product-card img {
      width: 100%;
      height: 200px;
      object-fit: cover;
    }
    .product-card-content {
      padding: 1.5rem;
    }
    .product-card h2 {
      font-size: 1.5rem;
      color: #A67B00;
      margin-bottom: 0.5rem;
    }
    .product-card p.description {
      color: #b0b0b0;
      font-size: 1rem;
      margin-bottom: 1rem;
    }
    .product-card p.price {
      font-size: 1.25rem;
      font-weight: bold;
      color: #D4A017;
      margin-bottom: 0.5rem;
    }
    .product-card ul {
      list-style: disc;
      padding-left: 1.5rem;
      color: #b0b0b0;
      font-size: 0.9rem;
      margin-bottom: 0.5rem;
    }
    .product-card p.info {
      color: #b0b0b0;
      font-size: 0.9rem;
      margin-bottom: 0.5rem;
    }
    .product-card button {
      width: 100%;
      padding: 0.75rem;
      background-color: #A67B00;
      color: #000000;
      border: none;
      border-radius: 4px;
      font-size: 1rem;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    .product-card button:disabled {
      background-color: #4b4b4b;
      cursor: not-allowed;
    }
    .product-card button:hover:not(:disabled) {
      background-color: #D4A017;
    }
    .cart-message {
      text-align: center;
      color: #D4A017;
      font-size: 0.9rem;
      margin-top: 0.5rem;
    }
    #history {
      background-color: #1a1a1a;
    }
    #history h2 {
      font-size: 2rem;
      margin-bottom: 1rem;
      text-align: center;
      color: #A67B00;
    }
    #history p {
      font-size: 1.1rem;
      max-width: 800px;
      margin: 0 auto 1rem;
      color: #b0b0b0;
    }
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.7);
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }
    .modal-content {
      background-color: #1a1a1a;
      padding: 2rem;
      border-radius: 8px;
      max-width: 500px;
      width: 90%;
      max-height: 80vh;
      overflow-y: auto;
      position: relative;
      color: #e5e7eb;
      border: 2px solid #A67B00;
    }
    .modal-content h2 {
      font-size: 1.5rem;
      margin-bottom: 1rem;
      color: #A67B00;
    }
    .modal-content ul {
      list-style: none;
      margin-bottom: 1rem;
    }
    .modal-content li {
      padding: 0.5rem 0;
      border-bottom: 1px solid #4b4b4b;
      display: flex;
      justify-content: space-between;
    }
    .modal-content button {
      padding: 0.5rem 1rem;
      background-color: #D4A017;
      color: #000000;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    .modal-content button:hover {
      background-color: #A67B00;
    }
    .close-modal {
      position: absolute;
      top: 1rem;
      right: 1rem;
      font-size: 1.5rem;
      cursor: pointer;
      color: #A67B00;
    }
    footer {
      background-color: #1a1a1a;
      color: #e5e7eb;
      padding: 2rem 0;
      text-align: center;
    }
    .contact-info {
      margin-top: 1rem;
      font-size: 1rem;
    }
    .contact-info a {
      color: #D4A017;
      text-decoration: none;
    }
    .contact-info a:hover {
      text-decoration: underline;
    }
    html {
      scroll-behavior: smooth;
    }
    @media (max-width: 600px) {
      .product-grid {
        grid-template-columns: 1fr;
      }
      header h1 {
        font-size: 1.5rem;
      }
      nav ul {
        flex-direction: column;
        gap: 0.5rem;
      }
      .header-content {
        flex-direction: column;
        gap: 1rem;
      }
      #home h2 {
        font-size: 1.8rem;
      }
      #home p {
        font-size: 1rem;
      }
      .contact-info {
        font-size: 0.9rem;
      }
    }
  </style>
</head>
<body>
  <header>
    <div class="container header-content">
      <img src="logo.png" alt="GhostWorker Logo" class="logo">
      <nav>
        <ul>
          <li><a href="#home" class="nav-link active">Home</a></li>
          <li><a href="#products" class="nav-link">Products</a></li>
          <li><a href="#history" class="nav-link">Our History</a></li>
        </ul>
      </nav>
      <button class="cart-button">
        Cart <span class="cart-count">0</span>
      </button>
    </div>
  </header>
  <main>
    <section id="home">
      <div class="container">
        <h2>Welcome to GhostWorker</h2>
        <p>In GhostWorker, discover tailored process and data solutions designed to streamline your daily tasks, boost efficiency, and deliver measurable results—so you can focus on what truly matters.</p>
      </div>
    </section>
    <section id="products">
      <div class="container">
        <h2>Our Products</h2>
        <div class="product-grid">
          <div class="product-card" data-handle="data-analytics">
            <img src="https://cdn.shopify.com/s/files/1/0956/8065/9751/files/data_analisis.jpg?v=1761168765" alt="Data Analytics">
            <div class="product-card-content">
              <h2>Data Analytics</h2>
              <p class="description">Converts complex datasets into actionable insights using statistical analysis, visualization, and predictive modeling. Enables informed decision-making by identifying trends, inefficiencies, and strategic opportunities within business operations.</p>
              <p class="price">$1500.00</p>
              <ul>
                <li>technical support</li>
                <li>customizable interface</li>
                <li>real time updates</li>
                <li>data import export</li>
                <li>cloud based</li>
                <li>built in templates</li>
              </ul>
              <p class="info">OS: windows, macos</p>
              <p class="info">For: individual, large enterprise, small business, medium sized business enterprise</p>
              <p class="info stock">Stock: 2</p>
              <button data-price="1500.00">Add to Cart</button>
              <p class="cart-message"></p>
            </div>
          </div>
          <div class="product-card" data-handle="etl-pipelines">
            <img src="https://cdn.shopify.com/s/files/1/0956/8065/9751/files/ETLPIPELINE.png?v=1761168863" alt="ETL Pipelines">
            <div class="product-card-content">
              <h2>ETL Pipelines</h2>
              <p class="description">Builds and manages ETL (Extract, Transform, Load) pipelines for seamless data integration across multiple sources. Focuses on reliability, data quality, and performance to ensure accurate and efficient data processing for downstream analytics and automation initiatives.</p>
              <p class="price">$2000.00</p>
              <ul>
                <li>cloud based</li>
                <li>data import export</li>
                <li>automatic updates</li>
                <li>technical support</li>
              </ul>
              <p class="info">For: large enterprise, medium sized business enterprise, small business</p>
              <p class="info stock">Stock: 2</p>
              <button data-price="2000.00">Add to Cart</button>
              <p class="cart-message"></p>
            </div>
          </div>
          <div class="product-card" data-handle="process-automation">
            <img src="https://cdn.shopify.com/s/files/1/0956/8065/9751/files/ProcessAutomation.jpg?v=1761168696" alt="Process Automation">
            <div class="product-card-content">
              <h2>Process Automation</h2>
              <p class="description">Implements end-to-end automation solutions to streamline operations and reduce manual effort. Focuses on achieving measurable productivity improvements through smart integration of technology and process engineering principles.</p>
              <p class="price">$3500.00</p>
              <p class="info">For: medium sized business enterprise, large enterprise, small business</p>
              <p class="info stock">Stock: 2</p>
              <button data-price="3500.00">Add to Cart</button>
              <p class="cart-message"></p>
            </div>
          </div>
          <div class="product-card" data-handle="process-consulting">
            <img src="https://cdn.shopify.com/s/files/1/0956/8065/9751/files/ProcessConsultingimg.jpg?v=1761168362" alt="Process Consulting">
            <div class="product-card-content">
              <h2>Process Consulting</h2>
              <p class="description">Provides strategic guidance to help businesses optimize workflows, eliminate inefficiencies, and improve overall performance. Combines industrial engineering methods with data-driven insights to design lean, scalable, and sustainable processes.</p>
              <p class="price">$2500.00</p>
              <p class="info">For: medium sized business enterprise, large enterprise, small business</p>
              <p class="info stock">Stock: 10</p>
              <button data-price="2500.00">Add to Cart</button>
              <p class="cart-message"></p>
            </div>
          </div>
          <div class="product-card" data-handle="robotic-process-automation">
            <img src="https://cdn.shopify.com/s/files/1/0956/8065/9751/files/RPA_image.jpg?v=1761168820" alt="Robotic Process Automation">
            <div class="product-card-content">
              <h2>Robotic Process Automation</h2>
              <p class="description">Designs and deploys robotic automation solutions to handle repetitive digital tasks efficiently. Ensures consistency, accuracy, and speed while freeing human resources for higher-value analysis and decision-making.</p>
              <p class="price">$1500.00</p>
              <ul>
                <li>technical support</li>
                <li>customizable interface</li>
                <li>cloud based</li>
                <li>automatic updates</li>
                <li>data import export</li>
              </ul>
              <p class="info">For: small business, large enterprise, medium sized business enterprise</p>
              <p class="info stock">Stock: Out of Stock</p>
              <button data-price="1500.00" disabled>Add to Cart</button>
              <p class="cart-message"></p>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section id="history">
      <div class="container">
        <h2>Our History</h2>
        <p>Our journey began with a vision to bridge the worlds of engineering, automation, and data. Founded by Julio Félix, an industrial and data engineer with years of practical experience leading innovative projects, our company was built on a belief that efficiency and technology are the twin engines of modern business transformation.</p>
        <p>From optimizing industrial processes to developing automated digital ecosystems, we have grown through a passion for solving complex challenges with simple, effective solutions. Every project—from designing ETL pipelines and process automation systems to implementing analytics and RPA solutions—reflects our commitment to precision, innovation, and measurable results.</p>
        <p>Today, we partner with organizations that want to move forward—integrating smart technology, automation, and strategic insight to achieve excellence. Our history is defined not just by what we’ve built, but by how we’ve empowered others to innovate, optimize, and thrive.</p>
      </div>
    </section>
  </main>
  <div class="modal" id="cart-modal">
    <div class="modal-content">
      <span class="close-modal">&times;</span>
      <h2>Shopping Cart</h2>
      <ul id="cart-items"></ul>
      <p id="cart-total">Total: $0.00</p>
      <button id="clear-cart">Clear Cart</button>
    </div>
  </div>
  <footer>
    <div class="container">
      <p>&copy; 2025 GhostWorker. All rights reserved.</p>
      <div class="contact-info">
        <p>Instagram: <a href="https://www.instagram.com/GhostWorker" target="_blank">@GhostWorker</a></p>
        <p>Email: <a href="mailto:ghost_worker@outlook.com">ghost_worker@outlook.com</a></p>
        <p>Phone: <a href="tel:+18296473440">+1 829 647 3440</a></p>
      </div>
    </div>
  </footer>
  <script>
    let cart = [];

    function updateCartDisplay() {
      const cartItems = document.getElementById('cart-items');
      const cartTotal = document.getElementById('cart-total');
      const cartCount = document.querySelector('.cart-count');

      cartItems.innerHTML = '';
      let total = 0;
      let totalItems = 0;

      cart.forEach(item => {
        const li = document.createElement('li');
        li.textContent = `${item.title} (x${item.quantity})`;
        cartItems.appendChild(li);
        total += item.price * item.quantity;
        totalItems += item.quantity;
      });

      cartTotal.textContent = `Total: $${total.toFixed(2)}`;
      cartCount.textContent = totalItems;
    }

    document.querySelectorAll('.product-card button').forEach(button => {
      button.addEventListener('click', () => {
        const card = button.closest('.product-card');
        const title = card.querySelector('h2').textContent;
        const price = parseFloat(button.getAttribute('data-price'));
        const stockElement = card.querySelector('.info.stock');
        const stockText = stockElement ? stockElement.textContent : '';
        const messageElement = card.querySelector('.cart-message');

        if (stockText.includes('Out of Stock')) {
          messageElement.textContent = `${title} is out of stock.`;
        } else {
          const existingItem = cart.find(item => item.title === title);
          if (existingItem) {
            messageElement.textContent = `${title} is already in the cart.`;
          } else {
            cart.push({ title, price, quantity: 1 });
            updateCartDisplay();
            messageElement.textContent = `${title} added to cart!`;
          }
        }

        setTimeout(() => {
          messageElement.textContent = '';
        }, 2000);
      });
    });

    document.querySelectorAll('.nav-link').forEach(link => {
      link.addEventListener('click', (e) => {
        e.preventDefault();
        const sectionId = link.getAttribute('href').substring(1);
        document.getElementById(sectionId).scrollIntoView({ behavior: 'smooth' });
        document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
        link.classList.add('active');
      });
    });

    const cartButton = document.querySelector('.cart-button');
    const cartModal = document.getElementById('cart-modal');
    const closeModal = document.querySelector('.close-modal');

    cartButton.addEventListener('click', () => {
      cartModal.style.display = 'flex';
    });

    closeModal.addEventListener('click', () => {
      cartModal.style.display = 'none';
    });

    window.addEventListener('click', (event) => {
      if (event.target === cartModal) {
        cartModal.style.display = 'none';
      }
    });

    document.getElementById('clear-cart').addEventListener('click', () => {
      cart = [];
      updateCartDisplay();
    });
  </script>
</body>
</html>
