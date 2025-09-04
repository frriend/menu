<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Our Food</title>
  <style>
    *{box-sizing:border-box}body{margin:0;font-family:ui-sans-serif,system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial;background:#f6f6f6;color:#111}
    .container{max-width:980px;margin:auto;padding:16px}
    .title{font-size:28px;font-weight:700;text-align:center;margin:8px 0 16px}
    .tabs{display:flex;gap:8px;flex-wrap:wrap;justify-content:center;margin:8px 0 16px}
    .tab{padding:10px 14px;border-radius:999px;border:1px solid #e5e7eb;background:#fff;color:#111;cursor:pointer}
    .tab.active{background:#111;color:#fff}
    .search{width:100%;padding:12px 14px;border:1px solid #e5e7eb;border-radius:12px;margin:8px 0 16px}
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

    <input class="search" id="search" placeholder="Search menu... (e.g., pork, noodles)" />

    <div class="grid" id="grid"></div>
  </div>

  <script>
    // --- Data (English only) ---
    const KRW = '₩';
    const DATA = {
      categories: [
        { id: 'meals', label: 'Meals' },
        { id: 'specials', label: 'Specials' },
        { id: 'drinks', label: 'Drinks & Alcohol' },
      ],
      items: [
        // MEALS
        { id:'pork-noodle', category:'meals', img:'https://images.unsplash.com/photo-1604908815163-9f9f2b805d6c?q=80&w=1200&auto=format&fit=crop',
          name:'Jeju Pork Noodle Soup', desc:'Signature pork broth with noodles. (Regular / Large)',
          options:[{label:'Regular', price:9000},{label:'Large', price:14000}] },
        { id:'pork-rice-soup', category:'meals', img:'https://images.unsplash.com/photo-1617191518000-6d4c27da1e8c?q=80&w=1200&auto=format&fit=crop',
          name:'Jeju Pork Rice Soup', desc:'Pork soup served with rice. (Regular / Large)',
          options:[{label:'Regular', price:9000},{label:'Large', price:14000}] },
        { id:'spicy-mixed-noodles', category:'meals', img:'https://images.unsplash.com/photo-1604908177093-4a3a6d53295f?q=80&w=1200&auto=format&fit=crop',
          name:'Spicy Mixed Noodles', desc:'Chilled noodles mixed with spicy sauce', priceKRW:9000 },
        { id:'momguk', category:'meals', img:'https://images.unsplash.com/photo-1602333866831-6548b1f0a950?q=80&w=1200&auto=format&fit=crop',
          name:'Momguk (Jeju Seaweed Pork Soup)', desc:'Daily limited. Seaweed & pork soup', priceKRW:9000 },

        // SPECIALS
        { id:'dombae-pork', category:'specials', img:'https://images.unsplash.com/photo-1604908176948-1f7c24c9b1bb?q=80&w=1200&auto=format&fit=crop',
          name:'Dombae Pork Slices', desc:'Sliced boiled pork (board serving)', options:[
            {label:'Half Board', price:13000}, {label:'Regular', price:25000}, {label:'Large', price:35000}
          ] },
        { id:'jeju-sundae', category:'specials', img:'https://images.unsplash.com/photo-1550547660-d9450f859349?q=80&w=1200&auto=format&fit=crop',
          name:'Jeju Glutinous Rice Sundae', desc:'Blood sausage, daily limited', priceKRW:15000 },
        { id:'steamed-rice', category:'specials', img:'https://images.unsplash.com/photo-1542444459-db63c4b2c8d2?q=80&w=1200&auto=format&fit=crop',
          name:'Steamed Rice', desc:'Plain white rice', priceKRW:1000 },

        // DRINKS
        { id:'cola-sprite', category:'drinks', img:'https://images.unsplash.com/photo-1541976076758-347942db197a?q=80&w=1200&auto=format&fit=crop',
          name:'Cola / Cider (Lemon-lime soda)', desc:'Bottled soft drink', priceKRW:2000 },
        { id:'hallasan-soju', category:'drinks', img:'https://images.unsplash.com/photo-1603565816274-976f3b6b3a0c?q=80&w=1200&auto=format&fit=crop',
          name:'Hallasan Soju', desc:'17% or 21%', priceKRW:5000 },
        { id:'udo-peanut-makgeolli', category:'drinks', img:'https://images.unsplash.com/photo-1613478223719-2b6d38396f2a?q=80&w=1200&auto=format&fit=crop',
          name:'Udo Peanut Makgeolli', desc:'Jeju specialty', priceKRW:7000 },
        { id:'cass-bottle', category:'drinks', img:'https://images.unsplash.com/photo-1541976076758-347942db197a?q=80&w=1200&auto=format&fit=crop',
          name:'Cass Beer (Bottle)', desc:'Korean lager', priceKRW:5000 },
        { id:'jeju-wheat-ale', category:'drinks', img:'https://images.unsplash.com/photo-1516455590571-18256e5bb9ff?q=80&w=1200&auto=format&fit=crop',
          name:'Jeju Wheat Ale (330ml)', desc:'Bottle', priceKRW:8000 },
        { id:'nimome', category:'drinks', img:'https://images.unsplash.com/photo-1532634896-26909d0d4b6a?q=80&w=1200&auto=format&fit=crop',
          name:'Nimome 11% (375ml)', desc:'Jeju citrus liqueur', priceKRW:15000 },
        { id:'hondiju', category:'drinks', img:'https://images.unsplash.com/photo-1532634896-26909d0d4b6a?q=80&w=1200&auto=format&fit=crop',
          name:'Hondiju 12% (330ml)', desc:'Jeju liqueur', priceKRW:15000 },
        { id:'omegi-sul', category:'drinks', img:'https://images.unsplash.com/photo-1532634896-26909d0d4b6a?q=80&w=1200&auto=format&fit=crop',
          name:'Omegi Sul 13% (375ml)', desc:'Jeju millet liqueur', priceKRW:15000 },
        { id:'gosori-sul', category:'drinks', img:'https://images.unsplash.com/photo-1563379926898-05f4575a45d8?q=80&w=1200&auto=format&fit=crop',
          name:'Gosori Sul 40% (375ml)', desc:'Jeju distilled spirit', priceKRW:35000 },
      ]
    };

    // --- State & Render ---
    let activeCat = 'meals';
    const tabsEl = document.getElementById('tabs');
    const gridEl = document.getElementById('grid');
    const bannerEl = document.getElementById('banner');
    const searchEl = document.getElementById('search');

    function renderTabs(){
      tabsEl.innerHTML = '';
      DATA.categories.forEach(c => {
        const b = document.createElement('button');
        b.className = 'tab' + (c.id===activeCat?' active':'');
        b.textContent = c.label;
        b.onclick = () => { activeCat = c.id; bannerEl.textContent = c.label.toUpperCase(); renderGrid(); };
        tabsEl.appendChild(b);
      });
    }

    function priceBlock(it){
      if (it.options){
        return '<div class="options">' + it.options.map(o=>`<span class="pill">${o.label}: ${KRW}${o.price.toLocaleString()}</span>`).join(' ') + '</div>';
      }
      return `<div class="price">${KRW}${(it.priceKRW||0).toLocaleString()}</div>`;
    }

    function renderGrid(){
      const q = (searchEl.value||'').toLowerCase();
      const filtered = DATA.items.filter(i => i.category===activeCat && (i.name.toLowerCase().includes(q) || i.desc.toLowerCase().includes(q)));
      gridEl.innerHTML = '';
      filtered.forEach(i => {
        const card = document.createElement('div');
        card.className = 'card';
        card.innerHTML = `
          <img class="img" src="${i.img}" alt="${i.name}"/>
          <div class="pad">
            <div class="name">${i.name}</div>
            <p class="desc">${i.desc}</p>
            ${priceBlock(i)}
          </div>`;
        gridEl.appendChild(card);
      });
    }

    function render(){ renderTabs(); renderGrid(); }

    searchEl.addEventListener('input', renderGrid);
    render();
  </script>
</body>
</html>
