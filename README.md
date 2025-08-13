# Kelompok-1
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Otomotif Kelompok 1</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
    }
    body {
      background: #f0f0f0;
      padding: 20px;
    }
    header {
      background-color: #1f2937;
      color: white;
      padding: 20px;
      text-align: center;
    }
    nav {
      display: flex;
      justify-content: center;
      gap: 20px;
      background: #374151;
      padding: 10px;
      flex-wrap: wrap;
    }
    nav button {
      background: #4b5563;
      color: white;
      border: none;
      padding: 10px 15px;
      cursor: pointer;
      border-radius: 5px;
    }
    nav button:hover {
      background-color: #6b7280;
    }
    .content > div {
      margin-top: 20px;
    }
    .hidden {
      display: none;
    }
    #searchBox {
      padding: 10px;
      width: 100%;
      margin-bottom: 20px;
      font-size: 16px;
    }
    .car-list {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      gap: 20px;
    }
    .car-card {
      background: white;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      padding: 15px;
      text-align: center;
      position: relative;
      transition: transform 0.2s;
    }
    .car-card:hover {
      transform: scale(1.02);
    }
    .car-card img {
      width: 100%;
      height: 150px;
      object-fit: cover;
      border-radius: 8px;
      margin-bottom: 10px;
    }
    .car-card h3 {
      margin-bottom: 10px;
      color: #1f2937;
    }
    .car-card button {
      margin-top: 10px;
      padding: 8px 12px;
      background-color: #2563eb;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .car-card button:hover {
      background-color: #1d4ed8;
    }
    .detail-box {
      background: #ffffff;
      padding: 15px;
      margin-top: 15px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      text-align: left;
      font-size: 14px;
      animation: fadeIn 0.3s ease-in-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @media (max-width: 600px) {
      nav {
        flex-direction: column;
      }
    }
  </style>
</head>
<body>

<header>
  <h1>WEB SITE KELOMPOK 1</h1>
  <p>Info lengkap mobil terbaru dan mobil second</p>
</header>

<nav>
  <button onclick="showPage('home')">Beranda</button>
  <button onclick="showPage('cars')">Daftar Mobil</button>
  <button onclick="showPage('usedCars')">Mobil Second</button>
  <button onclick="showPage('about')">Tentang</button>
</nav>

<div class="content">
  <div id="home">
    <h2>Selamat Datang di web kelompok 1</h2>
    <p>Kami menyajikan informasi terbaru seputar dunia otomotif, mobil terbaru, ulasan, dan harga terkini di pasar Indonesia.</p>
  </div>

  <div id="cars" class="hidden">
    <h2>Daftar Mobil Populer</h2>
    <input type="text" id="searchBox" placeholder="Cari mobil..." oninput="searchCars()" />
    <div class="car-list" id="carList"></div>
  </div>

  <div id="usedCars" class="hidden">
    <h2>Daftar Mobil Second</h2>
    <div class="car-list" id="usedCarList"></div>
  </div>

  <div id="about" class="hidden">
    <h2>Tentang Kami</h2>
    <p>Kami dari kelompok 1 yang menyajikan berita, review, dan informasi harga mobil dari berbagai merek seperti Toyota, Honda, Suzuki, Hyundai, dan lainnya. Website ini dibuat untuk membantu masyarakat mendapatkan informasi sebelum membeli kendaraan.</p>
  </div>
</div>

<script>
const carsData = [
  {
    name: "Toyota Avanza",
    brand: "Toyota",
    price: "Rp 250.000.000",
    engine: "1.5L Dual VVT-i",
    transmission: "Manual / CVT",
    fuel: "Bensin",
    seats: 7,
    image: "https://img.cintamobil.com/2021/11/10/tYG8w8tv/foto-10-1-0eb7.jpg"
  },
  {
    name: "Honda Brio",
    brand: "Honda",
    price: "Rp 180.000.000",
    engine: "1.2L i-VTEC",
    transmission: "Manual / CVT",
    fuel: "Bensin",
    seats: 5,
    image: "https://mobil-pedia.com/images/mobil/202404/honda-brio-84507.webp"
  },
  {
    name: "Suzuki XL7",
    brand: "Suzuki",
    price: "Rp 260.000.000",
    engine: "1.5L K15B",
    transmission: "Manual / Otomatis",
    fuel: "Bensin",
    seats: 7,
    image: "https://okinews.bacakoran.co/upload/731b695aa8d131f6e800e56a54c1ee06.jpg"
  },
  {
    name: "Hyundai Stargazer",
    brand: "Hyundai",
    price: "Rp 270.000.000",
    engine: "1.5L Smartstream",
    transmission: "IVT (CVT)",
    fuel: "Bensin",
    seats: 7,
    image: "https://hyundaibandungofficial.id/wp-content/uploads/2022/01/Hyundai-31.png"
  },
  {
    name: "Daihatsu Terios",
    brand: "Daihatsu",
    price: "Rp 270.000.000",
    engine: "1.5L Dual VVT-i",
    transmission: "Manual / Otomatis",
    fuel: "Bensin",
    seats: 7,
    image: "https://imgcdn.oto.com/large/gallery/color/7/1669/daihatsu-terios-color-920316.jpg"
  }
];

const usedCarsData = [
  {
    name: "Toyota Kijang Innova (2015)",
    brand: "Toyota",
    price: "Rp 160.000.000",
    engine: "2.0L VVT-i",
    transmission: "Manual",
    fuel: "Bensin",
    seats: 7,
    image: "https://sumateraekspres.bacakoran.co/upload/9af3ab3717cc4f826ff681001a1dac08.jpg"
  },
  {
    name: "Honda Jazz (2014)",
    brand: "Honda",
    price: "Rp 145.000.000",
    engine: "1.5L i-VTEC",
    transmission: "Automatic",
    fuel: "Bensin",
    seats: 5,
    image: "https://imgx.gridoto.com/crop/0x0:0x0/700x465/photo/2020/08/13/727184072.jpg"
  },
  {
    name: "Suzuki Ertiga GL (2016)",
    brand: "Suzuki",
    price: "Rp 120.000.000",
    engine: "1.4L VVT",
    transmission: "Manual",
    fuel: "Bensin",
    seats: 7,
    image: "https://img.hargamobil.com/2018/02/24/hwswm0Bu/post8771-6159.jpg"
  }
];

function showPage(pageId) {
  const pages = document.querySelectorAll('.content > div');
  pages.forEach(page => page.classList.add('hidden'));
  document.getElementById(pageId).classList.remove('hidden');

  if (pageId === 'cars') renderCars();
  if (pageId === 'usedCars') renderUsedCars();
}

function renderCars(filteredCars = carsData) {
  const carList = document.getElementById('carList');
  carList.innerHTML = '';
  filteredCars.forEach(car => {
    const card = document.createElement('div');
    card.className = 'car-card';
    card.innerHTML = `
      <img src="${car.image}" alt="${car.name}" />
      <h3>${car.name}</h3>
      <p><strong>Harga:</strong> ${car.price}</p>
      <button onclick="toggleDetail(this)">Lihat Detail</button>
      <div class="detail-box hidden">
        <p><strong>Merk:</strong> ${car.brand}</p>
        <p><strong>Mesin:</strong> ${car.engine}</p>
        <p><strong>Transmisi:</strong> ${car.transmission}</p>
        <p><strong>Bahan Bakar:</strong> ${car.fuel}</p>
        <p><strong>Kapasitas Penumpang:</strong> ${car.seats} orang</p>
      </div>
    `;
    carList.appendChild(card);
  });
}

function renderUsedCars() {
  const usedCarList = document.getElementById('usedCarList');
  usedCarList.innerHTML = '';
  usedCarsData.forEach(car => {
    const card = document.createElement('div');
    card.className = 'car-card';
    card.innerHTML = `
      <img src="${car.image}" alt="${car.name}" />
      <h3>${car.name}</h3>
      <p><strong>Harga:</strong> ${car.price}</p>
      <button onclick="toggleDetail(this)">Lihat Detail</button>
      <div class="detail-box hidden">
        <p><strong>Merk:</strong> ${car.brand}</p>
        <p><strong>Mesin:</strong> ${car.engine}</p>
        <p><strong>Transmisi:</strong> ${car.transmission}</p>
        <p><strong>Bahan Bakar:</strong> ${car.fuel}</p>
        <p><strong>Kapasitas Penumpang:</strong> ${car.seats} orang</p>
      </div>
    `;
    usedCarList.appendChild(card);
  });
}

function toggleDetail(button) {
  const detailBox = button.nextElementSibling;
  detailBox.classList.toggle('hidden');
  button.textContent = detailBox.classList.contains('hidden') ? 'Lihat Detail' : 'Sembunyikan Detail';
}

function searchCars() {
  const keyword = document.getElementById('searchBox').value.toLowerCase();
  const filtered = carsData.filter(car =>
    car.name.toLowerCase().includes(keyword) ||
    car.brand.toLowerCase().includes(keyword)
  );
  renderCars(filtered);
}

showPage('home');
</script>

</body>
</html>
