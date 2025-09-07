<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Our Food</title>
  <link rel="preload" as="image" href="images/sundae-soolguk.jpg">
  <style>
    *{box-sizing:border-box}body{margin:0;font-family:ui-sans-serif,system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial;background:#f6f6f6;color:#111}
    .container{max-width:980px;margin:auto;padding:16px}
    .title{font-size:28px;font-weight:700;text-align:center;margin:8px 0 16px}
    .tabs{display:flex;gap:8px;flex-wrap:wrap;justify-content:center;margin:8px 0 16px}
    .tab{padding:10px 14px;border-radius:999px;border:1px solid #e5e7eb;background:#fff;color:#111;cursor:pointer;transition:all .15s}
    .tab.active{background:#111;color:#fff}
    .grid{display:grid;grid-template-columns:1fr;gap:16px}
    @media(min-width:720px){.grid{grid-template-columns:1fr 1fr}}
    .card{background:#fff;border-radius:18px;box-shadow:0 6px 20px rgba(0,0,0,.08);overflow:hidden;display:flex;flex-direction:column}
    .img{width:100%;height:210px;object-fit:cover}
    .pad{padding:14px}
    .name{font-size:18px;font-weight:700;margin:2px 0 6px}
    .desc{font-size:14px;color:#6b7280;margin:0 0 10px}
    .price{font-weight:800;text-align:right}
    .banner{background:linear-gradient(90deg,#e68162,#be4a31);color:#fff;border-radius:18px;margin:10px 0 18px;padding:18px 20px;font-size:22px;font-weight:800;letter-spacing:.6px}
    .options{font-size:14px;color:#374151;display:flex;flex-wrap:wrap;gap:8px;justify-content:flex-end}
    .pill{background:#f3f4f6;border-radius:999px;padding:4px 10px;border:1px solid #e5e7eb}
  </style>
</head>
<body>
  <div class="container">
    <div class="title">Our Food</div>

    <div class="tabs" id="tabs"></div>
    <div class="banner" id="banner">MEALS</div>

    <div class="grid" id="grid"></div>
  </div>

  <script>
    // ====== CONFIG: USD display ======
    const USD_FMT = new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' });
    // 1 USD = RATE KRW (override with ?rate=1350)
    const RATE = Number(new URLSearchParams(location.search).get('rate')) || 1300;
    const krwToUSD = (krw) => USD_FMT.format((krw||0) / RATE);

    // ====== DATA ======
    const DATA = {
      categories: [
        { id: 'meals', label: 'Meals' },
        { id: 'specials', label: 'Specials' },
        { id: 'drinks', label: 'Drinks & Alcohol' },
      ],
      items: [
        // MEALS — Sundae soups
        { id:'sundae-guk', category:'meals', img:'images/sundae-guk.jpg',
          name:'Sundae Soup (Blood Sausage Soup)', desc:'Rich pork-bone broth with Korean blood sausage & chives', priceKRW:8000 },
        { id:'sundae-soolguk', category:'meals', img:'images/sundae-soolguk.jpg',
          name:'Sundae Soolguk (Hangover Soup)', desc:'Deeper, spicier hangover-style soup with sundae & pork', priceKRW:15000 },
        { id:'special-sundae-guk', category:'meals', img:'images/sundae-guk.jpg',
          name:'Special Sundae Soup', desc:'Extra meats & toppings', priceKRW:9000 },

        // SPECIALS — Platters
        { id:'king-sundae', category:'specials', img:'images/assorted-sundae.jpg',
          name:'King Sundae (Whole Blood Sausage)', desc:'Large, shareable Korean blood sausage', priceKRW:18000 },
        { id:'headmeat-suyuk', category:'specials', img:'images/headmeat-suyuk.jpg',
          name:'Boiled Pork Head Slices', desc:'Tender head meat (suyuk) platter', priceKRW:18000 },
        { id:'assorted-sundae', category:'specials', img:'images/assorted-sundae.jpg',
          name:'Assorted Sundae Platter', desc:'Mixed Korean blood sausage selection', priceKRW:18000 },
        { id:'sundae-set', category:'specials', img:'images/sundae-set.jpg',
          name:'Sundae Set Meal', desc:'Sundae with soup & rice', priceKRW:16000 },

        // DRINKS — real product shots
        { id:'soju', category:'drinks', img:'images/soju.jpg',
          name:'Soju', desc:'Korean distilled spirit', priceKRW:4000 },
        { id:'beer', category:'drinks', img:'images/beer.jpg',
          name:'Beer', desc:'Cass / Terra / Kloud', priceKRW:4000 },
        { id:'baekseju', category:'drinks', img:'images/baekseju.jpg',
          name:'Baekseju', desc:'Herbal rice wine', priceKRW:7000 },
        { id:'sansachun', category:'drinks', img:'images/sansachun.jpg',
          name:'Sansachun', desc:'Hawthorn wine', priceKRW:7000 },
        { id:'cheongha', category:'drinks', img:'images/cheongha.jpg',
          name:'Cheongha', desc:'Refined rice wine', priceKRW:5000 },
        { id:'makgeolli', category:'drinks', img:'images/makgeolli.jpg',
          name:'Makgeolli', desc:'Korean rice wine', priceKRW:4000 }
      ]
    };

    // ====== RENDER ======
    let activeCat = 'meals';
    const tabsEl = document.getElementById('tabs');
    const gridEl = document.getElementById('grid');
    const bannerEl = document.getElementById('banner');

    function renderTabs(){
      tabsEl.innerHTML = '';
      DATA.categories.forEach(c => {
        const b = document.createElement('button');
        b.className = 'tab' + (c.id===activeCat?' active':'');
        b.textContent = c.label;
        b.onclick = () => {
          activeCat = c.id;
          bannerEl.textContent = c.label.toUpperCase();
          renderTabs(); // update active style
          renderGrid(); // update list
        };
        tabsEl.appendChild(b);
      });
    }

    function priceBlock(it){
      if (it.options){
        return '<div class="options">' + it.options.map(o=>`<span class="pill">${o.label}: ${krwToUSD(o.price)}</span>`).join(' ') + '</div>';
      }
      return `<div class="price">${krwToUSD(it.priceKRW)}</div>`;
    }

    function renderGrid(){
      const filtered = DATA.items.filter(i => i.category===activeCat);
      gridEl.innerHTML = '';
      filtered.forEach(i => {
        const card = document.createElement('div');
        card.className = 'card';
        card.innerHTML = `
          <img class="img" src="${i.img}" alt="${i.name}" loading="eager" onerror="this.onerror=null;this.src='images/placeholder.jpg'" />
          <div class="pad">
            <div class="name">${i.name}</div>
            <p class="desc">${i.desc}</p>
            ${priceBlock(i)}
          </div>`;
        gridEl.appendChild(card);
      });
      if(filtered.length===0){
        gridEl.innerHTML = '<div style="opacity:.6;text-align:center;padding:24px">No items in this category yet.</div>';
      }
    }

    function render(){ renderTabs(); renderGrid(); }
    render();
  </script>
</body>
</html>
