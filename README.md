<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Vapers Shop</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      margin: 0;
      padding: 0;
      background: #fff;
      color: #111;
    }
    header {
      background: #111;
      color: #fff;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
    }
    nav a {
      color: #fff;
      margin-left: 1rem;
      text-decoration: none;
      font-weight: 500;
    }
    #carrusel {
      width: 100%;
      overflow: hidden;
      max-height: 300px;
      margin-bottom: 1rem;
    }
    .slider {
      display: flex;
      animation: slide 12s infinite;
      width: 300%;
    }
    .slider img {
      width: 100%;
      height: 300px;
      object-fit: cover;
    }
    @keyframes slide {
      0%, 33% { transform: translateX(0%); }
      34%, 66% { transform: translateX(-100%); }
      67%, 100% { transform: translateX(-200%); }
    }
    #filtros {
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 1rem;
      border-bottom: 1px solid #ddd;
      background: #f9f9f9;
    }
    select#ordenar {
      padding: 0.5rem 1rem;
      font-size: 1rem;
    }
    .categorias button {
      margin: 0.2rem;
      padding: 0.5rem 1rem;
      background: #444;
      color: #fff;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      transition: background 0.3s ease;
    }
    .categorias button:hover {
      background: #666;
    }
    #productos {
      display: flex;
      flex-wrap: wrap;
      padding: 2rem;
      gap: 1rem;
      justify-content: center;
      background: #fff;
    }
    .producto {
      border: 1px solid #ccc;
      padding: 1rem;
      width: 220px;
      text-align: center;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgb(0 0 0 / 0.1);
      transition: transform 0.2s ease;
      background: #fafafa;
    }
    .producto:hover {
      transform: translateY(-5px);
      box-shadow: 0 4px 12px rgb(0 0 0 / 0.15);
    }
    .producto h3 {
      margin: 0.5rem 0;
      font-size: 1.1rem;
    }
    .producto p {
      margin: 0.25rem 0;
      font-size: 0.9rem;
      color: #555;
    }
    #ruleta {
      background: #111;
      color: #fff;
      text-align: center;
      padding: 2rem 1rem;
    }
    #ruleta h2 {
      margin-bottom: 1rem;
      font-weight: 400;
    }
    #ruleta button {
      padding: 0.8rem 1.5rem;
      font-size: 1rem;
      background: #e63946;
      color: #fff;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      transition: background 0.3s ease;
    }
    #ruleta button:hover {
      background: #d62828;
    }
    #resultado-ruleta {
      margin-top: 1rem;
      font-size: 1.3rem;
      font-weight: 600;
      min-height: 1.5em;
    }
    #envio {
      text-align: center;
      padding: 1rem 0;
      font-size: 1.1rem;
      background: #f0f0f0;
      color: #111;
    }
    footer#contacto {
      background: #f4f4f4;
      padding: 2rem 1rem;
      text-align: center;
      font-size: 1rem;
      color: #333;
    }
    footer#contacto h3 {
      margin-bottom: 1rem;
      font-weight: 500;
    }
    footer#contacto p {
      margin: 0.3rem 0;
    }
    .redes a {
      margin: 0 1rem;
      color: #111;
      text-decoration: none;
      font-weight: 600;
      transition: color 0.3s ease;
    }
    .redes a:hover {
      color: #e63946;
    }
    /* Responsive */
    @media (max-width: 600px) {
      header {
        flex-direction: column;
        align-items: flex-start;
      }
      nav {
        margin-top: 0.5rem;
      }
      #filtros {
        flex-direction: column;
        align-items: flex-start;
      }
      .categorias {
        width: 100%;
      }
      #productos {
        justify-content: center;
      }
    }
  </style>
