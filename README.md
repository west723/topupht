<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NexUp Game Store</title>
<style>
  :root{
    --bg:#0b1020;
    --bg2:#11172b;
    --card:#161d35;
    --line:#242c4a;
    --text:#eef1fb;
    --sub:#9aa3c7;
    --accent:#baff29;
    --accent2:#5eead4;
    --danger:#ff5470;
    --warn:#ffb454;
  }
  *{box-sizing:border-box;margin:0;padding:0;}
  html,body{background:var(--bg);color:var(--text);font-family:'Segoe UI',system-ui,-apple-system,sans-serif;-webkit-font-smoothing:antialiased;}
  body{padding-bottom:70px;}
  a{color:inherit;text-decoration:none;}
  button{font-family:inherit;cursor:pointer;}
  input,select{font-family:inherit;}

  header{
    position:sticky;top:0;z-index:50;
    background:rgba(11,16,32,0.92);
    backdrop-filter:blur(8px);
    border-bottom:1px solid var(--line);
    padding:14px 16px;
    display:flex;align-items:center;justify-content:space-between;
  }
  .logo{
    font-family:'Arial Black',sans-serif;
    font-weight:900;font-size:20px;letter-spacing:-0.5px;
    display:flex;align-items:center;gap:8px;
  }
  .logo .dot{width:9px;height:9px;background:var(--accent);border-radius:2px;display:inline-block;transform:rotate(45deg);}
  .header-icons{display:flex;align-items:center;gap:8px;}
  .balance-badge{
    display:none;align-items:center;gap:5px;background:var(--card);border:1px solid var(--line);
    border-radius:10px;padding:0 10px;height:38px;font-size:13px;font-weight:800;color:var(--accent);
    white-space:nowrap;cursor:pointer;
  }
  .balance-badge .balance-plus{
    display:inline-flex;align-items:center;justify-content:center;
    width:16px;height:16px;margin-left:2px;border-radius:50%;
    background:var(--accent);color:#04241f;font-size:11px;font-weight:900;line-height:1;
  }
  .icon-btn{
    position:relative;background:var(--card);border:1px solid var(--line);
    width:38px;height:38px;border-radius:10px;
    display:flex;align-items:center;justify-content:center;font-size:16px;
  }
  .icon-badge{
    position:absolute;top:-6px;right:-6px;background:var(--accent);color:#05170f;
    font-size:10px;font-weight:800;border-radius:8px;padding:2px 5px;min-width:16px;text-align:center;
  }
  .icon-badge.danger{background:var(--danger);color:#fff;}

  .search-wrap{padding:14px 16px 4px;}
  .search-box{
    display:flex;align-items:center;gap:8px;
    background:var(--card);border:1px solid var(--line);border-radius:12px;
    padding:10px 12px;color:var(--sub);font-size:14px;
  }

  .slider{
    margin:16px;border-radius:16px;overflow:hidden;position:relative;height:130px;
    border:1px solid var(--line);
  }
  .slide{
    position:absolute;inset:0;display:flex;flex-direction:column;justify-content:center;
    padding:18px;opacity:0;transition:opacity 0.5s ease;
  }
  .slide.active{opacity:1;}
  .slide .tag{font-size:10.5px;font-weight:800;letter-spacing:1px;text-transform:uppercase;margin-bottom:6px;}
  .slide h3{font-size:18px;font-weight:900;margin-bottom:4px;}
  .slide p{font-size:12px;color:rgba(255,255,255,0.8);}
  .slide-dots{position:absolute;bottom:10px;left:0;right:0;display:flex;justify-content:center;gap:6px;}
  .slide-dot{width:6px;height:6px;border-radius:50%;background:rgba(255,255,255,0.35);}
  .slide-dot.active{background:var(--accent);width:16px;border-radius:4px;}

  .hero{
    margin:16px;border-radius:18px;padding:22px 18px;
    background:
      radial-gradient(120% 140% at 100% 0%, rgba(186,255,41,0.18), transparent 55%),
      radial-gradient(120% 140% at 0% 100%, rgba(94,234,212,0.14), transparent 55%),
      linear-gradient(160deg, #141b36, #0d1226);
    border:1px solid var(--line);
    position:relative;overflow:hidden;
  }
  .hero .eyebrow{
    font-size:11px;letter-spacing:1.5px;text-transform:uppercase;
    color:var(--accent);font-weight:700;margin-bottom:8px;
  }
  .hero h1{font-size:26px;line-height:1.15;font-weight:900;letter-spacing:-0.5px;margin-bottom:8px;}
  .hero p{color:var(--sub);font-size:13.5px;margin-bottom:16px;max-width:32ch;}
  .hero-actions{display:flex;gap:10px;}
  .btn-primary{
    background:var(--accent);color:#05170f;font-weight:800;font-size:13.5px;
    padding:11px 16px;border-radius:10px;border:none;
  }
  .btn-ghost{
    background:transparent;color:var(--text);font-weight:700;font-size:13.5px;
    padding:11px 16px;border-radius:10px;border:1px solid var(--line);
  }
  .btn-block{width:100%;padding:13px 16px;border-radius:10px;font-weight:800;font-size:14px;border:none;margin-top:6px;}

  .btn-google{
    width:100%;background:#fff;color:#3c4043;font-weight:700;font-size:13.5px;
    padding:11px 16px;border-radius:10px;border:1px solid var(--line);
    display:flex;align-items:center;justify-content:center;gap:10px;margin-top:6px;
  }
  .btn-google .g-ico{width:18px;height:18px;flex:0 0 auto;}
  .or-divider{display:flex;align-items:center;gap:10px;margin:16px 0;color:var(--sub);font-size:11.5px;}
  .or-divider::before,.or-divider::after{content:'';flex:1;height:1px;background:var(--line);}
  .legal-link{text-align:center;font-size:11.5px;color:var(--sub);margin-top:14px;line-height:1.6;}
  .legal-link b{color:var(--accent);cursor:pointer;font-weight:700;}

  .section{padding:6px 16px 4px;}
  .section-head{display:flex;align-items:baseline;justify-content:space-between;margin:18px 0 12px;}
  .section-head h2{font-size:16px;font-weight:800;}
  .section-head span{font-size:12px;color:var(--sub);}

  .cat-rail, .row-scroll{display:flex;gap:10px;overflow-x:auto;padding-bottom:6px;scrollbar-width:none;}
  .cat-rail::-webkit-scrollbar, .row-scroll::-webkit-scrollbar{display:none;}
  .cat-chip{
    flex:0 0 auto;background:var(--card);border:1px solid var(--line);
    border-radius:12px;padding:12px 14px;min-width:84px;text-align:center;
  }
  .cat-chip .ico{font-size:20px;margin-bottom:6px;}
  .cat-chip .lbl{font-size:11px;color:var(--sub);font-weight:600;}
  .cat-chip.active{border-color:var(--accent);background:rgba(186,255,41,0.08);}
  .cat-chip.active .lbl{color:var(--accent);}

  .grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
  .product{
    background:var(--card);border:1px solid var(--line);border-radius:14px;
    padding:12px;position:relative;flex:0 0 auto;
  }
  .row-scroll .product{width:150px;}
  .product .badge{
    position:absolute;top:10px;left:10px;background:var(--danger);color:#fff;
    font-size:9.5px;font-weight:800;padding:3px 7px;border-radius:6px;letter-spacing:0.3px;
  }
  .product .badge.new{background:var(--accent2);color:#04241f;}
  .product .badge.top{background:var(--warn);color:#331c00;}
  .product .art{
    height:78px;border-radius:10px;margin-bottom:10px;
    display:flex;align-items:center;justify-content:center;font-size:28px;
  }
  .product h3{font-size:13.5px;font-weight:700;margin-bottom:2px;}
  .product .meta{font-size:11px;color:var(--sub);margin-bottom:10px;}
  .product .row{display:flex;align-items:center;justify-content:space-between;}
  .product .price{font-size:14px;font-weight:800;color:var(--accent);}
  .product .price .old{
    display:block;font-size:10.5px;color:var(--sub);
    font-weight:600;text-decoration:line-through;
  }
  .add-btn{
    width:30px;height:30px;border-radius:9px;border:none;
    background:var(--accent);color:#05170f;font-weight:900;font-size:16px;
    display:flex;align-items:center;justify-content:center;
  }
  .see-price{
    width:100%;background:transparent;border:1px solid var(--line);color:var(--accent2);
    font-size:12px;font-weight:700;padding:9px 0;border-radius:9px;
  }

  .quick-recharge{
    background:linear-gradient(135deg, rgba(186,255,41,0.10), rgba(94,234,212,0.08));
    border:1px solid var(--line);border-radius:14px;padding:16px;
  }
  .quick-recharge h3{font-size:15px;font-weight:800;margin-bottom:4px;}
  .quick-recharge p{font-size:12px;color:var(--sub);margin-bottom:12px;}
  .qr-row{display:flex;gap:8px;margin-bottom:8px;}
  .qr-row select, .qr-row input{
    flex:1;background:var(--bg2);border:1px solid var(--line);color:var(--text);
    border-radius:9px;padding:10px 12px;font-size:13px;
  }

  .steps{display:flex;flex-direction:column;gap:10px;}
  .step{
    display:flex;gap:12px;background:var(--card);border:1px solid var(--line);
    border-radius:12px;padding:12px 14px;align-items:flex-start;
  }
  .step .num{
    flex:0 0 auto;width:26px;height:26px;border-radius:8px;background:rgba(186,255,41,0.12);
    color:var(--accent);font-weight:800;font-size:12.5px;display:flex;align-items:center;justify-content:center;
  }
  .step h4{font-size:13px;font-weight:700;margin-bottom:2px;}
  .step p{font-size:12px;color:var(--sub);}

  .review-card{
    background:var(--card);border:1px solid var(--line);border-radius:14px;
    padding:14px;width:220px;flex:0 0 auto;
  }
  .review-card .stars{color:var(--warn);font-size:13px;margin-bottom:6px;}
  .review-card p{font-size:12px;color:var(--sub);line-height:1.5;margin-bottom:10px;}
  .review-card .who{font-size:11.5px;font-weight:700;}

  .faq{background:var(--card);border:1px solid var(--line);border-radius:12px;padding:4px 14px;margin-bottom:8px;}
  .faq summary{font-size:13px;font-weight:700;padding:12px 0;list-style:none;display:flex;justify-content:space-between;align-items:center;}
  .faq summary::-webkit-details-marker{display:none;}
  .faq summary::after{content:"+";color:var(--accent);font-size:16px;font-weight:900;}
  .faq[open] summary::after{content:"–";}
  .faq p{font-size:12px;color:var(--sub);padding-bottom:12px;line-height:1.5;}

  .lookup{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:14px;}
  .lookup .row2{display:flex;gap:8px;margin-top:10px;}
  .lookup input{
    flex:1;background:var(--bg2);border:1px solid var(--line);color:var(--text);
    border-radius:9px;padding:10px 12px;font-size:13px;
  }
  .lookup button{
    background:var(--accent2);color:#04241f;border:none;border-radius:9px;
    padding:0 16px;font-weight:800;font-size:12.5px;
  }

  .screen{display:none;padding:16px;}
  .screen.active{display:block;}
  .screen-header{display:flex;align-items:center;gap:10px;margin-bottom:18px;}
  .back-btn{
    width:34px;height:34px;border-radius:9px;background:var(--card);border:1px solid var(--line);
    display:flex;align-items:center;justify-content:center;font-size:16px;
  }
  .screen-title{font-size:18px;font-weight:900;}
  .field{margin-bottom:12px;}
  .field label{display:block;font-size:12px;color:var(--sub);margin-bottom:6px;font-weight:600;}
  .field input{
    width:100%;background:var(--card);border:1px solid var(--line);color:var(--text);
    border-radius:10px;padding:12px 14px;font-size:13.5px;
  }
  .field input:focus{outline:none;border-color:var(--accent);}
  .form-note{font-size:12px;color:var(--sub);text-align:center;margin-top:14px;}
  .form-note b{color:var(--accent2);font-weight:700;}
  .form-card{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:16px;}

  .avatar-row{display:flex;align-items:center;gap:14px;margin-bottom:18px;}
  .avatar{
    width:58px;height:58px;border-radius:16px;background:linear-gradient(135deg,#2c1e57,#4a2f7d);
    display:flex;align-items:center;justify-content:center;font-size:24px;font-weight:900;
  }
  .avatar-row .name{font-size:16px;font-weight:800;}
  .avatar-row .email{font-size:12px;color:var(--sub);}

  .menu-list{display:flex;flex-direction:column;gap:8px;}
  .menu-item{
    display:flex;align-items:center;justify-content:space-between;
    background:var(--card);border:1px solid var(--line);border-radius:12px;padding:14px;font-size:13.5px;font-weight:600;
  }
  .menu-item .l{display:flex;align-items:center;gap:10px;}
  .menu-item .chev{color:var(--sub);}

  .order-item, .invoice-item, .notif-item{
    background:var(--card);border:1px solid var(--line);border-radius:12px;padding:13px 14px;margin-bottom:10px;
  }
  .order-item .top-row, .invoice-item .top-row{display:flex;justify-content:space-between;align-items:center;margin-bottom:4px;}
  .order-item .id, .invoice-item .id{font-size:13px;font-weight:800;}
  .order-item .date, .invoice-item .date{font-size:11px;color:var(--sub);}
  .status{font-size:10.5px;font-weight:800;padding:3px 9px;border-radius:20px;}
  .status.done{background:rgba(94,234,212,0.15);color:var(--accent2);}
  .status.pending{background:rgba(255,180,84,0.15);color:var(--warn);}
  .status.failed{background:rgba(255,84,112,0.15);color:var(--danger);}
  .invoice-item .row2{display:flex;justify-content:space-between;align-items:center;margin-top:8px;}
  .invoice-item .amount{font-weight:800;color:var(--accent);}
  .invoice-item .dl{font-size:11.5px;font-weight:700;color:var(--accent2);}

  .notif-item{display:flex;gap:10px;}
  .notif-item.unread{border-color:rgba(186,255,41,0.35);}
  .notif-item .ico{font-size:18px;}
  .notif-item .txt p{font-size:11.5px;color:var(--sub);margin-top:2px;}
  .notif-item .txt h4{font-size:13px;font-weight:700;}

  .pay-option{
    display:flex;align-items:center;gap:12px;background:var(--card);border:1.5px solid var(--line);
    border-radius:12px;padding:14px;margin-bottom:10px;
  }
  .pay-option.selected{border-color:var(--accent);background:rgba(186,255,41,0.06);}
  .pay-option .ico{width:38px;height:38px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;font-weight:900;}
  .pay-option .txt h4{font-size:13.5px;font-weight:700;}
  .pay-option .txt p{font-size:11px;color:var(--sub);}
  .pay-option .radio{margin-left:auto;width:18px;height:18px;border-radius:50%;border:2px solid var(--line);}
  .pay-option.selected .radio{border-color:var(--accent);background:radial-gradient(var(--accent) 40%, transparent 44%);}

  .verify-box{text-align:center;padding:10px 0 20px;}
  .verify-box .big-ico{font-size:44px;margin-bottom:14px;}
  .verify-box p{font-size:13px;color:var(--sub);margin-bottom:18px;}
  .code-boxes{display:flex;gap:8px;justify-content:center;margin-bottom:16px;}
  .code-boxes input{
    width:42px;height:50px;text-align:center;font-size:18px;font-weight:800;
    background:var(--card);border:1px solid var(--line);color:var(--text);border-radius:10px;
  }
  .resend{font-size:12px;color:var(--accent2);font-weight:700;}

  .gd-hero{
    height:140px;border-radius:16px;display:flex;align-items:center;justify-content:center;
    font-size:52px;margin-bottom:16px;border:1px solid var(--line);
  }
  .gd-note{font-size:12px;color:var(--sub);margin-bottom:14px;}
  .gd-step-head{display:flex;align-items:center;gap:10px;margin:4px 0 12px;}
  .gd-step-head .num{
    flex:0 0 auto;width:26px;height:26px;border-radius:8px;background:rgba(186,255,41,0.12);
    color:var(--accent);font-weight:800;font-size:12.5px;display:flex;align-items:center;justify-content:center;
  }
  .gd-step-head h4{font-size:14px;font-weight:800;}
  .gd-id-box{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:14px;margin-bottom:20px;}
  .gd-id-row{display:flex;gap:8px;}
  .gd-id-row input{
    flex:1;background:var(--bg2);border:1px solid var(--line);color:var(--text);
    border-radius:9px;padding:11px 12px;font-size:13.5px;
  }
  .gd-id-row input:focus{outline:none;border-color:var(--accent);}
  .gd-id-row button{
    background:var(--accent2);color:#04241f;border:none;border-radius:9px;
    padding:0 16px;font-weight:800;font-size:12.5px;white-space:nowrap;
  }
  .gd-delivery{display:inline-flex;align-items:center;gap:6px;margin-top:10px;font-size:11px;font-weight:800;color:var(--accent2);}

  .legal-intro{font-size:12.5px;line-height:1.6;color:var(--sub);margin-bottom:16px;}
  .legal-toc{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:14px 16px;margin-bottom:16px;}
  .legal-toc h4{font-size:13px;font-weight:800;margin-bottom:8px;}
  .legal-toc ol{margin:0 0 0 18px;padding:0;}
  .legal-toc li{font-size:12.5px;color:var(--sub);line-height:1.8;}
  .legal-block{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:16px;margin-bottom:12px;}
  .legal-block h4{font-size:13.5px;font-weight:800;margin-bottom:8px;color:var(--accent);}
  .legal-block p{font-size:12.5px;line-height:1.65;color:var(--sub);margin-bottom:6px;}
  .legal-block p:last-child{margin-bottom:0;}
  .legal-block ul{margin:6px 0 2px 18px;padding:0;}
  .legal-block li{font-size:12.5px;line-height:1.65;color:var(--sub);margin-bottom:4px;}

  .summary-row{display:flex;justify-content:space-between;align-items:center;font-size:13px;color:var(--sub);padding:8px 0;border-bottom:1px solid var(--line);}
  .summary-row:last-child{border-bottom:none;}
  .summary-row span:last-child{font-weight:800;color:var(--text);}
  .summary-row.total{padding-top:10px;}
  .summary-row.total span{font-size:14px;}
  .summary-row.total span:last-child{color:var(--accent);font-size:15.5px;}
  .package-item{
    display:flex;align-items:center;justify-content:space-between;background:var(--card);
    border:1px solid var(--line);border-radius:12px;padding:14px;margin-bottom:10px;position:relative;
  }
  .package-item .discount-badge{
    position:absolute;top:-8px;left:12px;background:var(--danger);color:#fff;
    font-size:10px;font-weight:800;padding:3px 8px;border-radius:7px;letter-spacing:0.2px;
  }
  .package-item .pi-left{display:flex;align-items:center;gap:10px;min-width:0;}
  .package-item .pi-icon{
    flex:0 0 auto;width:36px;height:36px;border-radius:10px;background:rgba(186,255,41,0.10);
    display:flex;align-items:center;justify-content:center;font-size:17px;
  }
  .package-item .pi-text{min-width:0;}
  .package-item .lbl{font-size:13.5px;font-weight:700;}
  .package-item .bonus{font-size:11px;color:var(--accent2);font-weight:700;margin-top:2px;}
  .package-item .desc{font-size:11px;color:var(--sub);margin-top:2px;}
  .package-item .pr{display:flex;align-items:center;gap:10px;flex:0 0 auto;}
  .package-item .price{font-size:14px;font-weight:800;color:var(--accent);text-align:right;}
  .package-item .price .old{display:block;font-size:10.5px;color:var(--sub);font-weight:600;text-decoration:line-through;}
  .gd-subhead{
    font-size:12px;font-weight:800;color:var(--sub);text-transform:uppercase;
    letter-spacing:0.6px;margin:18px 0 10px;
  }

  .devnote{
    margin:16px 0;padding:12px 14px;border:1px dashed rgba(186,255,41,0.4);
    border-radius:12px;background:rgba(186,255,41,0.05);font-size:11.5px;color:var(--sub);line-height:1.5;
  }
  .devnote b{color:var(--accent);}

  .tabbar{
    position:fixed;bottom:0;left:0;right:0;background:var(--bg2);
    border-top:1px solid var(--line);display:flex;padding:8px 6px 12px;z-index:50;
  }
  .tab{flex:1;text-align:center;font-size:10px;color:var(--sub);font-weight:600;background:none;border:none;}
  .tab .ico{font-size:18px;display:block;margin-bottom:2px;}
  .tab.active{color:var(--accent);}
</style>
</head>
<body>

<header>
  <div class="logo"><span class="dot"></span>NexUp</div>
  <div class="header-icons">
    <div class="balance-badge" id="balance-badge" onclick="showScreen('deposit')">💰 0 G</div>
    <div class="icon-btn" onclick="showScreen('notifications')">🔔<span class="icon-badge">2</span></div>
    <div class="icon-btn">🛒<span class="icon-badge danger">3</span></div>
  </div>
</header>

<!-- ============ HOME SCREEN ============ -->
<div class="screen active" id="screen-home">

  <div class="search-wrap">
    <div class="search-box">🔍 &nbsp;Chèche yon jwèt oswa yon kat...</div>
  </div>

  <div class="slider" id="slider">
    <div class="slide active" style="background:linear-gradient(135deg,#2c1e57,#1b1440);">
      <div class="tag" style="color:var(--accent);">Pwomosyon</div>
      <h3>-20% sou tout Diamond Free Fire</h3>
      <p>Jiska dimanch sa a — kòd la rive nan segond.</p>
    </div>
    <div class="slide" style="background:linear-gradient(135deg,#1e3a57,#122238);">
      <div class="tag" style="color:var(--accent2);">Nouvo</div>
      <h3>Blood Strike ak Delta Force disponib</h3>
      <p>Achte k