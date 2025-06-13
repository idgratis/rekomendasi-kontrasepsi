<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Rekomendasi Kontrasepsi</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    label { display: block; margin-top: 10px; }
    select, button { margin-top: 5px; width: 100%; padding: 8px; }
    .result { margin-top: 20px; padding: 10px; background: #f1f1f1; border-radius: 5px; }
  </style>
</head>
<body>
  <h2>Formulir Rekomendasi Kontrasepsi</h2>

  <form id="form-kb">
    <label>1. Usia:
      <select name="usia">
        <option value="<20 tahun">&lt;20 tahun</option>
        <option value="20-35 tahun">20-35 tahun</option>
        <option value=">35 tahun">>35 tahun</option>
      </select>
    </label>

    <label>2. Tujuan ber-KB:
      <select name="tujuan">
        <option value="Menunda kehamilan">Menunda kehamilan</option>
        <option value="Mengatur jarak">Mengatur jarak kehamilan</option>
        <option value="Tidak ingin hamil">Tidak ingin hamil</option>
      </select>
    </label>

    <label>3. Sedang menyusui:
      <select name="menyusui">
        <option value="Ya">Ya</option>
        <option value="Tidak">Tidak</option>
      </select>
    </label>

    <label>4. Merokok:
      <select name="merokok">
        <option value="Ya">Ya</option>
        <option value="Tidak">Tidak</option>
      </select>
    </label>

    <label>5. Masalah hormonal:
      <select name="hormonal">
        <option value="Ya">Ya</option>
        <option value="Tidak">Tidak</option>
      </select>
    </label>

    <label>6. Riwayat penyakit tekanan darah tinggi/jantung/diabetes:
      <select name="penyakit_kronis">
        <option value="Ya">Ya</option>
        <option value="Tidak">Tidak</option>
      </select>
    </label>

    <label>7. Riwayat penyakit menular seksual:
      <select name="pms">
        <option value="Ya">Ya</option>
        <option value="Tidak">Tidak</option>
      </select>
    </label>

    <label>8. Riwayat radang panggul:
      <select name="radang_panggul">
        <option value="Ya">Ya</option>
        <option value="Tidak">Tidak</option>
      </select>
    </label>

    <label>9. Riwayat kanker serviks/payudara:
      <select name="kanker">
        <option value="Ya">Ya</option>
        <option value="Tidak">Tidak</option>
      </select>
    </label>

    <label>10. Masalah haid (seperti darah berlebihan):
      <select name="haid">
        <option value="Ya">Ya</option>
        <option value="Tidak">Tidak</option>
      </select>
    </label>

    <button type="submit">Lihat Rekomendasi</button>
  </form>

  <div class="result" id="hasil"></div>

  <script>
    const dataRekomendasi = {
      "usia": {
        "<20 tahun": ["Pil progestin", "Pil kombinasi", "Kondom"],
        "20-35 tahun": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "AKDR IUD", "Implant", "Kondom"],
        ">35 tahun": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "AKDR IUD", "Implant", "Sterilisasi"]
      },
      "tujuan": {
        "Menunda kehamilan": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "Implant", "AKDR IUD", "Kondom"],
        "Mengatur jarak": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "Implant", "AKDR IUD"],
        "Tidak ingin hamil": ["Implant", "AKDR IUD", "Sterilisasi"]
      },
      "menyusui": {
        "Ya": ["Pil progestin", "Suntik 3 bulan", "AKDR IUD", "Kondom"],
        "Tidak": ["Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "Implant", "AKDR IUD", "Kondom"]
      },
      "merokok": {
        "Ya": ["Kondom", "AKDR IUD"],
        "Tidak": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "Implant", "AKDR IUD", "Kondom"]
      },
      "hormonal": {
        "Ya": ["AKDR IUD", "Kondom"],
        "Tidak": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "Implant", "AKDR IUD", "Kondom"]
      },
      "penyakit_kronis": {
        "Ya": ["AKDR IUD", "Kondom", "Sterilisasi"],
        "Tidak": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "Implant", "AKDR IUD", "Kondom"]
      },
      "pms": {
        "Ya": ["Kondom"],
        "Tidak": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "Implant", "AKDR IUD", "Kondom"]
      },
      "radang_panggul": {
        "Ya": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "Implant", "Kondom"],
        "Tidak": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "Implant", "AKDR IUD", "Kondom"]
      },
      "kanker": {
        "Ya": ["Kondom", "AKDR IUD"],
        "Tidak": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "Implant", "AKDR IUD", "Kondom"]
      },
      "haid": {
        "Ya": ["Pil kombinasi", "Implant", "Suntik 1 bulan"],
        "Tidak": ["Pil progestin", "Pil kombinasi", "Suntik 1 bulan", "Suntik 3 bulan", "Implant", "AKDR IUD", "Kondom"]
      }
    };

    document.getElementById("form-kb").addEventListener("submit", function(e) {
      e.preventDefault();

      const form = new FormData(e.target);
      let hasilSet = null;

      for (let [key, value] of form.entries()) {
        const rekom = dataRekomendasi[key][value];
        if (hasilSet === null) {
          hasilSet = new Set(rekom);
        } else {
          hasilSet = new Set(rekom.filter(r => hasilSet.has(r)));
        }
      }

      const hasil = Array.from(hasilSet || []);
      const hasilDiv = document.getElementById("hasil");
      hasilDiv.innerHTML = hasil.length ?
        `<strong>Rekomendasi metode kontrasepsi:</strong><ul>${hasil.map(r => `<li>${r}</li>`).join('')}</ul>` :
        `<strong>Tidak ada metode kontrasepsi yang sesuai dengan semua kriteria.</strong>`;
    });
  </script>
</body>
</html>
