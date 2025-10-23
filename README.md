<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GhostWorker - Soluciones de Datos Personalizadas</title>
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
      color: #ff851a;
      padding: 1rem 0;
      position: sticky;
      top: 0;
      z-index: 1000;
      border-bottom: 2px solid #ff851a;
    }
    .header-content {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .header-left {
      display: flex;
      align-items: center;
      gap: 2rem;
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
      color: #ff851a;
      text-decoration: none;
      font-size: 1.1rem;
      padding: 0.5rem;
      transition: color 0.3s;
    }
    nav a:hover, nav a.active {
      color: #ffaa66;
    }
    .language-toggle {
      background: none;
      border: 2px solid #ff851a;
      color: #ff851a;
      font-size: 1rem;
      cursor: pointer;
      padding: 0.5rem 1rem;
      border-radius: 4px;
      transition: all 0.3s;
    }
    .language-toggle:hover {
      background-color: #ff851a;
      color: #000000;
    }
    .cart-button {
      background: none;
      border: 2px solid #ff851a;
      color: #ff851a;
      font-size: 1.1rem;
      cursor: pointer;
      padding: 0.5rem 1rem;
      border-radius: 4px;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
    .cart-button:hover {
      background-color: #ff851a;
      color: #000000;
    }
    .cart-count {
      background-color: #ffaa66;
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
      background: url('background.jpg') no-repeat center center/cover;
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
      color: #ff851a;
    }
    #home p {
      font-size: 1.2rem;
      max-width: 600px;
      margin: 0 auto;
      color: #e5e7eb;
    }
    #products h2, #history h2 {
      font-size: 2rem;
      margin-bottom: 1rem;
      text-align: center;
      color: #ff851a;
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
      color: #ff851a;
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
      color: #ffaa66;
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
      background-color: #ff851a;
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
      background-color: #ffaa66;
    }
    .cart-message {
      text-align: center;
      color: #ffaa66;
      font-size: 0.9rem;
      margin-top: 0.5rem;
    }
    #history {
      background-color: #1a1a1a;
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
      border: 2px solid #ff851a;
    }
    .modal-content h2 {
      font-size: 1.5rem;
      margin-bottom: 1rem;
      color: #ff851a;
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
      background-color: #ffaa66;
      color: #000000;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    .modal-content button:hover {
      background-color: #ff851a;
    }
    .close-modal {
      position: absolute;
      top: 1rem;
      right: 1rem;
      font-size: 1.5rem;
      cursor: pointer;
      color: #ff851a;
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
      color: #ffaa66;
      text-decoration: none;
    }
    .contact-info a:hover {
      text-decoration: underline;
    }
    html {
      scroll-behavior: smooth;
    }
    @media (max-width: 768px) {
      .header-left {
        flex-direction: column;
        gap: 1rem;
      }
      nav ul {
        flex-direction: column;
        gap: 0.5rem;
      }
      .header-content {
        flex-direction: column;
        gap: 1rem;
      }
      .product-grid {
        grid-template-columns: 1fr;
      }
      #home h2 {
        font-size: 1.8rem;
      }
      #home p {
        font-size: 1rem;
      }
    }
  </style>
