<?php
// Data venue
$venue = [
    'name' => 'Orion Sport Center Purwokerto',
    'rating' => 4.6,
    'location' => 'Purwokerto, Jawa Tengah',
    'price' => 975000,
    'description' => 'HARGA DIBERITAHUKAN DAHULU!!!',
    'facilities' => [
        'Musholla',
        'Parkir Mobil',
        'Parkir Motor',
        'Ruang Ganti',
        'Shower',
        'Toilet',
        'Tribun Penonton',
        'Wi-fi',
        'Jual Makanan Ringan',
        'Jual Minuman',
    ],
    'rules' => [
        'Booking Lapangan Hanya Melalui Web Bal-Balan yuk',
        'Proses Booking semua melalui Web Bal-Balan yuk. Lapangan tidak terima titipan booking',
        'Pelaksana Lapangan akan infokan jika Kondisi Hujan dan akan reschedule bookingan',
        'Pelaksana Lapangan Hanya Mengatur Jam Booking',
        'Stadion Akan ditutup selama bermain',
        'Pintu Stadion akan dibuka 25 Menit Team Kedua akan bermain',
        'Jika terjadi hujan sebelum bermain maka lapangan tidak bisa di pakai dan bookingan team akan di reschdule',
        'Jika team sedang bermain dan hujan tetap di lanjutkan bermain dan team selanjutkan akan di reschdule',
        'Pemain, Official dan penonton DILARANG MEROKOK DI AREA STADION',
        'DILARANG MEMBAWA MAKANAN ATAU MINUMAN DARI LUAR',
        'Seluruh Barang Pribadi dan Team jika Hilang Tanggung Jawab Sendiri',
        'Kami menyediakan Fasilitas Toilet, Ruang Ganti Pemain, Musholla, Tempat Cuci Sepatu dan Area Parkir yg nyaman',
        'JIKA 3 JAM SEBELUM MAIN HUJAN MAKA JADWAL AKAN DI CANCEL DAN TEAM BISA MENGAJUKAN RESCHDULE ATAU REFUND',
    ],
    'refund_policy' => [
        'Reschedule hingga 1 hari sebelum jadwal sewa. Hanya berlaku untuk 1 kali reschedule.',
        'Reservasi tidak dapat dibatalkan dan tidak berlaku refund.',
        'Tidak ada refund',
    ],
    'latitude' => -6.2088,
    'longitude' => 106.8456,
    'map_link' => 'https://maps.app.goo.gl/PRcPy88MQGYG8JqaA',
    'image' => 'https://example.com/path/to/venue/image.jpg',
];

// Fungsi untuk mendapatkan URL gambar peta statis
function getStaticMapUrl($latitude, $longitude, $apiKey) {
    $baseUrl = "https://maps.googleapis.com/maps/api/staticmap";
    $center = "{$latitude},{$longitude}";
    $zoom = 15;
    $size = "600x300";
    $mapType = "roadmap";
    $markers = "color:red|{$center}";

    return "{$baseUrl}?center={$center}&zoom={$zoom}&size={$size}&maptype={$mapType}&markers={$markers}&key={$apiKey}";
}

// Fungsi untuk menampilkan fasilitas
function displayFacilities($facilities) {
    echo '<ul class="facilities-list">';
    foreach ($facilities as $facility) {
        echo "<li>$facility</li>";
    }
    echo '</ul>';
}

// Fungsi untuk memformat harga
function formatPrice($price) {
    return 'Rp ' . number_format($price, 0, ',', '.');
}

// Fungsi untuk menampilkan rating bintang
function displayStarRating($rating) {
    $fullStars = floor($rating);
    $halfStar = $rating - $fullStars >= 0.5;
    $emptyStars = 5 - $fullStars - ($halfStar ? 1 : 0);

    $stars = str_repeat('★', $fullStars);
    $stars .= $halfStar ? '½' : '';
    $stars .= str_repeat('☆', $emptyStars);

    return $stars;
}

// Fungsi untuk menampilkan daftar aturan
function displayRules($rules) {
    echo '<ol class="rules-list">';
    foreach ($rules as $rule) {
        echo "<li>$rule</li>";
    }
    echo '</ol>';
}

// Fungsi untuk menampilkan kebijakan refund
function displayRefundPolicy($policy) {
    echo '<ul class="refund-policy-list">';
    foreach ($policy as $item) {
        echo "<li>$item</li>";
    }
    echo '</ul>';
}

// Ganti 'YOUR_API_KEY' dengan API key Anda yang sebenarnya
$apiKey = 'YOUR_API_KEY';
$staticMapUrl = getStaticMapUrl($venue['latitude'], $venue['longitude'], $apiKey);
?>
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><?php echo htmlspecialchars($venue['name']); ?></title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 800px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h1, h2 {
            color: #333;
            border-bottom: 2px solid #eee;
            padding-bottom: 10px;
        }
        .rating {
            font-size: 18px;
            color: #ffa500;
            margin-bottom: 10px;
        }
        .price {
            font-size: 24px;
            color: #28a745;
            font-weight: bold;
            margin: 15px 0;
        }
        .facilities-list, .rules-list, .refund-policy-list {
            padding-left: 20px;
        }
        .facilities-list li, .rules-list li, .refund-policy-list li {
            margin-bottom: 10px;
        }
        .venue-image, .static-map {
            width: 100%;
            max-height: 300px;
            object-fit: cover;
            border-radius: 8px;
            margin-bottom: 20px;
        }
        .map-link {
            display: inline-block;
            margin-top: 20px;
            background-color: #007bff;
            color: white;
            padding: 10px 15px;
            text-decoration: none;
            border-radius: 5px;
            transition: background-color 0.3s;
        }
        .map-link:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1><?php echo htmlspecialchars($venue['name']); ?></h1>
        <img src="<?php echo htmlspecialchars($venue['image']); ?>" alt="<?php echo htmlspecialchars($venue['name']); ?>" class="venue-image">
        <div class="rating">
            Rating: <?php echo $venue['rating']; ?> 
            <?php echo displayStarRating($venue['rating']); ?>
        </div>
        <div class="location">Lokasi: <?php echo htmlspecialchars($venue['location']); ?></div>
        <div class="price"><?php echo formatPrice($venue['price']); ?></div>
        
        <h2>Tentang Venue</h2>
        <p><?php echo htmlspecialchars($venue['description']); ?></p>
        
        <h2>Fasilitas</h2>
        <?php displayFacilities($venue['facilities']); ?>
        
        <h2>Aturan Venue</h2>
        <p><strong>HARAP DIBACA TERLEBIH DAHULU!!!</strong></p>
        <?php displayRules($venue['rules']); ?>
        
        <h2>Kebijakan Refund & Reschedule</h2>
        <?php displayRefundPolicy($venue['refund_policy']); ?>
        
        <img src="<?php echo $staticMapUrl; ?>" alt="Peta Lokasi" class="static-map">
        <a href="<?php echo htmlspecialchars($venue['map_link']); ?>" target="_blank" class="map-link">Buka di Google Maps</a>
    </div>
</body>
</html>