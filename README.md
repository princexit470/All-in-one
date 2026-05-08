
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>princexit_ | Creative Studio</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2">
    </script>
    <style>
        :root {
            --gold: #e8a850;
            --gold-hover: #f3b965;
            --bg: #000;
            --surface: #0a0a0a;
            --surface-hover: #141414;
            --border: rgba(255, 255, 255, 0.08);
            --text: #fff;
            --dim: #a0a0a0;
            --radius: 18px;
            --transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', 'Inter', system-ui, sans-serif;
            background: var(--bg);
            color: var(--text);
            min-height: 100vh;
            line-height: 1.6;
            -webkit-tap-highlight-color: transparent;
            overflow-x: hidden;
        }
        body.no-scroll {
            overflow: hidden;
            touch-action: none;
        }
        .toast-container {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 10000;
            display: flex;
            flex-direction: column;
            gap: 10px;
            pointer-events: none;
        }
        .toast {
            padding: 14px 24px;
            border-radius: 12px;
            color: #fff;
            font-weight: 500;
            font-size: 0.9rem;
            background: rgba(20, 20, 20, 0.95);
            backdrop-filter: blur(10px);
            animation: toastIn 0.4s ease forwards;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            max-width: 350px;
            border-left: 4px solid var(--gold);
            pointer-events: auto;
        }
        .toast.success {
            border-left-color: #2ecc71;
        }
        .toast.error {
            border-left-color: #e74c3c;
        }
        @keyframes toastIn {
            from {
                transform: translateX(120%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }
        .navbar {
            position: sticky;
            top: 0;
            z-index: 500;
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(20px);
            padding: 0.8rem 2rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid var(--border);
        }
        .nav-logo {
            font-size: 1.4rem;
            font-weight: 800;
            color: var(--gold);
            cursor: pointer;
            letter-spacing: -0.5px;
        }
        .nav-links {
            display: flex;
            gap: 0.5rem;
            list-style: none;
            align-items: center;
        }
        .nav-links a {
            color: var(--dim);
            text-decoration: none;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            cursor: pointer;
            font-size: 0.9rem;
            font-weight: 500;
            transition: var(--transition);
        }
        .nav-links a:hover,
        .nav-links a.active {
            color: #fff;
            background: rgba(255, 255, 255, 0.05);
        }
        .nav-right {
            display: flex;
            align-items: center;
            gap: 12px;
            position: relative;
        }
        .nav-btn {
            padding: 0.5rem 1.2rem;
            border-radius: 20px;
            border: 1px solid var(--border);
            background: transparent;
            color: #fff;
            cursor: pointer;
            font-size: 0.85rem;
            font-weight: 500;
            transition: var(--transition);
            white-space: nowrap;
        }
        .nav-btn:hover {
            background: rgba(255, 255, 255, 0.05);
        }
        .nav-btn.primary {
            background: var(--gold);
            border: none;
            color: #000;
            font-weight: 600;
        }
        .nav-btn.primary:hover {
            background: var(--gold-hover);
        }
        .profile-chip {
            display: flex;
            align-items: center;
            gap: 8px;
            background: rgba(255, 255, 255, 0.05);
            padding: 0.4rem 1rem;
            border-radius: 20px;
            cursor: pointer;
            border: 1px solid var(--border);
        }
        .profile-chip span {
            color: var(--gold);
            font-size: 0.85rem;
            font-weight: 500;
            max-width: 120px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
        .profile-dropdown {
            position: absolute;
            top: 50px;
            right: 0;
            background: #0f0f0f;
            border-radius: 12px;
            padding: 0.5rem;
            border: 1px solid var(--border);
            z-index: 60;
            display: none;
            min-width: 180px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.8);
        }
        .profile-dropdown.show {
            display: block;
            animation: dropIn 0.2s ease;
        }
        @keyframes dropIn {
            from {
                opacity: 0;
                transform: translateY(-10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .profile-dropdown a {
            display: block;
            padding: 0.7rem 1rem;
            color: var(--dim);
            text-decoration: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 0.85rem;
            transition: var(--transition);
        }
        .profile-dropdown a:hover {
            background: rgba(255, 255, 255, 0.05);
            color: #fff;
        }
        .hamburger {
            display: none;
            background: none;
            border: none;
            flex-direction: column;
            gap: 5px;
            cursor: pointer;
            padding: 5px;
        }
        .hamburger span {
            width: 24px;
            height: 2px;
            background: #fff;
            display: block;
            border-radius: 2px;
            transition: var(--transition);
        }
        .mobile-menu {
            position: fixed;
            top: 0;
            right: -300px;
            width: 280px;
            height: 100vh;
            background: rgba(5, 5, 5, 0.98);
            backdrop-filter: blur(20px);
            z-index: 600;
            padding: 5rem 1.5rem 2rem;
            transition: right 0.4s ease;
            border-left: 1px solid var(--border);
        }
        .mobile-menu.open {
            right: 0;
        }
        .mobile-menu a {
            display: block;
            color: var(--dim);
            padding: 1rem;
            text-decoration: none;
            border-radius: 12px;
            cursor: pointer;
            font-weight: 500;
        }
        .mobile-divider {
            border: none;
            border-top: 1px solid var(--border);
            margin: 1rem 0;
        }
        .overlay {
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.8);
            z-index: 550;
            display: none;
        }
        .overlay.show {
            display: block;
        }
        .main-content {
            padding: 2rem;
            max-width: 1400px;
            margin: 0 auto;
            min-height: 80vh;
        }
        .page {
            display: none;
            animation: pageFade 0.35s ease forwards;
        }
        .page.show {
            display: block;
        }
        @keyframes pageFade {
            from {
                opacity: 0;
                transform: translateY(12px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .hero-section {
            text-align: center;
            padding: 3rem 0;
        }
        .hero-title {
            font-size: 3.5rem;
            color: var(--gold);
            font-weight: 900;
        }
        .hero-subtitle {
            color: var(--dim);
            font-size: 1.2rem;
        }
        .live-section {
            margin: 2rem auto;
            max-width: 1000px;
            padding: 1.5rem;
            background: var(--surface);
            border-radius: var(--radius);
            border: 1px solid var(--border);
            position: relative;
        }
        .live-badge {
            background: #e74c3c;
            color: #fff;
            padding: 0.35rem 0.9rem;
            border-radius: 20px;
            font-size: 0.78rem;
            font-weight: 700;
            animation: pulse 2s infinite;
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }
        .live-badge.offline {
            background: #333;
            color: #888;
            animation: none;
        }
        @keyframes pulse {
            0% {
                box-shadow: 0 0 0 0 rgba(231, 76, 60, 0.4);
            }
            70% {
                box-shadow: 0 0 0 10px rgba(231, 76, 60, 0);
            }
            100% {
                box-shadow: 0 0 0 0 rgba(231, 76, 60, 0);
            }
        }
        .live-video-container {
            width: 100%;
            aspect-ratio: 16/9;
            background: #000;
            border-radius: 12px;
            overflow: hidden;
            position: relative;
            border: 1px solid var(--border);
        }
        .live-video-container iframe,
        .live-video-container video {
            width: 100%;
            height: 100%;
            border: none;
        }
        .coming-soon-overlay {
            position: absolute;
            inset: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            background: #000;
            flex-direction: column;
            gap: 15px;
            z-index: 2;
        }
        .coming-soon-overlay i {
            font-size: 3.5rem;
            color: #333;
        }
        .coming-soon-overlay h3 {
            color: var(--dim);
            letter-spacing: 3px;
        }
        .live-admin-set-btn {
            position: absolute;
            top: 12px;
            right: 16px;
            background: rgba(255, 255, 255, 0.08);
            border: 1px solid var(--border);
            color: #fff;
            padding: 0.3rem 0.9rem;
            border-radius: 20px;
            font-size: 0.75rem;
            cursor: pointer;
            transition: var(--transition);
            z-index: 5;
        }
        .live-admin-set-btn:hover {
            background: var(--gold);
            color: #000;
        }
        .quick-links {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 3rem;
            flex-wrap: wrap;
        }
        .quick-link-card {
            background: var(--surface);
            border: 1px solid var(--border);
            padding: 1.5rem 2rem;
            border-radius: var(--radius);
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
            min-width: 150px;
        }
        .quick-link-card:hover {
            border-color: var(--gold);
            transform: translateY(-4px);
        }
        .quick-link-card i {
            font-size: 2rem;
            color: var(--gold);
        }
        .quick-link-card span {
            font-weight: 600;
        }
        .section-title {
            font-size: 1.8rem;
            margin-bottom: 1rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .search-container {
            margin-bottom: 1.2rem;
            display: flex;
            align-items: center;
            background: var(--surface);
            border-radius: 30px;
            padding: 0.7rem 1.4rem;
            border: 1px solid var(--border);
        }
        .search-container i {
            color: var(--dim);
            margin-right: 10px;
        }
        .search-container input {
            background: transparent;
            border: none;
            color: #fff;
            width: 100%;
            outline: none;
            font-size: 0.95rem;
        }
        .add-media-bar {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 1rem;
            flex-wrap: wrap;
        }
        .add-media-btn {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            padding: 0.6rem 1.2rem;
            border-radius: 25px;
            background: var(--gold);
            color: #000;
            border: none;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.85rem;
            transition: var(--transition);
        }
        .add-media-btn:hover {
            background: var(--gold-hover);
            transform: translateY(-2px);
        }
        .media-count-badge {
            font-size: 0.78rem;
            color: var(--dim);
            background: var(--surface);
            padding: 0.35rem 0.9rem;
            border-radius: 20px;
            border: 1px solid var(--border);
        }
        /* GALLERY */
        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
            gap: 1.2rem;
        }
        .gallery-item {
            position: relative;
            border-radius: 14px;
            overflow: hidden;
            cursor: pointer;
            background: var(--surface);
            aspect-ratio: 4/5;
            border: 1px solid var(--border);
            transition: var(--transition);
        }
        .gallery-item:hover {
            border-color: rgba(255, 255, 255, 0.2);
        }
        .gallery-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s;
        }
        .gallery-item:hover img {
            transform: scale(1.06);
        }
        .media-title {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(transparent, rgba(0, 0, 0, 0.9));
            color: #fff;
            padding: 30px 15px 15px;
            font-size: 0.85rem;
            font-weight: 500;
            z-index: 5;
        }
        .menu-btn,
        .delete-media-btn {
            position: absolute;
            top: 10px;
            width: 32px;
            height: 32px;
            border-radius: 50%;
            cursor: pointer;
            z-index: 10;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
            background: rgba(0, 0, 0, 0.6);
            color: #fff;
            font-size: 0.8rem;
        }
        .menu-btn {
            right: 10px;
        }
        .delete-media-btn {
            left: 10px;
            background: rgba(231, 76, 60, 0.7);
        }
        .context-menu {
            position: absolute;
            top: 48px;
            right: 10px;
            background: #111;
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 0.5rem 0;
            z-index: 20;
            min-width: 160px;
            display: none;
        }
        .context-menu.show {
            display: block;
            animation: dropIn 0.2s ease;
        }
        .context-menu button {
            display: block;
            width: 100%;
            text-align: left;
            padding: 0.7rem 1.2rem;
            background: none;
            border: none;
            color: #ccc;
            cursor: pointer;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .context-menu button:hover {
            background: rgba(255, 255, 255, 0.05);
            color: var(--gold);
        }
        .lightbox {
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.98);
            z-index: 3000;
            display: none;
            align-items: center;
            justify-content: center;
            flex-direction: column;
        }
        .lightbox.show {
            display: flex;
        }
        .lb-image-wrap {
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            height: 70vh;
            transition: transform 0.3s;
        }
        .lightbox img {
            max-width: 90vw;
            max-height: 68vh;
            border-radius: 8px;
            object-fit: contain;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.8);
        }
        .lb-close-btn,
        .lb-download-btn {
            position: absolute;
            top: 20px;
            width: 44px;
            height: 44px;
            border-radius: 50%;
            border: none;
            color: #fff;
            cursor: pointer;
            z-index: 20;
            background: rgba(255, 255, 255, 0.1);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
        }
        .lb-close-btn {
            right: 25px;
        }
        .lb-download-btn {
            right: 80px;
        }
        .lb-nav-btn {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid var(--border);
            color: #fff;
            font-size: 1.4rem;
            width: 46px;
            height: 46px;
            border-radius: 50%;
            cursor: pointer;
            z-index: 20;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .lb-nav-prev {
            left: 20px;
        }
        .lb-nav-next {
            right: 20px;
        }
        .lb-counter-text {
            position: absolute;
            bottom: 85px;
            color: var(--dim);
            z-index: 20;
        }
        .lb-action-bar button {
            padding: 0.6rem 1.3rem;
            border-radius: 25px;
            border: 1px solid var(--border);
            background: rgba(0, 0, 0, 0.5);
            color: #fff;
            cursor: pointer;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            gap: 7px;
        }
        /* VIDEOS */
        .video-feed {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            max-width: 1000px;
            margin: 0 auto;
        }
        .video-card-yt {
            display: flex;
            gap: 0.8rem;
            background: var(--surface);
            border-radius: 12px;
            overflow: visible;
            border: 1px solid var(--border);
            transition: var(--transition);
            align-items: stretch;
        }
        .video-card-yt:hover {
            border-color: rgba(255, 255, 255, 0.15);
        }
        .video-thumb-yt {
            width: 240px;
            min-width: 200px;
            aspect-ratio: 16/9;
            background: #050505;
            position: relative;
            flex-shrink: 0;
            border-right: 1px solid var(--border);
            overflow: hidden;
            cursor: pointer;
        }
        .video-thumb-yt iframe,
        .video-thumb-yt video {
            width: 100%;
            height: 100%;
            border: none;
            object-fit: cover;
        }
        .video-info-yt {
            padding: 1rem 1.2rem 1rem 0;
            display: flex;
            align-items: center;
            flex: 1;
            min-width: 0;
            position: relative;
        }
        .video-info-yt h3 {
            font-size: 0.95rem;
            font-weight: 600;
            color: #fff;
            margin: 0;
            padding-right: 36px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            flex: 1;
        }
        .video-menu-dot {
            position: absolute;
            top: 8px;
            right: 8px;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background: transparent;
            border: none;
            color: #fff;
            cursor: pointer;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 10;
            transition: var(--transition);
        }
        .video-menu-dot:hover {
            background: rgba(255, 255, 255, 0.1);
        }
        .doc-list {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }
        .doc-item {
            background: var(--surface);
            border: 1px solid var(--border);
            padding: 1rem 1.5rem;
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        .doc-info {
            display: flex;
            align-items: center;
            gap: 12px;
            flex: 1;
            min-width: 0;
        }
        .doc-info i {
            font-size: 1.8rem;
            color: #e74c3c;
        }
        .doc-info span {
            font-weight: 500;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .doc-actions-group button {
            padding: 0.5rem 1rem;
            border-radius: 20px;
            border: 1px solid var(--border);
            background: transparent;
            color: #fff;
            cursor: pointer;
            font-size: 0.8rem;
        }
        .doc-actions-group button.primary {
            background: var(--gold);
            border: none;
            color: #000;
        }
        .doc-lightbox-full {
            position: fixed;
            inset: 0;
            background: #000;
            z-index: 3500;
            display: none;
        }
        .doc-lightbox-full.show {
            display: block;
        }
        .doc-header {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            padding: 1rem 2rem;
            background: linear-gradient(to bottom, rgba(0, 0, 0, 0.95), transparent);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .doc-content {
            width: 100%;
            height: 100vh;
            border: none;
        }
        .modal-backdrop {
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.85);
            z-index: 5000;
            display: none;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(8px);
        }
        .modal-backdrop.show {
            display: flex;
        }
        .modal-dialog {
            background: #0a0a0a;
            border-radius: 24px;
            padding: 2.2rem;
            width: 90%;
            max-width: 420px;
            border: 1px solid var(--border);
            position: relative;
        }
        .modal-dialog h2 {
            color: var(--gold);
            text-align: center;
            margin-bottom: 1.2rem;
        }
        .modal-dialog input,
        .modal-dialog textarea {
            width: 100%;
            padding: 0.85rem 1.1rem;
            margin: 0.4rem 0;
            border-radius: 12px;
            border: 1px solid var(--border);
            background: #000;
            color: #fff;
            outline: none;
            font-size: 0.9rem;
        }
        .modal-dialog .modal-submit {
            width: 100%;
            padding: 0.85rem;
            margin-top: 1rem;
            border-radius: 12px;
            border: none;
            background: var(--gold);
            color: #000;
            font-weight: 700;
            cursor: pointer;
        }
        .modal-close {
            position: absolute;
            top: 14px;
            right: 18px;
            background: none;
            border: none;
            color: var(--dim);
            font-size: 1.1rem;
            cursor: pointer;
        }
        .hidden {
            display: none !important;
        }
        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }
            .hamburger {
                display: flex;
            }
            .main-content {
                padding: 1rem;
            }
            .video-card-yt {
                flex-direction: column;
            }
            .video-thumb-yt {
                width: 100%;
                min-width: unset;
                border-right: none;
                border-bottom: 1px solid var(--border);
            }
            .video-info-yt {
                padding: 0.8rem;
            }
            .video-info-yt h3 {
                padding-right: 30px;
            }
        }
    </style>
</head>
<body>
    <div class="toast-container" id="toastContainer"></div>
    <div class="overlay" id="mobileOverlay"></div>
    <!-- LIGHTBOX -->
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
        <div class="doc-header"><span class="doc-title" id="docFullTitle"></span><div><button class="doc-download-btn" id="docFullDownloadBtn"><i class="fas fa-download"></i> Download</button><button class="doc-close-btn" onclick="closeDocFullLB()">✕</button></div></div>
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
        <div id="mobileLoggedOut"><a onclick="showAuth('login')"><i class="fas fa-sign-in-alt fa-fw"></i> Log In</a><a onclick="showAuth('signup')" style="color:gold;"><i class="fas fa-user-plus fa-fw"></i> Sign Up</a></div>
        <div id="mobileLoggedIn" class="hidden"><a onclick="doLogout()"><i class="fas fa-sign-out-alt fa-fw"></i> Logout</a></div>
    </div>

    <div class="main-content">
        <div class="page show" id="page-home">
            <div class="hero-section"><h1 class="hero-title">princexit_</h1><p class="hero-subtitle">Photography • Cinematography • Creative</p></div>
            <div class="live-section" id="liveSection">
                <div class="live-header"><span class="live-badge offline" id="liveBadge"><i class="fas fa-circle"></i> OFFLINE</span><h3 style="font-size:1.3rem;">Live Broadcast</h3></div>
                <div class="live-video-container" id="liveVideoContainer"><div class="coming-soon-overlay" id="liveOverlay"><i class="fas fa-video-slash"></i><h3>STREAM OFFLINE</h3></div></div>
                <button class="live-admin-set-btn hidden" id="liveAdminSetBtn" onclick="showLiveStreamModal()"><i class="fas fa-cog"></i> Set Live</button>
            </div>
            <div class="quick-links">
                <div class="quick-link-card" onclick="navigateTo('gallery')"><i class="fas fa-camera-retro"></i><span>Photos</span></div>
                <div class="quick-link-card" onclick="navigateTo('videos')"><i class="fas fa-film"></i><span>Videos</span></div>
                <div class="quick-link-card" onclick="navigateTo('documents')"><i class="fas fa-folder-open"></i><span>Documents</span></div>
            </div>
        </div>
        <div class="page" id="page-gallery">
            <h2 class="section-title"><i class="fas fa-images" style="color:var(--gold);"></i> Photos</h2>
            <div class="add-media-bar" id="photoAddBar" style="display:none;"><button class="add-media-btn" onclick="openAddMediaModal('photo')"><i class="fas fa-plus-circle"></i> Add Photo</button><span class="media-count-badge" id="photoCountBadge">0</span></div>
            <div class="search-container"><i class="fas fa-search"></i><input type="text" id="searchPhotos" placeholder="Search photos..." onkeyup="renderPhotos()"></div>
            <div class="gallery-grid" id="photoGrid"></div>
        </div>
        <div class="page" id="page-videos">
            <h2 class="section-title"><i class="fas fa-play-circle" style="color:var(--gold);"></i> Videos</h2>
            <div class="add-media-bar" id="videoAddBar" style="display:none;"><button class="add-media-btn" onclick="openAddMediaModal('video')"><i class="fas fa-plus-circle"></i> Add Video</button><span class="media-count-badge" id="videoCountBadge">0</span></div>
            <div class="search-container"><i class="fas fa-search"></i><input type="text" id="searchVideos" placeholder="Search videos..." onkeyup="renderVideos()"></div>
            <div class="video-feed" id="videoFeed"></div>
        </div>
        <div class="page" id="page-documents">
            <h2 class="section-title"><i class="fas fa-file-pdf" style="color:var(--gold);"></i> Documents</h2>
            <div class="add-media-bar" id="docAddBar" style="display:none;"><button class="add-media-btn" onclick="openAddMediaModal('doc')"><i class="fas fa-plus-circle"></i> Add Document</button><span class="media-count-badge" id="docCountBadge">0</span></div>
            <div class="search-container"><i class="fas fa-search"></i><input type="text" id="searchDocs" placeholder="Search documents..." onkeyup="renderDocs()"></div>
            <div class="doc-list" id="docList"></div>
        </div>
        <div class="page" id="page-about">
            <div style="text-align:center;padding:4rem;background:var(--surface);border-radius:var(--radius);max-width:600px;margin:auto;">
                <h2 style="color:var(--gold);">Get in Touch</h2>
                <p>princekvishwakarma@yahoo.com</p>
                <div style="margin-top:1rem;"><a href="https://instagram.com/princexit_" target="_blank" style="color:#fff;font-size:2rem;"><i class="fab fa-instagram"></i></a></div>
            </div>
        </div>
    </div>

    <!-- AUTH MODAL -->
    <div class="modal-backdrop" id="authModal">
        <div class="modal-dialog">
            <button class="modal-close" onclick="closeModal('authModal')">✕</button>
            <h2 id="authTitle">Welcome Back</h2>
            <input type="email" id="authEmail" placeholder="Email address">
            <input type="password" id="authPass" placeholder="Password">
            <span class="forgot-link" id="forgotPassBtn" onclick="showAuth('reset')" style="display:block;text-align:right;margin:6px 0;font-size:0.8rem;color:var(--dim);cursor:pointer;">Forgot Password?</span>
            <button class="modal-submit" id="authSubmit">Log In</button>
            <p style="text-align:center;margin-top:1rem;font-size:0.85rem;color:var(--dim);" id="authSwitch">New here? <span class="modal-link" onclick="showAuth('signup')">Create account</span></p>
        </div>
    </div>
    <div class="modal-backdrop" id="addMediaModal">
        <div class="modal-dialog">
            <button class="modal-close" onclick="closeModal('addMediaModal')">✕</button>
            <h2 id="addMediaTitle">Add Media Link</h2>
            <label>Title <span style="color:#e74c3c;">*</span></label>
            <input type="text" id="addMediaName" placeholder="e.g., Sunset Portrait">
            <label>Link / URL <span style="color:#e74c3c;">*</span></label>
            <textarea id="addMediaUrl" placeholder="Paste your link..." rows="3"></textarea>
            <button class="modal-submit" id="addMediaSubmit">Add Media</button>
            <input type="hidden" id="addMediaType" value="photo">
        </div>
    </div>
    <div class="modal-backdrop" id="liveStreamModal">
        <div class="modal-dialog">
            <button class="modal-close" onclick="closeModal('liveStreamModal')">✕</button>
            <h2>Set Live Stream</h2>
            <p style="color:var(--dim);text-align:center;margin-bottom:1rem;">Paste embed URL (YouTube Live, HLS, etc.)</p>
            <label>Stream URL</label>
            <input type="text" id="liveStreamUrl" placeholder="https://...">
            <button class="modal-submit" id="liveStreamSubmit">Go Live</button>
            <button class="nav-btn" style="width:100%;margin-top:0.5rem;background:transparent;color:var(--dim);" onclick="clearLiveStream()">Stop Streaming</button>
        </div>
    </div>

    <script>
        const SB = window.supabase.createClient('https://wvlvamuehbyfdsozjczk.supabase.co', 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Ind2bHZhbXVlaGJ5ZmRzb3pqY3prIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzU1NTM4MDAsImV4cCI6MjA5MTEyOTgwMH0.oaF4wymSu0ePwQSp3moV0sKZVgz5f50ILun5iaU816A');
        const ADMIN_EMAIL = "helloworldd1224@gmail.com";
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
            setTimeout(() => { d.style.animation = 'toastIn 0.4s ease reverse forwards';
                setTimeout(() => d.remove(), 400); }, 3500);
        }

        function isAdmin() { return USER && USER.email === ADMIN_EMAIL; }

        function updateAdminUI() {
            const admin = isAdmin();
            document.getElementById('photoAddBar').style.display = admin ? 'flex' : 'none';
            document.getElementById('videoAddBar').style.display = admin ? 'flex' : 'none';
            document.getElementById('docAddBar').style.display = admin ? 'flex' : 'none';
            document.getElementById('liveAdminSetBtn').classList.toggle('hidden', !admin);
            renderPhotos();
            renderVideos();
            renderDocs();
        }

        // URL helpers
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
                isDrive: true,
                isDirectVideo: false
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
                else ALL_DOCS.push(obj);
            });
            updateCountBadges();
            renderPhotos(); renderVideos(); renderDocs();
        }
        function updateCountBadges() {
            document.getElementById('photoCountBadge').textContent = ALL_PHOTOS.length + ' photo' + (ALL_PHOTOS.length !== 1 ? 's' : '');
            document.getElementById('videoCountBadge').textContent = ALL_VIDEOS.length + ' video' + (ALL_VIDEOS.length !== 1 ? 's' : '');
            document.getElementById('docCountBadge').textContent = ALL_DOCS.length + ' doc' + (ALL_DOCS.length !== 1 ? 's' : '');
        }

        function openAddMediaModal(type) {
            if (!isAdmin()) return TOAST('Only admin can add', 'error');
            document.getElementById('addMediaType').value = type;
            document.getElementById('addMediaTitle').textContent = 'Add ' + { photo: 'Photo', video: 'Video', doc: 'Document' }[type] + ' Link';
            document.getElementById('addMediaModal').classList.add('show');
        }
        document.getElementById('addMediaSubmit').onclick = async () => {
            const type = document.getElementById('addMediaType').value;
            const title = document.getElementById('addMediaName').value.trim();
            const url = document.getElementById('addMediaUrl').value.trim();
            if (!title || !url) return TOAST('Title and URL required', 'error');
            if (!url.startsWith('http') && !url.includes('drive.google.com') && !url.includes('youtu')) return TOAST('Valid URL required', 'error');
            const res = await addMediaToDB(type, title, url);
            if (res) { TOAST('Added!', 'success'); closeModal('addMediaModal'); await loadAllMediaFromDB(); }
        };

        // Auth
        async function initAuth() { const { data } = await SB.auth.getSession(); updateUI(data.session ? data.session.user : null); await loadAllMediaFromDB(); }
        SB.auth.onAuthStateChange((event, session) => { updateUI(session ? session.user : null); if (session) loadAllMediaFromDB(); });
        function updateUI(u) {
            USER = u; const li = !!u;
            document.getElementById('desktopAuthBtns').classList.toggle('hidden', li);
            document.getElementById('profileChip').classList.toggle('hidden', !li);
            document.getElementById('mobileLoggedOut').classList.toggle('hidden', li);
            document.getElementById('mobileLoggedIn').classList.toggle('hidden', !li);
            if (u) document.getElementById('profileEmailText').textContent = u.email.split('@')[0];
            updateAdminUI();
            loadLiveStreamFromDB();
        }
        function showAuth(mode) {
            AUTH_MODE = mode;
            document.getElementById('authEmail').style.display = 'block';
            document.getElementById('authPass').style.display = 'block';
            document.getElementById('forgotPassBtn').style.display = 'none';
            if (mode === 'login') {
                document.getElementById('authTitle').textContent = 'Welcome Back';
                document.getElementById('authSubmit').textContent = 'Log In';
                document.getElementById('authSwitch').innerHTML = 'New here? <span class="modal-link" onclick="showAuth(\'signup\')">Create account</span>';
                document.getElementById('forgotPassBtn').style.display = 'block';
            } else if (mode === 'signup') {
                document.getElementById('authTitle').textContent = 'Create Account';
                document.getElementById('authSubmit').textContent = 'Sign Up';
                document.getElementById('authSwitch').innerHTML = 'Have account? <span class="modal-link" onclick="showAuth(\'login\')">Log In</span>';
            } else if (mode === 'reset') {
                document.getElementById('authTitle').textContent = 'Reset Password';
                document.getElementById('authSubmit').textContent = 'Send Reset Link';
                document.getElementById('authPass').style.display = 'none';
                document.getElementById('authSwitch').innerHTML = '<span class="modal-link" onclick="showAuth(\'login\')">Back to Login</span>';
            }
            document.getElementById('authModal').classList.add('show');
        }
        function closeModal(id) { document.getElementById(id).classList.remove('show'); }
        document.getElementById('authSubmit').onclick = async () => {
            const email = document.getElementById('authEmail').value.trim(), pass = document.getElementById('authPass').value.trim();
            if (AUTH_MODE !== 'reset' && (!email || !pass)) return TOAST('Fill all fields', 'error');
            if (AUTH_MODE === 'reset' && !email) return TOAST('Enter email', 'error');
            try {
                if (AUTH_MODE === 'reset') {
                    const { error } = await SB.auth.resetPasswordForEmail(email);
                    if (error) throw error;
                    TOAST('Reset link sent!', 'success'); closeModal('authModal'); return;
                }
                const r = AUTH_MODE === 'signup' ? await SB.auth.signUp({ email, password: pass }) : await SB.auth.signInWithPassword({ email, password: pass });
                if (r.error) throw r.error;
                TOAST(AUTH_MODE === 'signup' ? 'Account created!' : 'Logged in!', 'success');
                closeModal('authModal'); updateUI(r.data.user); await loadAllMediaFromDB();
            } catch (e) { TOAST(e.message, 'error'); }
        };
        async function doLogout() { await SB.auth.signOut(); document.getElementById('profileDropdown').classList.remove('show'); ALL_PHOTOS = []; ALL_VIDEOS = []; ALL_DOCS = []; updateCountBadges(); renderPhotos(); renderVideos(); renderDocs(); TOAST('Logged out', 'info'); }

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
        }

        // RENDER FUNCTIONS
        function renderPhotos() {
            const q = (document.getElementById('searchPhotos')?.value || '').toLowerCase();
            const filtered = ALL_PHOTOS.filter(p => (p.title || '').toLowerCase().includes(q));
            const grid = document.getElementById('photoGrid');
            if (!ALL_PHOTOS.length) { grid.innerHTML = '<div style="text-align:center;padding:4rem;color:var(--dim);">No photos yet</div>'; return; }
            if (!filtered.length) { grid.innerHTML = '<div style="text-align:center;padding:2rem;color:var(--dim);">No match</div>'; return; }
            const admin = isAdmin();
            grid.innerHTML = filtered.map((p) => {
                const idx = ALL_PHOTOS.indexOf(p);
                return `
                <div class="gallery-item" onclick="openLB(${idx})">
                    <img src="${p.displayUrl}" loading="lazy" alt="${p.title}">
                    <div class="media-title">${p.title}</div>
                    <button class="menu-btn" onclick="toggleMenu(event,'pm${idx}')">⋮</button>
                    ${admin ? `<button class="delete-media-btn" onclick="event.stopPropagation();deleteMediaById('${p.id}')"><i class="fas fa-trash"></i></button>` : ''}
                    <div class="context-menu" id="pm${idx}">
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
            if (!ALL_VIDEOS.length) { feed.innerHTML = '<div style="text-align:center;padding:3rem;color:var(--dim);">No videos yet</div>'; return; }
            if (!filtered.length) { feed.innerHTML = '<div style="text-align:center;padding:2rem;color:var(--dim);">No match</div>'; return; }
            const admin = isAdmin();
            feed.innerHTML = filtered.map((v, idx) => {
                const thumb = v.isDirectVideo ? `<video src="${v.displayUrl}" preload="metadata" controls playsinline></video>` : `<iframe src="${v.displayUrl}" allowfullscreen loading="lazy"></iframe>`;
                return `
                <div class="video-card-yt">
                    <div class="video-thumb-yt" onclick="window.open('${v.originalLink}','_blank')">${thumb}</div>
                    <div class="video-info-yt">
                        <h3>${v.title}</h3>
                        <button class="video-menu-dot" onclick="toggleMenu(event,'vm${idx}')">⋮</button>
                        <div class="context-menu" id="vm${idx}" style="top:40px;right:4px;">
                            <button onclick="event.stopPropagation(); window.open('${v.originalLink}','_blank')"><i class="fas fa-external-link-alt"></i> Open Original</button>
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
            if (!ALL_DOCS.length) { list.innerHTML = '<div style="text-align:center;padding:3rem;color:var(--dim);">No documents yet</div>'; return; }
            if (!filtered.length) { list.innerHTML = '<div style="text-align:center;padding:2rem;color:var(--dim);">No match</div>'; return; }
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
                TOAST('Download complete!', 'success');
            } catch (e) {
                const a = document.createElement('a'); a.href = url; a.download = filename || ''; a.target = '_blank'; document.body.appendChild(a); a.click(); document.body.removeChild(a);
            }
        }
        async function deleteMediaById(id) { if (!isAdmin()) return; if (!confirm('Delete permanently?')) return; const ok = await deleteMediaFromDB(id); if (ok) { TOAST('Deleted', 'success'); await loadAllMediaFromDB(); } }

        // LIGHTBOX
        let LB_IDX = 0;
        function openLB(idx) { if (!ALL_PHOTOS.length) return; LB_IDX = idx; updateLB(); document.getElementById('lightbox').classList.add('show'); document.body.classList.add('no-scroll'); }
        function closeLB() { document.getElementById('lightbox').classList.remove('show'); document.body.classList.remove('no-scroll'); }
        function updateLB() { const p = ALL_PHOTOS[LB_IDX]; if (!p) return; document.getElementById('lbImage').src = p.displayUrl; document.getElementById('lbCounter').textContent = `${LB_IDX+1} / ${ALL_PHOTOS.length} - ${p.title}`; }
        function lbNav(dir) { if (ALL_PHOTOS.length <= 1) return; LB_IDX = (LB_IDX + dir + ALL_PHOTOS.length) % ALL_PHOTOS.length; updateLB(); }
        document.getElementById('lbDownloadBtn').onclick = () => { const p = ALL_PHOTOS[LB_IDX]; if (p) downloadMedia(p.downloadUrl, p.title); };
        document.getElementById('lbCopyBtn').onclick = () => { const p = ALL_PHOTOS[LB_IDX]; if (p) { navigator.clipboard.writeText(p.originalLink); TOAST('Link copied', 'success'); } };

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

        // MOBILE
        document.getElementById('hamburgerBtn').onclick = () => { document.getElementById('mobileMenu').classList.add('open'); document.getElementById('mobileOverlay').classList.add('show'); };
        document.getElementById('mobileOverlay').onclick = () => { document.getElementById('mobileMenu').classList.remove('open'); document.getElementById('mobileOverlay').classList.remove('show'); };

        // ========== LIVE STREAM (Supabase global) ==========
        async function loadLiveStreamFromDB() {
            // Fetch latest live row from media table (type='live')
            const { data, error } = await SB.from('media').select('*').eq('type', 'live').order('created_at', { ascending: false }).limit(1);
            if (error) { console.warn('Live fetch error:', error); return; }
            const url = data && data.length ? data[0].url : null;
            updateLiveStreamUI(url);
        }
        function updateLiveStreamUI(url) {
            const badge = document.getElementById('liveBadge');
            const overlay = document.getElementById('liveOverlay');
            const container = document.getElementById('liveVideoContainer');
            // clear previous
            container.querySelectorAll('iframe,video').forEach(el => el.remove());
            if (url) {
                badge.classList.remove('offline');
                badge.innerHTML = '<i class="fas fa-circle"></i> LIVE NOW';
                overlay.style.display = 'none';
                if (url.includes('youtube.com/embed') || url.includes('youtu.be')) {
                    const iframe = document.createElement('iframe');
                    const sep = url.includes('?') ? '&' : '?';
                    iframe.src = url + sep + 'autoplay=1&controls=0&disablekb=1&modestbranding=1';
                    iframe.allowFullscreen = true;
                    container.appendChild(iframe);
                } else if (isDirectVideoFile(url)) {
                    const video = document.createElement('video');
                    video.src = url;
                    video.controls = true;
                    video.autoplay = true;
                    video.playsInline = true;
                    container.appendChild(video);
                } else {
                    const iframe = document.createElement('iframe');
                    iframe.src = url;
                    iframe.allowFullscreen = true;
                    container.appendChild(iframe);
                }
            } else {
                badge.classList.add('offline');
                badge.innerHTML = '<i class="fas fa-circle"></i> OFFLINE';
                overlay.style.display = 'flex';
            }
        }
        function showLiveStreamModal() {
            if (!isAdmin()) return;
            document.getElementById('liveStreamModal').classList.add('show');
            // prefill with current live url (if any)
            const current = document.querySelector('#liveVideoContainer iframe')?.src || '';
            document.getElementById('liveStreamUrl').value = current;
        }
        document.getElementById('liveStreamSubmit').onclick = async () => {
            const url = document.getElementById('liveStreamUrl').value.trim();
            if (!url) return TOAST('Enter a URL', 'error');
            // Delete any existing live rows and insert new
            await SB.from('media').delete().eq('type', 'live');
            const { error } = await SB.from('media').insert([{ type: 'live', title: 'live', url }]);
            if (error) { TOAST('Failed to set live: ' + error.message, 'error'); return; }
            TOAST('Live stream is now ON!', 'success');
            closeModal('liveStreamModal');
            loadLiveStreamFromDB();
        };
        function clearLiveStream() {
            if (!isAdmin()) return;
            SB.from('media').delete().eq('type', 'live').then(() => {
                TOAST('Live stream stopped', 'info');
                closeModal('liveStreamModal');
                loadLiveStreamFromDB();
            });
        }

        window.onload = () => {
            initAuth();
            loadLiveStreamFromDB();
            const hash = window.location.hash.replace('#', '');
            navigateTo(hash || 'home', false);
        };
    </script>
</body>
</html>