</head>
<body>
  <header>
    <div class="container header-content">
      <div class="header-left">
        <img src="logo.png" alt="GhostWorker Logo" class="logo">
        <nav>
          <ul>
            <li><a href="#home" class="nav-link active" data-en="Home" data-es="Inicio">Inicio</a></li>
            <li><a href="#products" class="nav-link" data-en="Products" data-es="Productos">Productos</a></li>
            <li><a href="#history" class="nav-link" data-en="Our History" data-es="Nuestra Historia">Nuestra Historia</a></li>
          </ul>
        </nav>
      </div>
      <div style="display: flex; gap: 1rem; align-items: center;">
        <button class="language-toggle" id="lang-toggle" data-lang="en">🇺🇸 English</button>
        <button class="cart-button">
          <span data-en="Cart" data-es="Carrito">Carrito</span> <span class="cart-count">0</span>
        </button>
      </div>
    </div>
  </header>
  <main>
    <section id="home">
      <div class="container">
        <h2 data-en="Welcome to GhostWorker" data-es="Bienvenido a GhostWorker">Bienvenido a GhostWorker</h2>
        <p data-en="In GhostWorker, discover tailored process and data solutions designed to streamline your daily tasks, boost efficiency, and deliver measurable results—so you can focus on what truly matters." 
           data-es="En GhostWorker, descubre soluciones personalizadas de procesos y datos diseñadas para optimizar tus tareas diarias, aumentar la eficiencia y entregar resultados medibles, para que puedas enfocarte en lo que realmente importa.">En GhostWorker, descubre soluciones personalizadas de procesos y datos diseñadas para optimizar tus tareas diarias, aumentar la eficiencia y entregar resultados medibles, para que puedas enfocarte en lo que realmente importa.</p>
      </div>
    </section>
    <section id="products">
      <div class="container">
        <h2 data-en="Our Products" data-es="Nuestros Productos">Nuestros Productos</h2>
        <div class="product-grid">
          <div class="product-card" data-handle="data-analytics">
            <img src="https://cdn.shopify.com/s/files/1/0956/8065/9751/files/data_analisis.jpg?v=1761168765" alt="Data Analytics">
            <div class="product-card-content">
              <h2 data-en="Data Analytics" data-es="Análisis de Datos">Análisis de Datos</h2>
              <p class="description" data-en="Converts complex datasets into actionable insights using statistical analysis, visualization, and predictive modeling. Enables informed decision-making by identifying trends, inefficiencies, and strategic opportunities within business operations." 
                 data-es="Convierte conjuntos de datos complejos en información accionable mediante análisis estadístico, visualización y modelado predictivo. Permite la toma de decisiones informadas identificando tendencias, ineficiencias y oportunidades estratégicas en las operaciones empresariales.">Convierte conjuntos de datos complejos en información accionable mediante análisis estadístico, visualización y modelado predictivo. Permite la toma de decisiones informadas identificando tendencias, ineficiencias y oportunidades estratégicas en las operaciones empresariales.</p>
              <p class="price">$1500.00</p>
              <ul>
                <li data-en="technical support" data-es="soporte técnico">soporte técnico</li>
                <li data-en="customizable interface" data-es="interfaz personalizable">interfaz personalizable</li>
                <li data-en="real time updates" data-es="actualizaciones en tiempo real">actualizaciones en tiempo real</li>
                <li data-en="data import export" data-es="importación/exportación de datos">importación/exportación de datos</li>
                <li data-en="cloud based" data-es="basado en la nube">basado en la nube</li>
                <li data-en="built in templates" data-es="plantillas integradas">plantillas integradas</li>
              </ul>
              <p class="info">OS: windows, macos</p>
              <p class="info">For: individual, large enterprise, small business, medium sized business enterprise</p>
              <p class="info stock">Stock: 2</p>
              <button data-price="1500.00" data-en="Add to Cart" data-es="Agregar al Carrito">Agregar al Carrito</button>
              <p class="cart-message"></p>
            </div>
          </div>
          <div class="product-card" data-handle="etl-pipelines">
            <img src="https://cdn.shopify.com/s/files/1/0956/8065/9751/files/ETLPIPELINE.png?v=1761168863" alt="ETL Pipelines">
            <div class="product-card-content">
              <h2 data-en="ETL Pipelines" data-es="Tuberías ETL">Tuberías ETL</h2>
              <p class="description" data-en="Builds and manages ETL (Extract, Transform, Load) pipelines for seamless data integration across multiple sources. Focuses on reliability, data quality, and performance to ensure accurate and efficient data processing for downstream analytics and automation initiatives." 
                 data-es="Construye y gestiona tuberías ETL (Extract, Transform, Load) para una integración de datos sin problemas desde múltiples fuentes. Se enfoca en confiabilidad, calidad de datos y rendimiento para garantizar un procesamiento de datos preciso y eficiente para análisis y automatización posteriores.">Construye y gestiona tuberías ETL (Extract, Transform, Load) para una integración de datos sin problemas desde múltiples fuentes. Se enfoca en confiabilidad, calidad de datos y rendimiento para garantizar un procesamiento de datos preciso y eficiente para análisis y automatización posteriores.</p>
              <p class="price">$2000.00</p>
              <ul>
                <li data-en="cloud based" data-es="basado en la nube">basado en la nube</li>
                <li data-en="data import export" data-es="importación/exportación de datos">importación/exportación de datos</li>
                <li data-en="automatic updates" data-es="actualizaciones automáticas">actualizaciones automáticas</li>
                <li data-en="technical support" data-es="soporte técnico">soporte técnico</li>
              </ul>
              <p class="info">For: large enterprise, medium sized business enterprise, small business</p>
              <p class="info stock">Stock: 2</p>
              <button data-price="2000.00" data-en="Add to Cart" data-es="Agregar al Carrito">Agregar al Carrito</button>
              <p class="cart-message"></p>
            </div>
          </div>
          <div class="product-card" data-handle="process-automation">
            <img src="https://cdn.shopify.com/s/files/1/0956/8065/9751/files/ProcessAutomation.jpg?v=1761168696" alt="Process Automation">
            <div class="product-card-content">
              <h2 data-en="Process Automation" data-es="Automatización de Procesos">Automatización de Procesos</h2>
              <p class="description" data-en="Implements end-to-end automation solutions to streamline operations and reduce manual effort. Focuses on achieving measurable productivity improvements through smart integration of technology and process engineering principles." 
                 data-es="Implementa soluciones de automatización de extremo a extremo para optimizar operaciones y reducir el esfuerzo manual. Se enfoca en lograr mejoras medibles de productividad mediante la integración inteligente de tecnología y principios de ingeniería de procesos.">Implementa soluciones de automatización de extremo a extremo para optimizar operaciones y reducir el esfuerzo manual. Se enfoca en lograr mejoras medibles de productividad mediante la integración inteligente de tecnología y principios de ingeniería de procesos.</p>
              <p class="price">$3500.00</p>
              <p class="info">For: medium sized business enterprise, large enterprise, small business</p>
              <p class="info stock">Stock: 2</p>
              <button data-price="3500.00" data-en="Add to Cart" data-es="Agregar al Carrito">Agregar al Carrito</button>
              <p class="cart-message"></p>
            </div>
          </div>
          <div class="product-card" data-handle="process-consulting">
            <img src="https://cdn.shopify.com/s/files/1/0956/8065/9751/files/ProcessConsultingimg.jpg?v=1761168362" alt="Process Consulting">
            <div class="product-card-content">
              <h2 data-en="Process Consulting" data-es="Consultoría de Procesos">Consultoría de Procesos</h2>
              <p class="description" data-en="Provides strategic guidance to help businesses optimize workflows, eliminate inefficiencies, and improve overall performance. Combines industrial engineering methods with data-driven insights to design lean, scalable, and sustainable processes." 
                 data-es="Proporciona orientación estratégica para ayudar a las empresas a optimizar flujos de trabajo, eliminar ineficiencias y mejorar el rendimiento general. Combina métodos de ingeniería industrial con información basada en datos para diseñar procesos magros, escalables y sostenibles.">Proporciona orientación estratégica para ayudar a las empresas a optimizar flujos de trabajo, eliminar ineficiencias y mejorar el rendimiento general. Combina métodos de ingeniería industrial con información basada en datos para diseñar procesos magros, escalables y sostenibles.</p>
              <p class="price">$2500.00</p>
              <p class="info">For: medium sized business enterprise, large enterprise, small business</p>
              <p class="info stock">Stock: 10</p>
              <button data-price="2500.00" data-en="Add to Cart" data-es="Agregar al Carrito">Agregar al Carrito</button>
              <p class="cart-message"></p>
            </div>
          </div>
          <div class="product-card" data-handle="robotic-process-automation">
            <img src="https://cdn.shopify.com/s/files/1/0956/8065/9751/files/RPA_image.jpg?v=1761168820" alt="Robotic Process Automation">
            <div class="product-card-content">
              <h2 data-en="Robotic Process Automation" data-es="Automatización Robótica de Procesos">Automatización Robótica de Procesos</h2>
              <p class="description" data-en="Designs and deploys robotic automation solutions to handle repetitive digital tasks efficiently. Ensures consistency, accuracy, and speed while freeing human resources for higher-value analysis and decision-making." 
                 data-es="Diseña e implementa soluciones de automatización robótica para manejar tareas digitales repetitivas de manera eficiente. Garantiza consistencia, precisión y velocidad mientras libera recursos humanos para análisis y toma de decisiones de mayor valor.">Diseña e implementa soluciones de automatización robótica para manejar tareas digitales repetitivas de manera eficiente. Garantiza consistencia, precisión y velocidad mientras libera recursos humanos para análisis y toma de decisiones de mayor valor.</p>
              <p class="price">$1500.00</p>
              <ul>
                <li data-en="technical support" data-es="soporte técnico">soporte técnico</li>
                <li data-en="customizable interface" data-es="interfaz personalizable">interfaz personalizable</li>
                <li data-en="cloud based" data-es="basado en la nube">basado en la nube</li>
                <li data-en="automatic updates" data-es="actualizaciones automáticas">actualizaciones automáticas</li>
                <li data-en="data import export" data-es="importación/exportación de datos">importación/exportación de datos</li>
              </ul>
              <p class="info">For: small business, large enterprise, medium sized business enterprise</p>
              <p class="info stock">Stock: Out of Stock</p>
              <button data-price="1500.00" disabled data-en="Add to Cart" data-es="Agregar al Carrito">Agregar al Carrito</button>
              <p class="cart-message"></p>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section id="history">
      <div class="container">
        <h2 data-en="Our History" data-es="Nuestra Historia">Nuestra Historia</h2>
        <p data-en="Our journey began with a vision to bridge the worlds of engineering, automation, and data. Founded by Julio Félix, an industrial and data engineer with years of practical experience leading innovative projects, our company was built on a belief that efficiency and technology are the twin engines of modern business transformation." 
           data-es="Nuestro viaje comenzó con una visión de unir los mundos de la ingeniería, la automatización y los datos. Fundada por Julio Félix, ingeniero industrial y de datos con años de experiencia práctica liderando proyectos innovadores, nuestra empresa se construyó bajo la creencia de que la eficiencia y la tecnología son los motores gemelos de la transformación empresarial moderna.">Nuestro viaje comenzó con una visión de unir los mundos de la ingeniería, la automatización y los datos. Fundada por Julio Félix, ingeniero industrial y de datos con años de experiencia práctica liderando proyectos innovadores, nuestra empresa se construyó bajo la creencia de que la eficiencia y la tecnología son los motores gemelos de la transformación empresarial moderna.</p>
        <p data-en="From optimizing industrial processes to developing automated digital ecosystems, we have grown through a passion for solving complex challenges with simple, effective solutions. Every project—from designing ETL pipelines and process automation systems to implementing analytics and RPA solutions—reflects our commitment to precision, innovation, and measurable results." 
           data-es="Desde la optimización de procesos industriales hasta el desarrollo de ecosistemas digitales automatizados, hemos crecido a través de una pasión por resolver desafíos complejos con soluciones simples y efectivas. Cada proyecto—desde el diseño de tuberías ETL y sistemas de automatización de procesos hasta la implementación de soluciones de análisis y RPA—refleja nuestro compromiso con la precisión, la innovación y resultados medibles.">Desde la optimización de procesos industriales hasta el desarrollo de ecosistemas digitales automatizados, hemos crecido a través de una pasión por resolver desafíos complejos con soluciones simples y efectivas. Cada proyecto—desde el diseño de tuberías ETL y sistemas de automatización de procesos hasta la implementación de soluciones de análisis y RPA—refleja nuestro compromiso con la precisión, la innovación y resultados medibles.</p>
        <p data-en="Today, we partner with organizations that want to move forward—integrating smart technology, automation, and strategic insight to achieve excellence. Our history is defined not just by what we've built, but by how we've empowered others to innovate, optimize, and thrive." 
           data-es="Hoy, nos asociamos con organizaciones que quieren avanzar—integrando tecnología inteligente, automatización e información estratégica para alcanzar la excelencia. Nuestra historia no se define solo por lo que hemos construido, sino por cómo hemos empoderado a otros para innovar, optimizar y prosperar.">Hoy, nos asociamos con organizaciones que quieren avanzar—integrando tecnología inteligente, automatización e información estratégica para alcanzar la excelencia. Nuestra historia no se define solo por lo que hemos construido, sino por cómo hemos empoderado a otros para innovar, optimizar y prosperar.</p>
      </div>
    </section>
  </main>
  <div class="modal" id="cart-modal">
    <div class="modal-content">
      <span class="close-modal">&times;</span>
      <h2 data-en="Shopping Cart" data-es="Carrito de Compras">Carrito de Compras</h2>
      <ul id="cart-items"></ul>
      <p id="cart-total" data-en="Total: $0.00" data-es="Total: $0.00">Total: $0.00</p>
      <button id="clear-cart" data-en="Clear Cart" data-es="Vaciar Carrito">Vaciar Carrito</button>
    </div>
  </div>
  <footer>
    <div class="container">
      <p data-en="© 2025 GhostWorker. All rights reserved." data-es="© 2025 GhostWorker. Todos los derechos reservados.">© 2025 GhostWorker. Todos los derechos reservados.</p>
      <div class="contact-info">
        <p data-en="Instagram:" data-es="Instagram:">Instagram: <a href="https://www.instagram.com/GhostWorker" target="_blank">@GhostWorker</a></p>
        <p data-en="Email:" data-es="Correo:">Correo: <a href="mailto:ghost_worker@outlook.com">ghost_worker@outlook.com</a></p>
        <p data-en="Phone:" data-es="Teléfono:">Teléfono: <a href="tel:+18296473440">+1 829 647 3440</a></p>
      </div>
    </div>
  </footer>

  <script>
    let cart = [];
    let currentLang = 'es'; // Spanish default

    const translations = {
      en: {
        langToggle: '🇺🇸 English',
        cart: 'Cart'
      },
      es: {
        langToggle: '🇺🇸 English',
        cart: 'Carrito'
      }
    };

    function setLanguage(lang) {
      currentLang = lang;
      document.documentElement.lang = lang;
      document.title = lang === 'es' ? 
        'GhostWorker - Soluciones de Datos Personalizadas' : 
        'GhostWorker - Software & Consulting Services';

      // Update all translatable elements
      document.querySelectorAll('[data-en]').forEach(el => {
        const text = el.getAttribute(`data-${lang}`);
        if (text) {
          if (el.tagName === 'BUTTON' || el.tagName === 'LI') {
            el.textContent = text;
          } else {
            el.innerHTML = text;
          }
        }
      });

      // Update language toggle button
      const langToggle = document.getElementById('lang-toggle');
      langToggle.textContent = translations[lang].langToggle;
      langToggle.setAttribute('data-lang', lang === 'es' ? 'en' : 'es');

      // Update cart button
      const cartBtnText = document.querySelector('.cart-button span');
      cartBtnText.textContent = translations[lang].cart;

      // Store preference
      localStorage.setItem('ghostworker-lang', lang);
    }

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

    // Initialize language
    function initLanguage() {
      const savedLang = localStorage.getItem('ghostworker-lang');
      const browserLang = navigator.language.startsWith('es') ? 'es' : 'en';
      
      // Default to Spanish, then saved preference, then browser language
      const initialLang = savedLang || (browserLang === 'es' ? 'es' : 'es');
      setLanguage(initialLang);
    }

    // Event listeners
    document.getElementById('lang-toggle').addEventListener('click', () => {
      const nextLang = currentLang === 'es' ? 'en' : 'es';
      setLanguage(nextLang);
    });

    document.querySelectorAll('.product-card button:not([disabled])').forEach(button => {
      button.addEventListener('click', () => {
        const card = button.closest('.product-card');
        const title = card.querySelector('h2').textContent;
        const price = parseFloat(button.getAttribute('data-price'));
        const stockElement = card.querySelector('.info.stock');
        const stockText = stockElement ? stockElement.textContent : '';
        const messageElement = card.querySelector('.cart-message');

        if (stockText.includes('Out of Stock')) {
          messageElement.textContent = currentLang === 'es' ? 
            `${title} no tiene stock.` : `${title} is out of stock.`;
        } else {
          const existingItem = cart.find(item => item.title === title);
          if (existingItem) {
            messageElement.textContent = currentLang === 'es' ? 
              `${title} ya está en el carrito.` : `${title} is already in the cart.`;
          } else {
            cart.push({ title, price, quantity: 1 });
            updateCartDisplay();
            messageElement.textContent = currentLang === 'es' ? 
              `${title} agregado al carrito!` : `${title} added to cart!`;
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
    const clearCartBtn = document.getElementById('clear-cart');

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

    clearCartBtn.addEventListener('click', () => {
      cart = [];
      updateCartDisplay();
    });

    // Initialize
    initLanguage();
  </script>
</body>
</html>
