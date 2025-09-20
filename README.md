<!doctype html>
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Pesan Pick Up — @azkasemarang.id</title>
  <meta name="description" content="Formulir pemesanan pick up & delivery cuci sepatu @azkasemarang.id — pilih alamat via Google Maps Autocomplete" />

  <!-- Styling: navy / putih / aksen emas -->
  <style>
    :root{
      --navy:#052240;
      --soft-navy:#0a3d91;
      --gold:#d4af37;
      --muted:#64748b;
      --bg:#f8fafc;
      --card:#ffffff;
      --radius:12px;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter,ui-sans-serif,system-ui,Arial,Helvetica,sans-serif;background:var(--bg);color:#0f172a;-webkit-font-smoothing:antialiased}
    .wrap{max-width:920px;margin:36px auto;padding:20px}
    header{display:flex;align-items:center;gap:14px;padding:18px;border-radius:14px;background:linear-gradient(90deg,var(--navy),var(--soft-navy));color:white}
    .brand{display:flex;gap:12px;align-items:center}
    .logo{width:56px;height:56px;border-radius:10px;background:linear-gradient(135deg,#ffffff20,#ffffff10);display:flex;align-items:center;justify-content:center;font-weight:700;color:var(--gold);font-size:20px}
    header h1{font-size:18px;margin:0}
    header p{margin:0;font-size:13px;opacity:.9}

    .card{background:var(--card);border-radius:var(--radius);padding:20px;box-shadow:0 8px 30px rgba(2,6,23,.06);margin-top:18px}
    .grid{display:grid;grid-template-columns:1fr 380px;gap:20px}
    @media(max-width:880px){.grid{grid-template-columns:1fr}}

    form .field{margin-bottom:12px}
    label{display:block;font-size:13px;color:var(--muted);margin-bottom:8px}
    input[type="text"], input[type="tel"], input[type="date"], input[type="time"], textarea, select{
      width:100%;padding:12px;border-radius:10px;border:1px solid #e6eef6;font-size:15px;background:#fbfdff;outline:none
    }
    textarea{resize:vertical;min-height:86px}

    .two-col{display:grid;grid-template-columns:1fr 1fr;gap:12px}
    .btn-primary{background:var(--soft-navy);color:white;padding:12px 16px;border-radius:10px;border:none;font-weight:600;cursor:pointer}
    .btn-ghost{background:transparent;border:1px solid #e6eef6;padding:10px 14px;border-radius:10px;cursor:pointer}

    .note{font-size:13px;color:var(--muted);margin-top:8px}
    .service-meta{display:flex;gap:12px;align-items:center;margin-top:12px}
    .service-chip{background:#f1f6ff;padding:8px 12px;border-radius:999px;font-weight:600;color:var(--soft-navy);border:1px solid #e6eef6}

    .tracking{background:#fbfbff;padding:12px;border-radius:10px;border:1px dashed #e6eef6}
    .tracking .row{display:flex;gap:8px;align-items:center}

    footer{margin-top:18px;text-align:center;color:var(--muted);font-size:13px}
    .powered{display:flex;gap:8px;align-items:center;justify-content:center;margin-top:10px}
    .map-hint{font-size:13px;color:var(--muted);margin-top:6px}
  </style>

  <!-- Google Maps Places API (ganti YOUR_API_KEY) -->
  <script src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&libraries=places&v=weekly" defer></script>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="brand">
        <div class="logo">AZK</div>
        <div>
          <h1>@azkasemarang.id</h1>
          <p>Pick Up & Delivery · Cuci Sepatu Profesional — Semarang</p>
        </div>
      </div>
    </header>

    <div class="card">
      <div style="display:flex;justify-content:space-between;align-items:center;gap:12px;flex-wrap:wrap">
        <div>
          <h2 style="margin:0;font-size:20px;color:var(--navy)">Pesan Layanan Pick Up</h2>
          <div class="note">Isi data di bawah. Pilih alamat dari saran Google Maps agar penjemputan akurat.</div>
        </div>
        <div class="service-chip">Gratis penjemputan area Semarang</div>
      </div>

      <div class="grid" style="margin-top:18px">
        <!-- LEFT: FORM -->
        <div>
          <form id="orderForm" class="order-form" autocomplete="off">
            <div class="field">
              <label for="name">Nama Lengkap <span style="color:#dc2626">*</span></label>
              <input id="name" name="name" type="text" placeholder="Contoh: Budi Santoso" required />
            </div>

            <div class="two-col">
              <div class="field">
                <label for="phone">Nomor WA / HP <span style="color:#dc2626">*</span></label>
                <input id="phone" name="phone" type="tel" inputmode="tel" placeholder="0812xxxxxxx" required />
              </div>
              <div class="field">
                <label for="package">Paket Layanan</label>
                <select id="package" name="package">
                  <option>Paket Cuci Sepatu Reguler — Rp 35.000</option>
                  <option>Paket Deep Cleaning — Rp 60.000</option>
                  <option>Paket Premium / Leather Care — Rp 120.000</option>
                  <option>Paket Kilat (Express) — Rp 80.000</option>
                </select>
              </div>
            </div>

            <div class="field">
              <label for="alamat">Alamat (pilih dari saran) <span style="color:#dc2626">*</span></label>
              <input id="alamat" name="alamat" type="text" placeholder="Ketik alamat lalu pilih saran" required />
              <div class="map-hint">Tip: kamu bisa klik hasil saran → alamat dan koordinat akan tersimpan otomatis.</div>
            </div>

            <div class="two-col">
              <div class="field">
                <label for="pickup-date">Tanggal Pick-up <span style="color:#dc2626">*</span></label>
                <input id="pickup-date" name="pickup_date" type="date" required />
              </div>
              <div class="field">
                <label for="pickup-time">Waktu Pick-up <span style="color:#dc2626">*</span></label>
                <input id="pickup-time" name="pickup_time" type="time" required />
              </div>
            </div>

            <div class="field">
              <label for="notes">Catatan (opsional)</label>
              <textarea id="notes" name="notes" placeholder="Contoh: Belok kiri di depan toko bunga"></textarea>
            </div>

            <!-- hidden fields for lat/lng -->
            <input type="hidden" id="lat" name="lat" />
            <input type="hidden" id="lng" name="lng" />

            <div style="display:flex;gap:12px;align-items:center;margin-top:8px">
              <button type="submit" class="btn-primary">Kirim & Konfirmasi WA</button>
              <button type="button" id="resetBtn" class="btn-ghost">Reset</button>
            </div>

            <div id="feedback" style="margin-top:12px;font-size:14px;color:var(--muted)"></div>
          </form>
        </div>

        <!-- RIGHT: INFO / TRACKING -->
        <aside>
          <div class="tracking">
            <div style="font-weight:700;margin-bottom:8px">Tracking (contoh demo)</div>
            <div class="row"><input id="trackNo" placeholder="Masukkan No. Pesanan (AZK-1001)" style="flex:1;padding:10px;border-radius:8px;border:1px solid #eef6ff" /> <button id="checkTrack" class="btn-ghost">Cek</button></div>
            <div id="trackResult" style="margin-top:10px;color:var(--muted);font-size:14px"></div>
          </div>

          <div style="margin-top:18px">
            <h4 style="margin:0">Kontak</h4>
            <div class="note" style="margin-top:8px">
              WhatsApp: <a id="waLink" href="#" style="color:var(--soft-navy);text-decoration:none">+62 812-3456-7890</a><br/>
              Instagram: <a href="https://instagram.com/azkasemarang.id" target="_blank" style="color:var(--soft-navy);text-decoration:none">@azkasemarang.id</a>
            </div>
            <div style="margin-top:12px" class="note">Alamat: Jl. Contoh No.123, Semarang</div>
          </div>

          <div style="margin-top:16px;font-size:13px;color:var(--muted)">
            <strong>Catatan teknis:</strong><br/>
            Form ini mengirim ke Formspree + membuka WhatsApp admin untuk konfirmasi. Kamu dapat menonaktifkan WA-redirect jika ingin simpan hanya ke backend.
          </div>
        </aside>
      </div>
    </div>

    <footer>
      <div>Copyright © 2025 @azkasemarang.id</div>
      <div class="powered">Dibuat untuk layanan pick up & delivery sepatu · Semarang</div>
    </footer>
  </div>

  <script>
    /* ====== CONFIG: ganti nilai ini sebelum deploy ====== */
    const FORMSPREE_ENDPOINT = 'https://formspree.io/f/your-form-id'; // <-- ganti dengan endpoint Formspree milikmu
    const ADMIN_WA = '6281234567890'; // <-- ganti dengan nomor admin (format internasional tanpa +)
    /* =================================================== */

    // Simple mock tracking demo
    const MOCK_STATUS = {
      'AZK-1001': 'Dijemput',
      'AZK-1002': 'Sedang Dicuci',
      'AZK-1003': 'Selesai',
      'AZK-1004': 'Dalam Pengiriman'
    };

    document.getElementById('checkTrack').addEventListener('click', () => {
      const id = (document.getElementById('trackNo').value || '').trim().toUpperCase();
      if(!id) { document.getElementById('trackResult').textContent = 'Masukkan nomor pesanan.'; return; }
      const status = MOCK_STATUS[id] || 'Tidak ditemukan';
      document.getElementById('trackResult').textContent = `Status: ${status}`;
    });

    // Google Places Autocomplete init
    function initAutocomplete(){
      const input = document.getElementById('alamat');
      if (!window.google || !google.maps || !google.maps.places) {
        console.warn('Google Maps API belum termuat. Pastikan API key benar.');
        return;
      }
      const options = { componentRestrictions: { country: 'id' } };
      const autocomplete = new google.maps.places.Autocomplete(input, options);
      autocomplete.setFields(['formatted_address','geometry','name']);
      autocomplete.addListener('place_changed', () => {
        const place = autocomplete.getPlace();
        if(!place.geometry) return;
        const lat = place.geometry.location.lat();
        const lng = place.geometry.location.lng();
        document.getElementById('lat').value = lat;
        document.getElementById('lng').value = lng;
      });
    }
    window.addEventListener('load', () => {
      if (typeof google === 'object' && google.maps) initAutocomplete();
    });

    // Form submit: send to Formspree, then open WA with summary
    document.getElementById('orderForm').addEventListener('submit', async function(e){
      e.preventDefault();
      const btn = this.querySelector('.btn-primary');
      const feedback = document.getElementById('feedback');
      feedback.style.color = 'var(--muted)';
      feedback.textContent = 'Mengirim...';

      const data = {
        name: document.getElementById('name').value.trim(),
        phone: document.getElementById('phone').value.trim(),
        package: document.getElementById('package').value,
        address: document.getElementById('alamat').value.trim(),
        pickup_date: document.getElementById('pickup-date').value,
        pickup_time: document.getElementById('pickup-time').value,
        notes: document.getElementById('notes').value.trim(),
        lat: document.getElementById('lat').value,
        lng: document.getElementById('lng').value,
        source: 'website-order-form'
      };

      // basic validation
      if(!data.name || !data.phone || !data.address || !data.pickup_date || !data.pickup_time){
        feedback.textContent = 'Lengkapi field yang wajib.';
        feedback.style.color = 'crimson';
        return;
      }

      try{
        // kirim ke Formspree
        const res = await fetch(FORMSPREE_ENDPOINT, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json', 'Accept': 'application/json' },
          body: JSON.stringify(data)
        });

        if(!res.ok){
          const txt = await res.text();
          console.warn('Formspree respons:', res.status, txt);
          feedback.textContent = 'Gagal mengirim. Coba lagi atau hubungi via WA.';
          feedback.style.color = 'crimson';
          return;
        }

        feedback.textContent = 'Terkirim! Membuka WhatsApp untuk konfirmasi...';
        feedback.style.color = 'green';

        // prepare WA message
        const msg = `Halo Admin AzkaSemarang.id%0A%0ANama:%20${encodeURIComponent(data.name)}%0ANo:%20${encodeURIComponent(data.phone)}%0APaket:%20${encodeURIComponent(data.package)}%0AAlamat:%20${encodeURIComponent(data.address)}%0ATanggal%20Pick-up:%20${encodeURIComponent(data.pickup_date)}%0AWaktu:%20${encodeURIComponent(data.pickup_time)}%0ANote:%20${encodeURIComponent(data.notes || '-')}%0A%0A(Ini%20dikirim%20dari%20form%20website)`;

        // open WA in new tab
        const waUrl = `https://wa.me/${ADMIN_WA}?text=${msg}`;
        window.open(waUrl, '_blank');

        // optional: reset form after small delay
        setTimeout(()=>{ document.getElementById('orderForm').reset(); document.getElementById('lat').value=''; document.getElementById('lng').value=''; feedback.textContent=''; }, 2500);

      }catch(err){
        console.error(err);
        feedback.textContent = 'Terjadi kesalahan jaringan. Silakan coba lagi.';
        feedback.style.color = 'crimson';
      }
    });

    document.getElementById('resetBtn').addEventListener('click', ()=>document.getElementById('orderForm').reset());
  </script>
</body>
</html>
# form-pickup
web
