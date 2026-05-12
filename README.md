<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>princexit_ | Creative Studio</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <style>
        :root {
            /* Minimal & Realistic Color Palette */
            --gold: #d4af37;
            --gold-hover: #e0bc48;
            --bg: #121212;
            --surface: #1e1e1e;
            --surface-hover: #2a2a2a;
            --border: rgba(255, 255, 255, 0.06);
            --text: #eaeaea;
            --dim: #8a8a8a;
            --radius: 12px;
            --transition: 0.25s cubic-bezier(0.4, 0, 0.2, 1);
        }
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Segoe UI', 'Inter', -apple-system, BlinkMacSystemFont, system-ui, sans-serif;
            background: var(--bg); color: var(--text); min-height: 100vh; line-height: 1.6;
            -webkit-tap-highlight-color: transparent; overflow-x: hidden;
            letter-spacing: 0.2px;
        }
        body.no-scroll { overflow: hidden; touch-action: none; }
        .toast-container { position: fixed; top: 20px; right: 20px; z-index: 10000; display: flex; flex-direction: column; gap: 10px; pointer-events: none; }
        .toast { padding: 14px 20px; border-radius: 8px; color: #fff; font-weight: 500; font-size: 0.9rem; background: #222; backdrop-filter: blur(10px); animation: toastIn 0.4s ease forwards; box-shadow: 0 4px 15px rgba(0,0,0,0.3); max-width: 350px; border-left: 3px solid var(--gold); pointer-events: auto; }
        .toast.success { border-left-color: #2ecc71; }
        .toast.error { border-left-color: #e74c3c; }
        @keyframes toastIn { from { transform: translateX(120%); opacity: 0; } to { transform: translateX(0); opacity: 1; } }
        
        .navbar { position: sticky; top: 0; z-index: 500; background: rgba(18, 18, 18, 0.85); backdrop-filter: saturate(180%) blur(20px); -webkit-backdrop-filter: saturate(180%) blur(20px); padding: 1rem 2rem; display: flex; align-items: center; justify-content: space-between; border-bottom: 1px solid var(--border); }
        .nav-logo { font-size: 1.3rem; font-weight: 700; color: var(--gold); cursor: pointer; letter-spacing: -0.5px; }
        .nav-links { display: flex; gap: 0.8rem; list-style: none; align-items: center; }
        .nav-links a { color: var(--dim); text-decoration: none; padding: 0.5rem 1rem; border-radius: 20px; cursor: pointer; font-size: 0.9rem; font-weight: 500; transition: var(--transition); }
        .nav-links a:hover, .nav-links a.active { color: #fff; background: rgba(255,255,255,0.06); }
        .nav-right { display: flex; align-items: center; gap: 12px; position: relative; }
        .nav-btn { padding: 0.55rem 1.2rem; border-radius: 20px; border: 1px solid var(--border); background: transparent; color: #fff; cursor: pointer; font-size: 0.85rem; font-weight: 500; transition: var(--transition); white-space: nowrap; }
        .nav-btn:hover { background: rgba(255,255,255,0.05); }
        .nav-btn.primary { background: var(--gold); border: none; color: #111; font-weight: 600; }
        .nav-btn.primary:hover { background: var(--gold-hover); }
        
        .profile-chip { display: flex; align-items: center; gap: 8px; background: rgba(255,255,255,0.05); padding: 0.4rem 1rem; border-radius: 20px; cursor: pointer; border: 1px solid var(--border); transition: var(--transition); }
        .profile-chip:hover { background: rgba(255,255,255,0.1); }
        .profile-chip span { color: var(--gold); font-size: 0.85rem; font-weight: 500; max-width: 120px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
        .profile-dropdown { position: absolute; top: 50px; right: 0; background: #1e1e1e; border-radius: 12px; padding: 0.5rem; border: 1px solid var(--border); z-index: 60; display: none; min-width: 180px; box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
        .profile-dropdown.show { display: block; animation: dropIn 0.2s ease; }
        @keyframes dropIn { from { opacity: 0; transform: translateY(-10px); } to { opacity: 1; transform: translateY(0); } }
        .profile-dropdown a { display: block; padding: 0.7rem 1rem; color: var(--dim); text-decoration: none; border-radius: 8px; cursor: pointer; font-size: 0.85rem; transition: var(--transition); }
        .profile-dropdown a:hover { background: rgba(255,255,255,0.05); color: #fff; }
        
        .hamburger { display: none; background: none; border: none; flex-direction: column; gap: 5px; cursor: pointer; padding: 5px; }
        .hamburger span { width: 22px; height: 2px; background: #fff; display: block; border-radius: 2px; transition: var(--transition); }
        .mobile-menu { position: fixed; top: 0; right: -300px; width: 280px; height: 100vh; background: rgba(18,18,18,0.98); backdrop-filter: blur(20px); z-index: 600; padding: 5rem 1.5rem 2rem; transition: right 0.4s ease; border-left: 1px solid var(--border); }
        .mobile-menu.open { right: 0; }
        .mobile-menu a { display: block; color: var(--dim); padding: 1rem; text-decoration: none; border-radius: 12px; cursor: pointer; font-weight: 500; }
        .mobile-divider { border: none; border-top: 1px solid var(--border); margin: 1rem 0; }
        
        .overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.6); z-index: 550; display: none; backdrop-filter: blur(4px); }
        .overlay.show { display: block; }
        .main-content { padding: 2.5rem 2rem; max-width: 1200px; margin: 0 auto; min-height: 80vh; }
        .page { display: none; animation: pageFade 0.35s ease forwards; }
        .page.show { display: block; }
        @keyframes pageFade { from { opacity: 0; transform: translateY(12px); } to { opacity: 1; transform: translateY(0); } }
        
        .hero-section { text-align: center; padding: 4rem 0 2rem; }
        .hero-title { font-size: 3rem; color: var(--gold); font-weight: 800; letter-spacing: -1px; margin-bottom: 0.5rem; }
        .hero-subtitle { color: var(--dim); font-size: 1.1rem; font-weight: 400; }
        
        .live-section { margin: 2rem auto; max-width: 900px; padding: 1.5rem; background: var(--surface); border-radius: var(--radius); border: 1px solid var(--border); position: relative; box-shadow: 0 4px 20px rgba(0,0,0,0.2); }
        .live-badge { background: #e74c3c; color: #fff; padding: 0.35rem 0.9rem; border-radius: 20px; font-size: 0.75rem; font-weight: 600; animation: pulse 2s infinite; display: inline-flex; align-items: center; gap: 6px; }
        .live-badge.offline { background: #333; color: #888; animation: none; }
        @keyframes pulse { 0% { box-shadow: 0 0 0 0 rgba(231,76,60,0.4); } 70% { box-shadow: 0 0 0 8px rgba(231,76,60,0); } 100% { box-shadow: 0 0 0 0 rgba(231,76,60,0); } }
        
        .live-video-container { width: 100%; aspect-ratio: 16/9; background: #000; border-radius: 8px; overflow: hidden; position: relative; border: 1px solid var(--border); margin-top: 1rem; }
        .live-video-container iframe, .live-video-container video { width: 100%; height: 100%; border: none; }
        .coming-soon-overlay { position: absolute; inset: 0; display: flex; align-items: center; justify-content: center; background: #050505; flex-direction: column; gap: 15px; z-index: 2; }
        .coming-soon-overlay i { font-size: 2.5rem; color: #444; }
        .coming-soon-overlay h3 { color: #666; letter-spacing: 2px; font-weight: 500; font-size: 0.9rem;}
        
        .live-buttons { position: absolute; top: 20px; right: 20px; display: flex; gap: 8px; z-index: 5; flex-wrap: wrap; }
        .live-buttons button { font-size: 0.75rem; padding: 0.4rem 1rem; border-radius: 20px; border: 1px solid var(--border); background: rgba(0,0,0,0.6); backdrop-filter: blur(5px); color: #fff; cursor: pointer; transition: var(--transition); }
        .live-buttons button:hover { background: rgba(255,255,255,0.15); border-color: rgba(255,255,255,0.3); }
        
        .quick-links { display: flex; justify-content: center; gap: 1.5rem; margin-top: 3.5rem; flex-wrap: wrap; }
        .quick-link-card { background: var(--surface); border: 1px solid var(--border); padding: 1.8rem 2.5rem; border-radius: var(--radius); cursor: pointer; transition: var(--transition); display: flex; flex-direction: column; align-items: center; gap: 12px; min-width: 160px; }
        .quick-link-card:hover { border-color: var(--gold); transform: translateY(-3px); background: var(--surface-hover); }
        .quick-link-card i { font-size: 1.8rem; color: var(--gold); }
        .quick-link-card span { font-weight: 500; color: #fff; }
        
        .section-title { font-size: 1.5rem; margin-bottom: 1.5rem; font-weight: 600; display: flex; align-items: center; gap: 10px; }
        .search-container { margin-bottom: 1.5rem; display: flex; align-items: center; background: var(--surface); border-radius: 30px; padding: 0.7rem 1.4rem; border: 1px solid var(--border); transition: var(--transition); }
        .search-container:focus-within { border-color: var(--gold); background: #222; }
        .search-container i { color: var(--dim); margin-right: 12px; }
        .search-container input { background: transparent; border: none; color: #fff; width: 100%; outline: none; font-size: 0.95rem; }
        
        .add-media-bar { display: flex; align-items: center; gap: 10px; margin-bottom: 1.5rem; flex-wrap: wrap; }
        .add-media-btn { display: inline-flex; align-items: center; gap: 6px; padding: 0.6rem 1.2rem; border-radius: 25px; background: var(--gold); color: #111; border: none; cursor: pointer; font-weight: 600; font-size: 0.85rem; transition: var(--transition); }
        .add-media-btn:hover { background: var(--gold-hover); transform: translateY(-2px); }
        .media-count-badge { font-size: 0.75rem; color: var(--dim); background: var(--surface); padding: 0.4rem 1rem; border-radius: 20px; border: 1px solid var(--border); font-weight: 500;}
        
        .gallery-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 1rem; }
        .gallery-item { position: relative; border-radius: 10px; overflow: hidden; cursor: pointer; background: var(--surface); aspect-ratio: 4/5; border: 1px solid var(--border); transition: var(--transition); }
        .gallery-item:hover { border-color: rgba(255,255,255,0.15); box-shadow: 0 5px 15px rgba(0,0,0,0.3); }
        .gallery-item img { width: 100%; height: 100%; object-fit: cover; transition: transform 0.5s ease; }
        .gallery-item:hover img { transform: scale(1.05); }
        .media-title { position: absolute; bottom: 0; left: 0; right: 0; background: linear-gradient(transparent, rgba(0,0,0,0.9)); color: #fff; padding: 30px 15px 15px; font-size: 0.85rem; font-weight: 500; z-index: 5; text-shadow: 0 2px 4px rgba(0,0,0,0.5); }
        
        .menu-btn, .delete-media-btn { position: absolute; top: 10px; width: 30px; height: 30px; border-radius: 50%; cursor: pointer; z-index: 10; display: flex; align-items: center; justify-content: center; border: 1px solid rgba(255,255,255,0.1); background: rgba(0,0,0,0.5); backdrop-filter: blur(5px); color: #fff; font-size: 0.8rem; transition: var(--transition); }
        .menu-btn:hover, .delete-media-btn:hover { background: rgba(0,0,0,0.8); }
        .menu-btn { right: 10px; }
        .delete-media-btn { left: 10px; background: rgba(231,76,60,0.6); }
        .delete-media-btn:hover { background: rgba(231,76,60,0.9); }
        
        .context-menu { position: absolute; top: 45px; right: 10px; background: #1e1e1e; border: 1px solid var(--border); border-radius: 10px; padding: 0.5rem 0; z-index: 20; min-width: 160px; display: none; box-shadow: 0 10px 25px rgba(0,0,0,0.5); }
        .context-menu.show { display: block; animation: dropIn 0.2s ease; }
        .context-menu button { display: block; width: 100%; text-align: left; padding: 0.7rem 1.2rem; background: none; border: none; color: #ccc; cursor: pointer; font-size: 0.85rem; display: flex; align-items: center; gap: 10px; transition: var(--transition); }
        .context-menu button:hover { background: rgba(255,255,255,0.05); color: var(--gold); }
        
        .lightbox { position: fixed; inset: 0; background: rgba(10,10,10,0.95); z-index: 3000; display: none; align-items: center; justify-content: center; flex-direction: column; backdrop-filter: blur(10px); }
        .lightbox.show { display: flex; }
        .lb-image-wrap { position: relative; display: flex; align-items: center; justify-content: center; width: 100%; height: 75vh; overflow: hidden; }
        .lightbox img { max-width: 90vw; max-height: 70vh; border-radius: 8px; object-fit: contain; box-shadow: 0 10px 40px rgba(0,0,0,0.5); }
        .lb-close-btn, .lb-download-btn { position: absolute; top: 20px; width: 40px; height: 40px; border-radius: 50%; border: none; color: #fff; cursor: pointer; z-index: 20; background: rgba(255,255,255,0.1); display: flex; align-items: center; justify-content: center; font-size: 1.1rem; transition: var(--transition); }
        .lb-close-btn:hover, .lb-download-btn:hover { background: rgba(255,255,255,0.2); }
        .lb-close-btn { right: 25px; }
        .lb-download-btn { right: 75px; }
        .lb-nav-btn { position: absolute; top: 50%; transform: translateY(-50%); background: rgba(255,255,255,0.05); border: 1px solid var(--border); color: #fff; font-size: 1.2rem; width: 40px; height: 40px; border-radius: 50%; cursor: pointer; z-index: 20; display: flex; align-items: center; justify-content: center; transition: var(--transition); }
        .lb-nav-btn:hover { background: rgba(255,255,255,0.15); }
        .lb-nav-prev { left: 20px; }
        .lb-nav-next { right: 20px; }
        .lb-counter-text { position: absolute; bottom: 85px; color: var(--dim); z-index: 20; font-size: 0.9rem; }
        .lb-action-bar button { padding: 0.6rem 1.3rem; border-radius: 25px; border: 1px solid var(--border); background: rgba(255,255,255,0.1); color: #fff; cursor: pointer; font-size: 0.85rem; display: flex; align-items: center; gap: 7px; transition: var(--transition); }
        .lb-action-bar button:hover { background: rgba(255,255,255,0.2); }
        
        .video-feed { display: flex; flex-direction: column; gap: 1rem; max-width: 900px; margin: 0 auto; }
        .video-card-yt { display: flex; gap: 1rem; background: var(--surface); border-radius: 12px; overflow: visible; border: 1px solid var(--border); transition: var(--transition); align-items: stretch; }
        .video-card-yt:hover { border-color: rgba(255,255,255,0.1); background: var(--surface-hover); }
        .video-thumb-yt { width: 220px; min-width: 220px; aspect-ratio: 16/9; background: #050505; position: relative; flex-shrink: 0; border-right: 1px solid var(--border); overflow: hidden; cursor: pointer; border-radius: 12px 0 0 12px; }
        .video-thumb-yt iframe, .video-thumb-yt video { width: 100%; height: 100%; border: none; object-fit: cover; }
        .video-info-yt { padding: 1.2rem 1.2rem 1.2rem 0; display: flex; align-items: center; flex: 1; min-width: 0; position: relative; }
        .video-info-yt h3 { font-size: 0.95rem; font-weight: 500; color: #fff; margin: 0; padding-right: 36px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; flex: 1; }
        .video-menu-dot { position: absolute; top: 12px; right: 12px; width: 30px; height: 30px; border-radius: 50%; background: transparent; border: none; color: var(--dim); cursor: pointer; font-size: 1rem; display: flex; align-items: center; justify-content: center; z-index: 10; transition: var(--transition); }
        .video-menu-dot:hover { background: rgba(255,255,255,0.05); color: #fff; }
        
        .doc-list { display: flex; flex-direction: column; gap: 0.8rem; }
        .doc-item { background: var(--surface); border: 1px solid var(--border); padding: 1rem 1.5rem; border-radius: 12px; display: flex; align-items: center; justify-content: space-between; transition: var(--transition); }
        .doc-item:hover { border-color: rgba(255,255,255,0.1); background: var(--surface-hover); }
        .doc-info { display: flex; align-items: center; gap: 12px; flex: 1; min-width: 0; }
        .doc-info i { font-size: 1.5rem; color: #e74c3c; }
        .doc-info span { font-weight: 500; font-size: 0.95rem; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .doc-actions-group { display: flex; gap: 8px; }
        .doc-actions-group button { padding: 0.5rem 1rem; border-radius: 20px; border: 1px solid var(--border); background: transparent; color: var(--dim); cursor: pointer; font-size: 0.8rem; transition: var(--transition); }
        .doc-actions-group button:hover { background: rgba(255,255,255,0.05); color: #fff; }
        .doc-actions-group button.primary { background: var(--gold); border: none; color: #111; font-weight: 600; }
        .doc-actions-group button.primary:hover { background: var(--gold-hover); color: #111; }
        
        .doc-lightbox-full { position: fixed; inset: 0; background: #0a0a0a; z-index: 3500; display: none; }
        .doc-lightbox-full.show { display: block; }
        .doc-header { position: absolute; top: 0; left: 0; right: 0; padding: 1rem 2rem; background: linear-gradient(to bottom, rgba(0,0,0,0.9), transparent); display: flex; justify-content: space-between; align-items: center; }
        .doc-content { width: 100%; height: 100vh; border: none; }
        
        .modal-backdrop { position: fixed; inset: 0; background: rgba(0,0,0,0.7); z-index: 5000; display: none; align-items: center; justify-content: center; backdrop-filter: blur(8px); }
        .modal-backdrop.show { display: flex; }
        .modal-dialog { background: var(--surface); border-radius: 16px; padding: 2.2rem; width: 90%; max-width: 400px; border: 1px solid var(--border); position: relative; box-shadow: 0 20px 50px rgba(0,0,0,0.5); }
        .modal-dialog h2 { color: #fff; font-size: 1.4rem; text-align: center; margin-bottom: 1.5rem; font-weight: 600; }
        .modal-dialog label { font-size: 0.85rem; color: var(--dim); margin-bottom: 4px; display: block; margin-top: 10px; }
        .modal-dialog input, .modal-dialog textarea, .modal-dialog select { width: 100%; padding: 0.9rem 1rem; margin: 0.4rem 0; border-radius: 10px; border: 1px solid var(--border); background: var(--bg); color: #fff; outline: none; font-size: 0.95rem; transition: var(--transition); }
        .modal-dialog input:focus, .modal-dialog textarea:focus { border-color: var(--gold); }
        .modal-dialog .modal-submit { width: 100%; padding: 0.9rem; margin-top: 1.5rem; border-radius: 10px; border: none; background: var(--gold); color: #111; font-weight: 600; cursor: pointer; transition: var(--transition); font-size: 0.95rem; }
        .modal-dialog .modal-submit:hover { background: var(--gold-hover); }
        .modal-close { position: absolute; top: 16px; right: 20px; background: none; border: none; color: var(--dim); font-size: 1.2rem; cursor: pointer; transition: var(--transition); }
        .modal-close:hover { color: #fff; }
        .modal-link { color: var(--gold); cursor: pointer; text-decoration: none; font-weight: 500; transition: var(--transition); }
        .modal-link:hover { color: var(--gold-hover); text-decoration: underline; }
        
        .hidden { display: none !important; }
        .tabs { display: flex; gap: 8px; margin-bottom: 1.2rem; background: var(--bg); padding: 4px; border-radius: 10px; border: 1px solid var(--border); }
        .tab-btn { flex: 1; padding: 0.6rem; border: none; background: transparent; color: var(--dim); border-radius: 8px; cursor: pointer; font-size: 0.85rem; font-weight: 500; transition: var(--transition); }
        .tab-btn.active { background: var(--surface); color: #fff; box-shadow: 0 2px 8px rgba(0,0,0,0.2); }
        
        @media (max-width: 768px) {
            .nav-links { display: none; }
            .hamburger { display: flex; }
            .main-content { padding: 1.5rem 1rem; }
            .video-card-yt { flex-direction: column; gap: 0; }
            .video-thumb-yt { width: 100%; min-width: unset; border-right: none; border-bottom: 1px solid var(--border); border-radius: 12px 12px 0 0; }
            .video-info-yt { padding: 1rem; }
            .video-info-yt h3 { padding-right: 30px; }
            .hero-title { font-size: 2.2rem; }
            .quick-links { gap: 1rem; }
            .quick-link-card { min-width: 140px; padding: 1.5rem; }
        }
    </style>
</head>
<body>
    <div class="toast-container" id="toastContainer"></div>
    <div class="overlay" id="mobileOverlay"></div>
    
    <div class="lightbox" id="lightbox">
        <button class="lb-download-btn" id="lbDownloadBtn"><i class="fas fa-download"></i></button>
        <button class="lb-close-btn" onclick="closeLB()">✕</button>
        <button class="lb-nav-btn lb-nav-prev" onclick="lbNav(-1)"><i class="fas fa-chevron-left"></i></button>
        <button class="lb-nav-btn lb-nav-next" onclick="lbNav(1)"><i class="fas fa-chevron-right"></i></button>
        <div class="lb-image-wrap" id="lbImageWrap"><img id="lbImage" src=""></div>
        <div class="lb-counter-text" id="lbCounter"></div>
        <div class="lb-action-bar"><button id="lbCopyBtn"><i class="fas fa-link"></i> Copy Link</button></div>
    </div>
    
    <div class="doc-lightbox-full" id="docFullLightbox">
        <div class="doc-header"><span class="doc-title" id="docFullTitle"></span><div><button class="nav-btn primary" id="docFullDownloadBtn" style="margin-right:10px;"><i class="fas fa-download"></i> Download</button><button class="modal-close" style="position:static;" onclick="closeDocFullLB()">✕</button></div></div>
        <iframe class="doc-content" id="docFullIframe"></iframe>
    </div>

    <nav class="navbar">
        <div class="nav-logo" onclick="navigateTo('home')">princexit_</div>
        <ul class="nav-links" id="desktopNavLinks">
            <li><a data-page="home" class="active" onclick="navigateTo('home')">Home</a></li>
            <li><a data-page="gallery" onclick="navigateTo('gallery')">Photos</a></li>
            <li><a data-page="videos" onclick="navigateTo('videos')">Videos</a></li>
            <li><a data-page="documents" onclick="navigateTo('documents')">Documents</a></li>
            <li><a data-page="about" onclick="navigateTo('about')">Contact</a></li>
        </ul>
        <div class="nav-right">
            <span id="desktopAuthBtns"><button class="nav-btn" onclick="showAuth('login')">Log In</button><button class="nav-btn primary" onclick="showAuth('signup')">Sign Up</button></span>
            <span class="profile-chip hidden" id="profileChip"><span id="profileEmailText"></span><i class="fas fa-chevron-down" style="font-size:0.7rem;"></i></span>
            <div class="profile-dropdown" id="profileDropdown"><a onclick="doLogout()"><i class="fas fa-sign-out-alt"></i> Logout</a></div>
            <button class="hamburger" id="hamburgerBtn"><span></span><span></span><span></span></button>
        </div>
    </nav>
    
    <div class="mobile-menu" id="mobileMenu">
        <a onclick="navigateTo('home')"><i class="fas fa-home fa-fw"></i> Home</a>
        <a onclick="navigateTo('gallery')"><i class="fas fa-image fa-fw"></i> Photos</a>
        <a onclick="navigateTo('videos')"><i class="fas fa-video fa-fw"></i> Videos</a>
        <a onclick="navigateTo('documents')"><i class="fas fa-file-alt fa-fw"></i> Documents</a>
        <a href="https://princexit470.github.io/Chatus/" target="_blank"><i class="fas fa-comment fa-fw"></i> ChatUs</a>
        <a href="https://princexit470.github.io/QR-studio/" target="_blank"><i class="fas fa-qrcode fa-fw"></i> QR Studio</a>
        <a onclick="navigateTo('about')"><i class="fas fa-info-circle fa-fw"></i> Contact</a>
        <hr class="mobile-divider">
        <div id="mobileLoggedOut"><a onclick="showAuth('login')"><i class="fas fa-sign-in-alt fa-fw"></i> Log In</a><a onclick="showAuth('signup')" style="color:var(--gold);"><i class="fas fa-user-plus fa-fw"></i> Sign Up</a></div>
        <div id="mobileLoggedIn" class="hidden"><a onclick="doLogout()"><i class="fas fa-sign-out-alt fa-fw"></i> Logout</a></div>
    </div>

    <div class="main-content">
        <div class="page show" id="page-home">
            <div class="hero-section"><h1 class="hero-title">princexit_</h1><p class="hero-subtitle">Photography • Cinematography • Creative Studio</p></div>
            <div class="live-section" id="liveSection">
                <div class="live-header"><span class="live-badge offline" id="liveBadge"><i class="fas fa-circle"></i> OFFLINE</span><h3 style="font-size:1.2rem;margin-top:10px;font-weight:600;">Live Broadcast</h3></div>
                <div class="live-video-container" id="liveVideoContainer"><div class="coming-soon-overlay" id="liveOverlay"><i class="fas fa-video-slash"></i><h3>STREAM OFFLINE</h3></div></div>
                <div class="live-buttons" id="liveAdminButtons" style="display:none;">
                    <button onclick="showLiveStreamModal()"><i class="fas fa-link"></i> Set URL</button>
                    <button onclick="showScheduleLiveModal()"><i class="fas fa-clock"></i> Schedule</button>
                    <button onclick="showLiveCameraModal()"><i class="fas fa-camera"></i> OBS Live</button>
                </div>
            </div>
            <div class="quick-links">
                <div class="quick-link-card" onclick="navigateTo('gallery')"><i class="fas fa-camera-retro"></i><span>Photos</span></div>
                <div class="quick-link-card" onclick="navigateTo('videos')"><i class="fas fa-film"></i><span>Videos</span></div>
                <div class="quick-link-card" onclick="navigateTo('documents')"><i class="fas fa-folder-open"></i><span>Documents</span></div>
            </div>
        </div>
        
        <div class="page" id="page-gallery">
            <h2 class="section-title"><i class="fas fa-images" style="color:var(--gold);"></i> Photos</h2>
            <div class="add-media-bar" id="photoAddBar" style="display:none;"><button class="add-media-btn" onclick="openAddMediaModal('photo')"><i class="fas fa-plus"></i> Upload Photo</button><span class="media-count-badge" id="photoCountBadge">0</span></div>
            <div class="search-container"><i class="fas fa-search"></i><input type="text" id="searchPhotos" placeholder="Search photos..." onkeyup="renderPhotos()"></div>
            <div class="gallery-grid" id="photoGrid"></div>
        </div>
        
        <div class="page" id="page-videos">
            <h2 class="section-title"><i class="fas fa-play-circle" style="color:var(--gold);"></i> Videos</h2>
            <div class="add-media-bar" id="videoAddBar" style="display:none;"><button class="add-media-btn" onclick="openAddMediaModal('video')"><i class="fas fa-plus"></i> Upload Video</button><span class="media-count-badge" id="videoCountBadge">0</span></div>
            <div class="search-container"><i class="fas fa-search"></i><input type="text" id="searchVideos" placeholder="Search videos..." onkeyup="renderVideos()"></div>
            <div class="video-feed" id="videoFeed"></div>
        </div>
        
        <div class="page" id="page-documents">
            <h2 class="section-title"><i class="fas fa-file-pdf" style="color:var(--gold);"></i> Documents</h2>
            <div class="add-media-bar" id="docAddBar" style="display:none;"><button class="add-media-btn" onclick="openAddMediaModal('doc')"><i class="fas fa-plus"></i> Upload Document</button><span class="media-count-badge" id="docCountBadge">0</span></div>
            <div class="search-container"><i class="fas fa-search"></i><input type="text" id="searchDocs" placeholder="Search documents..." onkeyup="renderDocs()"></div>
            <div class="doc-list" id="docList"></div>
        </div>
        
        <div class="page" id="page-about">
            <div style="text-align:center;padding:4rem 2rem;background:var(--surface);border-radius:var(--radius);max-width:600px;margin:2rem auto;border:1px solid var(--border);">
                <h2 style="color:var(--gold);margin-bottom:1rem;font-size:2rem;">Get in Touch</h2>
                <p style="color:var(--dim);margin-bottom:2rem;">Interested in working together? Drop an email or connect on socials.</p>
                <p style="font-weight:500;">princekvishwakarma@yahoo.com</p>
                <div style="margin-top:1.5rem;"><a href="https://instagram.com/princexit_" target="_blank" style="color:#fff;font-size:2.2rem;transition:var(--transition);display:inline-block;"><i class="fab fa-instagram"></i></a></div>
            </div>
        </div>
    </div>

    <div class="modal-backdrop" id="authModal">
        <div class="modal-dialog">
            <button class="modal-close" onclick="closeModal('authModal')">✕</button>
            <h2 id="authTitle">Welcome Back</h2>
            <input type="text" id="authName" placeholder="Full Name" style="display:none;">
            <input type="email" id="authEmail" placeholder="Email address">
            <input type="password" id="authPass" placeholder="Password">
            <input type="password" id="authConfirmPass" placeholder="Confirm Password" style="display:none;">
            <span id="forgotPassBtn" onclick="showAuth('reset')" style="display:block;text-align:right;margin:8px 0;font-size:0.85rem;color:var(--dim);cursor:pointer;transition:var(--transition);">Forgot Password?</span>
            <button class="modal-submit" id="authSubmit">Log In</button>
            <p style="text-align:center;margin-top:1.2rem;font-size:0.9rem;color:var(--dim);" id="authSwitch">New here? <span class="modal-link" onclick="showAuth('signup')">Create account</span></p>
        </div>
    </div>

    <div class="modal-backdrop" id="addMediaModal">
        <div class="modal-dialog">
            <button class="modal-close" onclick="closeModal('addMediaModal')">✕</button>
            <h2 id="addMediaTitle">Add Media</h2>
            <div class="tabs" id="mediaTabs">
                <button class="tab-btn active" data-tab="upload">📁 Upload File</button>
                <button class="tab-btn" data-tab="link">🔗 Add URL</button>
            </div>
            
            <div id="mediaTabUpload">
                <label>Media Title *</label>
                <input type="text" id="addMediaNameUpload" placeholder="e.g., Sunset Portrait">
                <label>Select File</label>
                <input type="file" id="addMediaFile" style="padding:0.6rem;background:transparent;">
                <small id="fileTypeHint" style="color:var(--dim);font-size:0.8rem;display:block;margin-top:-5px;">Max size depends on Cloudinary plan</small>
                <div id="cameraPreview" style="margin-top:10px;"></div>
            </div>
            
            <div id="mediaTabLink" style="display:none;">
                <label>Media Title *</label>
                <input type="text" id="addMediaName" placeholder="e.g., Sunset Portrait">
                <label>Direct Link / YouTube URL</label>
                <textarea id="addMediaUrl" placeholder="Paste link here..." rows="3"></textarea>
                <label id="recordVideoLabel" style="display:none;margin-top:10px;">Or record instantly</label>
                <button type="button" id="recordFromCameraBtn" style="display:none;margin-top:5px;width:100%;" class="nav-btn" onclick="startCameraRecording()"><i class="fas fa-video"></i> Record Video</button>
            </div>
            
            <button class="modal-submit" id="addMediaSubmit">Upload Media</button>
            <input type="hidden" id="addMediaType" value="photo">
        </div>
    </div>

    <div class="modal-backdrop" id="liveStreamModal">
        <div class="modal-dialog">
            <button class="modal-close" onclick="closeModal('liveStreamModal')">✕</button>
            <h2>Set Stream URL</h2>
            <p style="color:var(--dim);text-align:center;margin-bottom:1.5rem;font-size:0.9rem;">Paste an embed link (YouTube Live, direct HLS, etc.)</p>
            <label>Stream URL</label>
            <input type="text" id="liveStreamUrl" placeholder="https://...">
            <button class="modal-submit" id="liveStreamSubmit">Broadcast Now</button>
            <button class="nav-btn" style="width:100%;margin-top:0.8rem;background:transparent;color:var(--dim);border-color:transparent;" onclick="clearLiveStream()">Stop Broadcast</button>
        </div>
    </div>

    <div class="modal-backdrop" id="liveCameraModal">
        <div class="modal-dialog">
            <button class="modal-close" onclick="closeModal('liveCameraModal')">✕</button>
            <h2>OBS Studio Connect</h2>
            <p style="color:var(--dim);margin-bottom:1.5rem;font-size:0.9rem;text-align:center;">Copy these details into your OBS Streaming settings.</p>
            <label>RTMP Server URL</label>
            <input type="text" id="liveRtmpUrl" value="rtmp://live.cloudinary.com/streams" readonly onclick="this.select();document.execCommand('copy');TOAST('Copied!','success');">
            <label>Stream Key</label>
            <input type="text" id="liveStreamKey" value="T4e1jE08Epr7CNzf4tgjEL5o6Ks4Q4" readonly onclick="this.select();document.execCommand('copy');TOAST('Copied!','success');">
            <p style="font-size:0.8rem;color:var(--dim);margin-top:15px;text-align:center;">After starting OBS, click below to show player to users.</p>
            <button class="modal-submit" id="liveCameraGoLive">Show Stream on Website</button>
            <button class="nav-btn" style="width:100%;margin-top:0.8rem;background:transparent;color:var(--dim);border-color:transparent;" onclick="clearLiveStream()">Stop Broadcast</button>
        </div>
    </div>

    <div class="modal-backdrop" id="scheduleLiveModal">
        <div class="modal-dialog">
            <button class="modal-close" onclick="closeModal('scheduleLiveModal')">✕</button>
            <h2>Schedule Premiere</h2>
            <label>Event Title</label>
            <input type="text" id="scheduleTitle" placeholder="My Scheduled Event">
            
            <div class="tabs">
                <button class="tab-btn active" data-tab="scheduleExisting">Library</button>
                <button class="tab-btn" data-tab="scheduleUpload">Upload File</button>
            </div>
            
            <div id="scheduleExisting">
                <label>Select Video</label>
                <select id="scheduleVideoSelect" style="background:#121212;"></select>
            </div>
            <div id="scheduleUpload" style="display:none;">
                <label>Upload Premiere Video</label>
                <input type="file" id="scheduleVideoFile" accept="video/*" style="padding:0.6rem;background:transparent;">
            </div>
            
            <label>Scheduled Date & Time</label>
            <input type="datetime-local" id="scheduleDateTime">
            <label>Duration (minutes)</label>
            <input type="number" id="scheduleDuration" min="1" value="30" placeholder="30">
            
            <button class="modal-submit" id="scheduleLiveSubmit">Schedule Event</button>
            <button class="nav-btn" style="width:100%;margin-top:0.8rem;background:transparent;color:#e74c3c;border-color:transparent;" onclick="cancelSchedule()">Cancel All Schedules</button>
        </div>
    </div>

    <script>
        // ========== CONFIG ==========
        const SB = window.supabase.createClient('https://wvlvamuehbyfdsozjczk.supabase.co', 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Ind2bHZhbXVlaGJ5ZmRzb3pqY3prIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzU1NTM4MDAsImV4cCI6MjA5MTEyOTgwMH0.oaF4wymSu0ePwQSp3moV0sKZVgz5f50ILun5iaU816A');
        const ADMIN_EMAIL = "princekvishwakarma@yahoo.com";
        const CLOUDINARY_CLOUD_NAME = "dl4pbclvi";
        
        // --- FIX 1: UPDATE PRESET NAME HERE ---
        const CLOUDINARY_UPLOAD_PRESET = "princexit_upload"; 

        let USER = null, AUTH_MODE = 'login';
        let ALL_PHOTOS = [], ALL_VIDEOS = [], ALL_DOCS = [];

        function TOAST(m, t = 'info') {
            const b = document.getElementById('toastContainer');
            const d = document.createElement('div');
            d.className = 'toast ' + t;
            d.innerHTML = (t === 'success' ? '<i class="fas fa-check-circle" style="color:#2ecc71;margin-right:8px;"></i>' :
                          t === 'error' ? '<i class="fas fa-exclamation-circle" style="color:#e74c3c;margin-right:8px;"></i>' :
                          '<i class="fas fa-info-circle" style="color:#3498db;margin-right:8px;"></i>') + m;
            b.appendChild(d);
            setTimeout(() => { d.style.animation = 'toastIn 0.4s ease reverse forwards'; setTimeout(() => d.remove(), 400); }, 3500);
        }

        function isAdmin() { return USER && USER.email === ADMIN_EMAIL; }

        function updateAdminUI() {
            const admin = isAdmin();
            document.getElementById('photoAddBar').style.display = admin ? 'flex' : 'none';
            document.getElementById('videoAddBar').style.display = admin ? 'flex' : 'none';
            document.getElementById('docAddBar').style.display = admin ? 'flex' : 'none';
            document.getElementById('liveAdminButtons').style.display = admin ? 'flex' : 'none';
            if (document.getElementById('page-home').classList.contains('show')) populateScheduleVideoSelect();
            renderPhotos(); renderVideos(); renderDocs();
        }

        function extractDriveId(url) { const m = url.match(/\/d\/([a-zA-Z0-9_-]+)/) || url.match(/id=([a-zA-Z0-9_-]+)/); return m ? m[1] : null; }
        function isYouTube(url) { return /(youtube\.com|youtu\.be)/i.test(url); }
        function getYouTubeEmbed(url) { const m = url.match(/(?:v=|youtu\.be\/|embed\/|shorts\/)([a-zA-Z0-9_-]{11})/); return m ? `https://www.youtube.com/embed/${m[1]}` : url; }
        function isDirectVideoFile(url) { return /\.(mp4|webm|mov|avi|mkv|ogg|m3u8)(\?|$)/i.test(url); }

        function processMediaUrl(url, type) {
            const driveId = extractDriveId(url);
            if (driveId) return {
                displayUrl: type === 'photo' ? `https://drive.google.com/uc?export=view&id=${driveId}` : `https://drive.google.com/file/d/${driveId}/preview`,
                downloadUrl: `https://drive.google.com/uc?export=download&id=${driveId}`,
                originalLink: `https://drive.google.com/file/d/${driveId}/view`,
                isDrive: true, isDirectVideo: false
            };
            if (type === 'video' && isYouTube(url)) return { displayUrl: getYouTubeEmbed(url), downloadUrl: url, originalLink: url, isYouTube: true, isDirectVideo: false };
            if (type === 'video' && isDirectVideoFile(url)) return { displayUrl: url, downloadUrl: url, originalLink: url, isDirectVideo: true, isYouTube: false };
            return { displayUrl: url, downloadUrl: url, originalLink: url, isDirect: true, isDirectVideo: type === 'video' };
        }

        async function fetchAllMedia() {
            const { data, error } = await SB.from('media').select('*').order('created_at', { ascending: false });
            if (error) { TOAST('Error loading media: ' + error.message, 'error'); return []; }
            return data || [];
        }
        async function addMediaToDB(type, title, url) {
            const { data, error } = await SB.from('media').insert([{ type, title, url }]).select();
            if (error) { TOAST(error.message, 'error'); return null; }
            return data;
        }
        async function deleteMediaFromDB(id) {
            const { error } = await SB.from('media').delete().eq('id', id);
            if (error) { TOAST(error.message, 'error'); return false; }
            return true;
        }

        async function loadAllMediaFromDB() {
            const all = await fetchAllMedia();
            ALL_PHOTOS = []; ALL_VIDEOS = []; ALL_DOCS = [];
            all.forEach(item => {
                const p = processMediaUrl(item.url, item.type);
                const obj = { id: item.id, title: item.title, displayUrl: p.displayUrl, downloadUrl: p.downloadUrl, originalLink: p.originalLink, type: item.type, isYouTube: p.isYouTube || false, isDirectVideo: p.isDirectVideo || false };
                if (item.type === 'photo') ALL_PHOTOS.push(obj);
                else if (item.type === 'video') ALL_VIDEOS.push(obj);
                else if (item.type !== 'live') ALL_DOCS.push(obj);
            });
            updateCountBadges();
            renderPhotos(); renderVideos(); renderDocs();
        }
        function updateCountBadges() {
            document.getElementById('photoCountBadge').textContent = ALL_PHOTOS.length + ' item' + (ALL_PHOTOS.length !== 1 ? 's' : '');
            document.getElementById('videoCountBadge').textContent = ALL_VIDEOS.length + ' item' + (ALL_VIDEOS.length !== 1 ? 's' : '');
            document.getElementById('docCountBadge').textContent = ALL_DOCS.length + ' item' + (ALL_DOCS.length !== 1 ? 's' : '');
        }

        async function uploadToCloudinary(file) {
            const formData = new FormData();
            formData.append('file', file);
            formData.append('upload_preset', CLOUDINARY_UPLOAD_PRESET);
            formData.append('cloud_name', CLOUDINARY_CLOUD_NAME);
            
            TOAST('Uploading file... Please wait.', 'info');
            document.getElementById('addMediaSubmit').disabled = true;
            document.getElementById('addMediaSubmit').innerText = 'Uploading...';
            
            try {
                const response = await fetch(`https://api.cloudinary.com/v1_1/${CLOUDINARY_CLOUD_NAME}/auto/upload`, {
                    method: 'POST', body: formData
                });
                const result = await response.json();
                if (response.ok && result.secure_url) {
                    return result.secure_url;
                } else {
                    throw new Error(result.error?.message || 'Upload failed');
                }
            } catch (err) {
                TOAST('Cloudinary Error: ' + err.message, 'error');
                return null;
            } finally {
                document.getElementById('addMediaSubmit').disabled = false;
                document.getElementById('addMediaSubmit').innerText = 'Upload Media';
            }
        }

        // Add Media Modal
        function openAddMediaModal(type) {
            if (!isAdmin()) return TOAST('Access Denied', 'error');
            document.getElementById('addMediaType').value = type;
            document.getElementById('addMediaTitle').textContent = 'Add ' + { photo: 'Photo', video: 'Video', doc: 'Document' }[type];
            document.getElementById('addMediaName').value = '';
            document.getElementById('addMediaUrl').value = '';
            document.getElementById('addMediaFile').value = '';
            document.getElementById('addMediaNameUpload').value = '';
            document.getElementById('recordVideoLabel').style.display = 'none';
            document.getElementById('recordFromCameraBtn').style.display = 'none';
            document.getElementById('cameraPreview').innerHTML = '';
            
            // Reset to upload tab as default
            document.querySelectorAll('#mediaTabs .tab-btn').forEach(b => b.classList.remove('active'));
            document.querySelector('#mediaTabs .tab-btn[data-tab="upload"]').classList.add('active');
            document.getElementById('mediaTabUpload').style.display = 'block';
            document.getElementById('mediaTabLink').style.display = 'none';
            
            const fileInput = document.getElementById('addMediaFile');
            if (type === 'photo') fileInput.accept = 'image/*';
            else if (type === 'video') {
                fileInput.accept = 'video/*';
                document.getElementById('recordVideoLabel').style.display = 'block';
                document.getElementById('recordFromCameraBtn').style.display = 'inline-block';
            } else fileInput.accept = '.pdf,.doc,.docx,.txt,.csv,.xls,.xlsx,.ppt,.pptx,.zip,.rar';
            document.getElementById('addMediaModal').classList.add('show');
        }

        document.getElementById('mediaTabs').addEventListener('click', (e) => {
            if (!e.target.classList.contains('tab-btn')) return;
            const tab = e.target.dataset.tab;
            document.querySelectorAll('#mediaTabs .tab-btn').forEach(b => b.classList.remove('active'));
            e.target.classList.add('active');
            document.getElementById('mediaTabLink').style.display = tab === 'link' ? 'block' : 'none';
            document.getElementById('mediaTabUpload').style.display = tab === 'upload' ? 'block' : 'none';
        });

        let mediaRecorder, recordedChunks = [];
        async function startCameraRecording() {
            try {
                const stream = await navigator.mediaDevices.getUserMedia({ video: true, audio: true });
                mediaRecorder = new MediaRecorder(stream);
                recordedChunks = [];
                mediaRecorder.ondataavailable = e => { if (e.data.size > 0) recordedChunks.push(e.data); };
                mediaRecorder.onstop = async () => {
                    const blob = new Blob(recordedChunks, { type: 'video/webm' });
                    const file = new File([blob], 'recorded-video.webm', { type: 'video/webm' });
                    const url = await uploadToCloudinary(file);
                    if (url) {
                        document.getElementById('addMediaUrl').value = url;
                        TOAST('Recording uploaded successfully!', 'success');
                    }
                    stream.getTracks().forEach(t => t.stop());
                };
                mediaRecorder.start();
                TOAST('Recording started...', 'info');
                document.getElementById('recordFromCameraBtn').innerHTML = '<i class="fas fa-stop"></i> Stop Recording';
                document.getElementById('recordFromCameraBtn').onclick = () => {
                    mediaRecorder.stop();
                    document.getElementById('recordFromCameraBtn').innerHTML = '<i class="fas fa-video"></i> Record Video';
                    document.getElementById('recordFromCameraBtn').onclick = startCameraRecording;
                };
            } catch (err) {
                TOAST('Camera access denied or unavailable', 'error');
            }
        }

        document.getElementById('addMediaSubmit').onclick = async () => {
            const type = document.getElementById('addMediaType').value;
            let title, url;
            const activeTab = document.querySelector('#mediaTabs .tab-btn.active').dataset.tab;
            
            if (activeTab === 'link') {
                title = document.getElementById('addMediaName').value.trim();
                url = document.getElementById('addMediaUrl').value.trim();
                if (!title) return TOAST('Title is required', 'error');
                if (!url) return TOAST('URL is required', 'error');
            } else {
                title = document.getElementById('addMediaNameUpload').value.trim();
                const file = document.getElementById('addMediaFile').files[0];
                if (!title) return TOAST('Title is required', 'error');
                if (!file) return TOAST('Please select a file to upload', 'error');
                
                const uploadedUrl = await uploadToCloudinary(file);
                if (!uploadedUrl) return; // Error handled inside uploadToCloudinary
                url = uploadedUrl;
            }
            
            const res = await addMediaToDB(type, title, url);
            if (res) {
                TOAST('Media added successfully!', 'success');
                closeModal('addMediaModal');
                await loadAllMediaFromDB();
            }
        };

        // --- FIX 2: AUTH WITH FULL NAME & CONFIRM PASSWORD ---
        async function initAuth() { 
            const { data } = await SB.auth.getSession(); 
            updateUI(data.session ? data.session.user : null); 
            await loadAllMediaFromDB(); 
        }
        
        SB.auth.onAuthStateChange((event, session) => { 
            updateUI(session ? session.user : null); 
            if (session) loadAllMediaFromDB(); 
        });
        
        function updateUI(u) {
            USER = u; const li = !!u;
            document.getElementById('desktopAuthBtns').classList.toggle('hidden', li);
            document.getElementById('profileChip').classList.toggle('hidden', !li);
            document.getElementById('mobileLoggedOut').classList.toggle('hidden', li);
            document.getElementById('mobileLoggedIn').classList.toggle('hidden', !li);
            if (u) {
                // Try to display full name if available, else email prefix
                const displayName = u.user_metadata?.full_name || u.email.split('@')[0];
                document.getElementById('profileEmailText').textContent = displayName;
            }
            updateAdminUI();
            loadLiveStreamFromDB();
            checkScheduledLive();
        }
        
        function showAuth(mode) {
            AUTH_MODE = mode;
            const isSignup = mode === 'signup';
            
            document.getElementById('authName').style.display = isSignup ? 'block' : 'none';
            document.getElementById('authConfirmPass').style.display = isSignup ? 'block' : 'none';
            
            document.getElementById('authEmail').style.display = 'block';
            document.getElementById('authPass').style.display = mode === 'reset' ? 'none' : 'block';
            document.getElementById('forgotPassBtn').style.display = mode === 'login' ? 'block' : 'none';
            
            if (mode === 'login') {
                document.getElementById('authTitle').textContent = 'Welcome Back';
                document.getElementById('authSubmit').textContent = 'Log In';
                document.getElementById('authSwitch').innerHTML = 'New here? <span class="modal-link" onclick="showAuth(\'signup\')">Create account</span>';
            } else if (mode === 'signup') {
                document.getElementById('authTitle').textContent = 'Create Account';
                document.getElementById('authSubmit').textContent = 'Sign Up';
                document.getElementById('authSwitch').innerHTML = 'Have account? <span class="modal-link" onclick="showAuth(\'login\')">Log In</span>';
            } else if (mode === 'reset') {
                document.getElementById('authTitle').textContent = 'Reset Password';
                document.getElementById('authSubmit').textContent = 'Send Reset Link';
                document.getElementById('authSwitch').innerHTML = '<span class="modal-link" onclick="showAuth(\'login\')">Back to Login</span>';
            }
            document.getElementById('authModal').classList.add('show');
        }
        
        document.getElementById('authSubmit').onclick = async () => {
            const email = document.getElementById('authEmail').value.trim();
            const pass = document.getElementById('authPass').value.trim();
            const name = document.getElementById('authName').value.trim();
            const confirmPass = document.getElementById('authConfirmPass').value.trim();

            if (AUTH_MODE === 'reset') {
                if (!email) return TOAST('Enter email address', 'error');
                try {
                    const { error } = await SB.auth.resetPasswordForEmail(email);
                    if (error) throw error;
                    TOAST('Password reset link sent!', 'success'); 
                    closeModal('authModal');
                } catch(e) { TOAST(e.message, 'error'); }
                return;
            }

            if (AUTH_MODE === 'signup') {
                if (!name || !email || !pass || !confirmPass) return TOAST('Please fill all fields', 'error');
                if (pass !== confirmPass) return TOAST('Passwords do not match!', 'error');
            } else {
                if (!email || !pass) return TOAST('Please enter email and password', 'error');
            }

            try {
                let r;
                // Disable button during req
                document.getElementById('authSubmit').disabled = true;
                document.getElementById('authSubmit').innerText = 'Please wait...';
                
                if (AUTH_MODE === 'signup') {
                    // Supabase automatically handles duplicate emails if set in settings, throwing an error.
                    r = await SB.auth.signUp({ 
                        email, 
                        password: pass,
                        options: { data: { full_name: name } }
                    });
                } else {
                    r = await SB.auth.signInWithPassword({ email, password: pass });
                }
                
                if (r.error) throw r.error;
                // If signup requires email confirmation, the session might be null.
                if (AUTH_MODE === 'signup' && !r.data.session) {
                    TOAST('Verification email sent! Check your inbox.', 'success');
                } else {
                    TOAST(AUTH_MODE === 'signup' ? 'Account created & logged in!' : 'Logged in successfully!', 'success');
                    updateUI(r.data.user); 
                    await loadAllMediaFromDB();
                }
                closeModal('authModal'); 
            } catch (e) { 
                TOAST(e.message, 'error'); 
            } finally {
                document.getElementById('authSubmit').disabled = false;
                document.getElementById('authSubmit').innerText = AUTH_MODE === 'signup' ? 'Sign Up' : 'Log In';
            }
        };

        async function doLogout() { 
            await SB.auth.signOut(); 
            document.getElementById('profileDropdown').classList.remove('show'); 
            ALL_PHOTOS = []; ALL_VIDEOS = []; ALL_DOCS = []; 
            updateCountBadges(); renderPhotos(); renderVideos(); renderDocs(); 
            TOAST('Logged out successfully', 'info'); 
        }

        // Navigation
        function navigateTo(page, push = true) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('show'));
            const t = document.getElementById('page-' + page); if (t) t.classList.add('show');
            document.querySelectorAll('#desktopNavLinks a').forEach(a => a.classList.remove('active'));
            const link = document.querySelector(`a[data-page="${page}"]`); if (link) link.classList.add('active');
            if (push) history.pushState({ page }, "", "#" + page);
            document.getElementById('mobileMenu').classList.remove('open');
            document.getElementById('mobileOverlay').classList.remove('show');
            window.scrollTo({ top: 0, behavior: 'smooth' });
            updateAdminUI();
            if (page === 'home') checkScheduledLive();
        }

        // RENDER FUNCTIONS
        function renderPhotos() {
            const q = (document.getElementById('searchPhotos')?.value || '').toLowerCase();
            const filtered = ALL_PHOTOS.filter(p => (p.title || '').toLowerCase().includes(q));
            const grid = document.getElementById('photoGrid');
            if (!ALL_PHOTOS.length) { grid.innerHTML = '<div style="text-align:center;padding:4rem;color:var(--dim);">No photos found</div>'; return; }
            if (!filtered.length) { grid.innerHTML = '<div style="text-align:center;padding:2rem;color:var(--dim);">No results matching search</div>'; return; }
            const admin = isAdmin();
            grid.innerHTML = filtered.map((p, idx) => {
                const realIdx = ALL_PHOTOS.indexOf(p);
                return `
                <div class="gallery-item" onclick="openLB(${realIdx})">
                    <img src="${p.displayUrl}" loading="lazy" alt="${p.title}">
                    <div class="media-title">${p.title}</div>
                    <button class="menu-btn" onclick="toggleMenu(event,'pm${realIdx}')">⋮</button>
                    ${admin ? `<button class="delete-media-btn" onclick="event.stopPropagation();deleteMediaById('${p.id}')"><i class="fas fa-trash"></i></button>` : ''}
                    <div class="context-menu" id="pm${realIdx}">
                        <button onclick="event.stopPropagation();downloadMedia('${p.downloadUrl.replace(/'/g,"\\'")}','${p.title.replace(/'/g,"\\'")}')"><i class="fas fa-download"></i> Download</button>
                        <button onclick="event.stopPropagation();navigator.clipboard.writeText('${p.originalLink}');TOAST('Link copied','success')"><i class="fas fa-link"></i> Copy Link</button>
                    </div>
                </div>`;
            }).join('');
        }

        function renderVideos() {
            const q = (document.getElementById('searchVideos')?.value || '').toLowerCase();
            const filtered = ALL_VIDEOS.filter(v => (v.title || '').toLowerCase().includes(q));
            const feed = document.getElementById('videoFeed');
            if (!ALL_VIDEOS.length) { feed.innerHTML = '<div style="text-align:center;padding:4rem;color:var(--dim);">No videos found</div>'; return; }
            if (!filtered.length) { feed.innerHTML = '<div style="text-align:center;padding:2rem;color:var(--dim);">No results matching search</div>'; return; }
            const admin = isAdmin();
            feed.innerHTML = filtered.map((v, idx) => {
                const thumb = v.isDirectVideo
                    ? `<video src="${v.displayUrl}" preload="metadata" controls playsinline></video>`
                    : `<iframe src="${v.displayUrl}" allowfullscreen loading="lazy"></iframe>`;
                return `
                <div class="video-card-yt">
                    <div class="video-thumb-yt" onclick="${v.isDirectVideo ? '' : `window.open('${v.originalLink}','_blank')`}">${thumb}</div>
                    <div class="video-info-yt">
                        <h3>${v.title}</h3>
                        <button class="video-menu-dot" onclick="toggleMenu(event,'vm${idx}')">⋮</button>
                        <div class="context-menu" id="vm${idx}" style="top:40px;right:4px;">
                            ${admin ? `<button onclick="event.stopPropagation(); deleteMediaById('${v.id}')" style="color:#e74c3c;"><i class="fas fa-trash"></i> Delete</button>` : ''}
                        </div>
                    </div>
                </div>`;
            }).join('');
        }

        function renderDocs() {
            const q = (document.getElementById('searchDocs')?.value || '').toLowerCase();
            const filtered = ALL_DOCS.filter(d => (d.title || '').toLowerCase().includes(q));
            const list = document.getElementById('docList');
            if (!ALL_DOCS.length) { list.innerHTML = '<div style="text-align:center;padding:4rem;color:var(--dim);">No documents found</div>'; return; }
            if (!filtered.length) { list.innerHTML = '<div style="text-align:center;padding:2rem;color:var(--dim);">No results matching search</div>'; return; }
            const admin = isAdmin();
            list.innerHTML = filtered.map(d => {
                let icon = 'fa-file';
                if (d.title.toLowerCase().includes('pdf')) icon = 'fa-file-pdf';
                else if (d.title.toLowerCase().includes('doc')) icon = 'fa-file-word';
                return `
                <div class="doc-item">
                    <div class="doc-info"><i class="fas ${icon}"></i><span>${d.title}</span></div>
                    <div class="doc-actions-group">
                        <button class="primary" onclick="openDocFull('${d.displayUrl}','${d.title.replace(/'/g,"\\'")}')"><i class="fas fa-eye"></i> View</button>
                        <button onclick="downloadMedia('${d.downloadUrl.replace(/'/g,"\\'")}','${d.title.replace(/'/g,"\\'")}')"><i class="fas fa-download"></i></button>
                        ${admin ? `<button onclick="deleteMediaById('${d.id}')" style="color:#e74c3c;"><i class="fas fa-trash"></i></button>` : ''}
                    </div>
                </div>`;
            }).join('');
        }

        async function downloadMedia(url, filename) {
            try {
                const r = await fetch(url, { mode: 'cors' });
                if (!r.ok) throw new Error('fetch failed');
                const blob = await r.blob();
                const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = filename || 'download'; document.body.appendChild(a); a.click(); document.body.removeChild(a);
                TOAST('Download started!', 'success');
            } catch (e) {
                const a = document.createElement('a'); a.href = url; a.download = filename || ''; a.target = '_blank'; document.body.appendChild(a); a.click(); document.body.removeChild(a);
            }
        }
        
        async function deleteMediaById(id) { 
            if (!isAdmin()) return; 
            if (!confirm('Are you sure you want to permanently delete this?')) return; 
            const ok = await deleteMediaFromDB(id); 
            if (ok) { TOAST('Item deleted', 'success'); await loadAllMediaFromDB(); } 
        }

        function closeModal(id) { document.getElementById(id).classList.remove('show'); }

        // LIGHTBOX
        let LB_IDX = 0, touchStartX = 0, touchStartY = 0;
        function openLB(idx) { if (!ALL_PHOTOS.length) return; LB_IDX = idx; updateLB(); document.getElementById('lightbox').classList.add('show'); document.body.classList.add('no-scroll'); }
        function closeLB() { document.getElementById('lightbox').classList.remove('show'); document.body.classList.remove('no-scroll'); }
        function updateLB() { const p = ALL_PHOTOS[LB_IDX]; if (!p) return; document.getElementById('lbImage').src = p.displayUrl; document.getElementById('lbCounter').textContent = `${LB_IDX+1} / ${ALL_PHOTOS.length} - ${p.title}`; }
        function lbNav(dir) { if (ALL_PHOTOS.length <= 1) return; LB_IDX = (LB_IDX + dir + ALL_PHOTOS.length) % ALL_PHOTOS.length; updateLB(); }
        document.getElementById('lbDownloadBtn').onclick = () => { const p = ALL_PHOTOS[LB_IDX]; if (p) downloadMedia(p.downloadUrl, p.title); };
        document.getElementById('lbCopyBtn').onclick = () => { const p = ALL_PHOTOS[LB_IDX]; if (p) { navigator.clipboard.writeText(p.originalLink); TOAST('Link copied', 'success'); } };

        const lightbox = document.getElementById('lightbox');
        lightbox.addEventListener('touchstart', (e) => { touchStartX = e.touches[0].clientX; touchStartY = e.touches[0].clientY; }, {passive:true});
        lightbox.addEventListener('touchend', (e) => {
            const dx = e.changedTouches[0].clientX - touchStartX;
            const dy = e.changedTouches[0].clientY - touchStartY;
            if (Math.abs(dx) > Math.abs(dy) && Math.abs(dx) > 50) lbNav(dx > 0 ? -1 : 1);
            else if (dy > 100 && Math.abs(dx) < 30) closeLB();
        });

        // DOC VIEWER
        function openDocFull(url, title) { document.getElementById('docFullTitle').textContent = title; document.getElementById('docFullIframe').src = url; document.getElementById('docFullLightbox').classList.add('show'); document.body.classList.add('no-scroll'); document.getElementById('docFullDownloadBtn').onclick = () => downloadMedia(url, title); }
        function closeDocFullLB() { document.getElementById('docFullLightbox').classList.remove('show'); document.body.classList.remove('no-scroll'); document.getElementById('docFullIframe').src = ''; }

        // MENUS
        function toggleMenu(e, id) { e.stopPropagation(); document.querySelectorAll('.context-menu').forEach(m => m.classList.remove('show')); const menu = document.getElementById(id); if (menu) menu.classList.add('show'); }
        document.addEventListener('click', e => {
            if (!e.target.closest('#profileChip') && !e.target.closest('#profileDropdown')) document.getElementById('profileDropdown').classList.remove('show');
            if (!e.target.closest('.menu-btn') && !e.target.closest('.video-menu-dot') && !e.target.closest('.context-menu')) document.querySelectorAll('.context-menu').forEach(m => m.classList.remove('show'));
            if (e.target.closest('#profileChip')) document.getElementById('profileDropdown').classList.toggle('show');
        });

        // MOBILE MENU
        document.getElementById('hamburgerBtn').onclick = () => { document.getElementById('mobileMenu').classList.add('open'); document.getElementById('mobileOverlay').classList.add('show'); };
        document.getElementById('mobileOverlay').onclick = () => { document.getElementById('mobileMenu').classList.remove('open'); document.getElementById('mobileOverlay').classList.remove('show'); };

        // ========== LIVE STREAM ==========
        async function loadLiveStreamFromDB() {
            const { data, error } = await SB.from('media').select('*').eq('type', 'live').order('created_at', { ascending: false }).limit(1);
            if (error) { console.warn('Live fetch error:', error); return; }
            const url = data && data.length ? data[0].url : null;
            updateLiveStreamUI(url);
        }
        
        function updateLiveStreamUI(url) {
            const badge = document.getElementById('liveBadge');
            const overlay = document.getElementById('liveOverlay');
            const container = document.getElementById('liveVideoContainer');
            container.querySelectorAll('iframe, video').forEach(el => el.remove());
            if (url) {
                badge.classList.remove('offline');
                badge.innerHTML = '<i class="fas fa-circle"></i> LIVE NOW';
                overlay.style.display = 'none';
                
                if (url.includes('youtube.com') || url.includes('youtu.be')) {
                    const ytUrl = getYouTubeEmbed(url);
                    const iframe = document.createElement('iframe');
                    iframe.src = ytUrl + (ytUrl.includes('?') ? '&' : '?') + 'autoplay=1&controls=1&modestbranding=1';
                    iframe.allowFullscreen = true;
                    container.appendChild(iframe);
                } else if (url.includes('cloudinary.com') || url.includes('hls')) {
                    const iframe = document.createElement('iframe');
                    iframe.src = url;
                    iframe.allowFullscreen = true;
                    container.appendChild(iframe);
                } else if (isDirectVideoFile(url)) {
                    const video = document.createElement('video');
                    video.src = url; video.controls = true; video.autoplay = true; video.playsInline = true;
                    container.appendChild(video);
                } else {
                    const iframe = document.createElement('iframe'); iframe.src = url; iframe.allowFullscreen = true; container.appendChild(iframe);
                }
            } else {
                badge.classList.add('offline');
                badge.innerHTML = '<i class="fas fa-circle"></i> OFFLINE';
                overlay.style.display = 'flex';
            }
        }
        
        function showLiveStreamModal() { if (!isAdmin()) return; document.getElementById('liveStreamModal').classList.add('show'); }
        
        document.getElementById('liveStreamSubmit').onclick = async () => {
            const url = document.getElementById('liveStreamUrl').value.trim();
            if (!url) return TOAST('Please enter a stream URL', 'error');
            await SB.from('media').delete().eq('type', 'live');
            const { error } = await SB.from('media').insert([{ type: 'live', title: 'live', url }]);
            if (error) { TOAST('Failed: ' + error.message, 'error'); return; }
            TOAST('Live stream is now active!', 'success');
            closeModal('liveStreamModal');
            loadLiveStreamFromDB();
        };
        
        function clearLiveStream() {
            if (!isAdmin()) return;
            SB.from('media').delete().eq('type', 'live').then(() => {
                TOAST('Broadcast ended', 'info');
                closeModal('liveStreamModal');
                closeModal('liveCameraModal');
                updateLiveStreamUI(null);
            });
        }

        // Camera Live Modal (Cloudinary RTMP)
        function showLiveCameraModal() {
            if (!isAdmin()) return;
            document.getElementById('liveCameraModal').classList.add('show');
        }
        document.getElementById('liveCameraGoLive').onclick = async () => {
            const hlsPlayerLink = 'https://player.cloudinary.com/embed/?cloud_name=dl4pbclvi&public_id=live_stream_f1e3551f3179487a9bc883505c9c2518_hls&profile=cld-live-streaming';
            await SB.from('media').delete().eq('type', 'live');
            const { error } = await SB.from('media').insert([{ type: 'live', title: 'live', url: hlsPlayerLink }]);
            if (error) { TOAST('Failed: ' + error.message, 'error'); return; }
            TOAST('HLS player connected! Start your OBS stream.', 'success');
            closeModal('liveCameraModal');
            loadLiveStreamFromDB();
        };

        // ========== SCHEDULED LIVE ==========
        // FIX 3: Catching schema errors silently for smooth UI if table isn't created yet
        async function checkScheduledLive() {
            try {
                const now = new Date().toISOString();
                const { data, error } = await SB.from('live_schedule')
                    .select('*')
                    .lte('scheduled_at', now)
                    .order('scheduled_at', { ascending: false })
                    .limit(1);
                    
                if (error) {
                    if (error.code === 'PGRST205') {
                        // Silent fail for missing table - user notified in admin portal
                        loadLiveStreamFromDB(); return;
                    }
                    console.error('Schedule check error', error); 
                    loadLiveStreamFromDB(); return; 
                }
                
                if (!data || !data.length) { loadLiveStreamFromDB(); return; }
                const schedule = data[0];
                const start = new Date(schedule.scheduled_at).getTime();
                const end = start + (schedule.duration_minutes || 30) * 60000;
                
                if (new Date().getTime() <= end) {
                    const videoUrl = schedule.video_url;
                    updateLiveStreamUI(videoUrl);
                    const badge = document.getElementById('liveBadge');
                    badge.innerHTML = '<i class="fas fa-circle"></i> PREMIERE: ' + schedule.title;
                } else {
                    await SB.from('live_schedule').delete().eq('id', schedule.id);
                    loadLiveStreamFromDB();
                }
            } catch (err) {
                loadLiveStreamFromDB();
            }
        }

        function populateScheduleVideoSelect() {
            const select = document.getElementById('scheduleVideoSelect');
            select.innerHTML = ALL_VIDEOS.map(v => `<option value="${v.displayUrl}">${v.title}</option>`).join('');
            if (!ALL_VIDEOS.length) select.innerHTML = '<option value="">No videos available</option>';
        }

        function showScheduleLiveModal() {
            if (!isAdmin()) return;
            populateScheduleVideoSelect();
            const nowOffset = new Date(new Date().getTime() - new Date().getTimezoneOffset() * 60000);
            nowOffset.setMinutes(nowOffset.getMinutes() + 5);
            document.getElementById('scheduleDateTime').value = nowOffset.toISOString().slice(0,16);
            
            document.getElementById('scheduleLiveModal').classList.add('show');
            document.querySelectorAll('#scheduleLiveModal .tab-btn').forEach(b => b.classList.remove('active'));
            document.querySelector('#scheduleLiveModal .tab-btn[data-tab="scheduleExisting"]').classList.add('active');
            document.getElementById('scheduleExisting').style.display = 'block';
            document.getElementById('scheduleUpload').style.display = 'none';
        }

        document.querySelector('#scheduleLiveModal .tabs').addEventListener('click', (e) => {
            if (!e.target.classList.contains('tab-btn')) return;
            const tab = e.target.dataset.tab;
            document.querySelectorAll('#scheduleLiveModal .tab-btn').forEach(b => b.classList.remove('active'));
            e.target.classList.add('active');
            document.getElementById('scheduleExisting').style.display = tab === 'scheduleExisting' ? 'block' : 'none';
            document.getElementById('scheduleUpload').style.display = tab === 'scheduleUpload' ? 'block' : 'none';
        });

        document.getElementById('scheduleLiveSubmit').onclick = async () => {
            const title = document.getElementById('scheduleTitle').value.trim();
            const dateTime = document.getElementById('scheduleDateTime').value;
            const duration = parseInt(document.getElementById('scheduleDuration').value) || 30;
            
            if (!title || !dateTime) return TOAST('Title and date required', 'error');
            let videoUrl;
            const activeTab = document.querySelector('#scheduleLiveModal .tab-btn.active').dataset.tab;
            
            if (activeTab === 'scheduleExisting') {
                videoUrl = document.getElementById('scheduleVideoSelect').value;
                if (!videoUrl) return TOAST('Select a video from library', 'error');
            } else {
                const file = document.getElementById('scheduleVideoFile').files[0];
                if (!file) return TOAST('Please select a video file', 'error');
                
                document.getElementById('scheduleLiveSubmit').disabled = true;
                document.getElementById('scheduleLiveSubmit').innerText = 'Uploading...';
                
                const uploadedUrl = await uploadToCloudinary(file);
                document.getElementById('scheduleLiveSubmit').disabled = false;
                document.getElementById('scheduleLiveSubmit').innerText = 'Schedule Event';
                
                if (!uploadedUrl) return;
                videoUrl = uploadedUrl;
            }
            
            const scheduledAt = new Date(dateTime).toISOString();
            const { error } = await SB.from('live_schedule').insert([{
                title, video_url: videoUrl, scheduled_at: scheduledAt, duration_minutes: duration
            }]);
            
            if (error) { 
                if (error.code === 'PGRST205') TOAST('Database table missing. Run SQL query first.', 'error');
                else TOAST('Failed: ' + error.message, 'error'); 
                return; 
            }
            
            TOAST('Event Scheduled Successfully!', 'success');
            closeModal('scheduleLiveModal');
            checkScheduledLive();
        };

        function cancelSchedule() {
            if (!isAdmin()) return;
            SB.from('live_schedule').delete().neq('id', 0).then((res) => {
                if(res.error && res.error.code === 'PGRST205') {
                    TOAST('No schedules found (Table not created yet)', 'info');
                } else {
                    TOAST('All scheduled events cleared', 'info');
                    loadLiveStreamFromDB();
                }
                closeModal('scheduleLiveModal');
            });
        }

        window.onload = () => {
            initAuth();
            const hash = window.location.hash.replace('#', '');
            navigateTo(hash || 'home', false);
            setInterval(() => {
                if (document.getElementById('page-home').classList.contains('show')) checkScheduledLive();
            }, 30000);
        };
    </script>
</body>
</html>