</head>
<body>

  <header>
    <h1>Vapers Shop</h1>
    <nav>
      <a href="#productos">Productos</a>
      <a href="#ruleta">Descuentos</a>
      <a href="#contacto">Contacto</a>
    </nav>
  </header>

  <!-- Carrusel -->
  <section id="carrusel">
    <div class="slider">
      <img src="https://images.unsplash.com/photo-1590080877777-5a1e7bfa8cc1?auto=format&fit=crop&w=800&q=80" alt="Vaper 1" />
      <img src="https://images.unsplash.com/photo-1612935911747-952a4c0cd42f?auto=format&fit=crop&w=800&q=80" alt="Vaper 2" />
      <img src="https://images.unsplash.com/photo-1618037345972-801d12a1bf0b?auto=format&fit=crop&w=800&q=80" alt="Vaper 3" />
    </div>
  </section>

  <!-- Filtros -->
  <section id="filtros">
    <select id="ordenar" aria-label="Ordenar productos">
      <option value="">Ordenar por</option>
      <option value="alto">Precio más alto</option>
      <option value="bajo">Precio más bajo</option>
      <option value="vendido">Más vendido</option>
    </select>

    <div class="categorias" role="group" aria-label="Filtrar por marca">
      <button onclick="filtrar('elfbar')">Elfbar</button>
      <button onclick="filtrar('ignite')">Ignite</button>
      <button onclick="filtrar('lost-angel')">Lost Angel</button>
      <button onclick="filtrar('vozol')">Vozol</button>
      <button onclick="mostrarProductos(productos)">Mostrar todos</button>
    </div>
  </section>

  <!-- Productos -->
  <section id="productos" aria-live="polite" aria-label="Listado de productos">
    <!-- Productos se cargan aquí -->
  </section>

  <!-- Ruleta de descuento -->
  <section id="ruleta" aria-label="Ruleta de descuentos">
    <h2>¡Gira la ruleta y gana un descuento!</h2>
    <button onclick="girarRuleta()" aria-live="polite">Girar</button>
    <div id="resultado-ruleta" role="alert" aria-live="assertive"></div>
  </section>

  <!-- Envío gratis -->
  <section id="envio">
    <p>🛒 Envío gratis a partir de <strong>$100.000</strong></p>
  </section>

  <!-- Contacto y redes -->
  <footer id="contacto">
    <h3>Contacto</h3>
    <p>Email: contacto@vapershop.com</p>
    <p>WhatsApp: +56912345678</p>
    <div class="redes">
      <a href="https://instagram.com/tuemprendimiento" target="_blank" rel="noopener noreferrer">Instagram</a>
      <a href="https://facebook.com/tuemprendimiento" target="_blank" rel="noopener noreferrer">Facebook</a>
    </div>
  </footer>

  <script>
    const productos = [
      { nombre: 'Elfbar 5000', marca: 'elfbar', puff: 5000, precio: 25000, vendidos: 200 },
      { nombre: 'Ignite V20', marca: 'ignite', puff: 4000, precio: 28000, vendidos: 300 },
      { nombre: 'Lost Angel Max', marca: 'lost-angel', puff: 6000, precio: 30000, vendidos: 100 },
      { nombre: 'Vozol Star', marca: 'vozol', puff: 5500, precio: 27000, vendidos: 250 },
    ];

    function mostrarProductos(lista) {
      const contenedor = document.getElementById('productos');
      contenedor.innerHTML = '';
      if (lista.length === 0) {
        contenedor.innerHTML = '<p>No hay productos para mostrar.</p>';
        return;
      }
      lista.forEach(p => {
        contenedor.innerHTML += `
          <div class="producto">
            <h3>${p.nombre}</h3>
            <p><strong>Marca:</strong> ${p.marca.charAt(0).toUpperCase() + p.marca.slice(1).replace('-', ' ')}</p>
            <p><strong>Puffs:</strong> ${p.puff.toLocaleString()}</p>
            <p><strong>Precio:</strong> $${p.precio.toLocaleString()}</p>
          </div>
        `;
      });
    }

    mostrarProductos(productos);

    document.getElementById('ordenar').addEventListener('change', (e) => {
      let orden = e.target.value;
      let copia = [...productos];

      if (orden === 'alto') {
        copia.sort((a, b) => b.precio - a.precio);
      } else if (orden === 'bajo') {
        copia.sort((a, b) => a.precio - b.precio);
      } else if (orden === 'vendido') {
        copia.sort((a, b) => b.vendidos - a.vendidos);
      }

      mostrarProductos(copia);
    });

    function filtrar(marca) {
      const filtrados = productos.filter(p => p.marca === marca);
      mostrarProductos(filtrados);
    }

    function girarRuleta() {
      const descuentos = [10, 20, 30, 50, 0];
      const resultado = descuentos[Math.floor(Math.random() * descuentos.length)];
      const resultadoDiv = document.getElementById('resultado-ruleta');
      if (resultado === 0) {
        resultadoDiv.textContent = '¡Sigue intentando! No ganaste descuento esta vez.';
      } else {
        resultadoDiv.textContent = `¡Felicidades! Ganaste un ${resultado}% de descuento 🎉`;
      }
    }
  </script>
</body>
</html>

