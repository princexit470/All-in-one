<!DOCTYPE html>
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

        /* TOAST */
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

        /* NAVBAR */
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

        /* HAMBURGER */
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

        /* MAIN */
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

        .search-container {
            margin-bottom: 1.5rem;
            display: flex;
            align-items: center;
            background: var(--surface);
            border-radius: 30px;
            padding: 0.8rem 1.5rem;
            border: 1px solid var(--border);
            transition: var(--transition);
        }
        .search-container:focus-within {
            border-color: var(--gold);
            box-shadow: 0 0 15px rgba(232, 168, 80, 0.1);
        }
        .search-container i {
            color: var(--dim);
            margin-right: 12px;
        }
        .search-container input {
            background: transparent;
            border: none;
            color: #fff;
            width: 100%;
            outline: none;
            font-size: 1rem;
        }
        .search-container input::placeholder {
            color: var(--dim);
        }

        .add-media-bar {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 1rem;
            flex-wrap: wrap;
        }
        .add-media-btn {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 0.7rem 1.4rem;
            border-radius: 25px;
            background: var(--gold);
            color: #000;
            border: none;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.9rem;
            transition: var(--transition);
        }
        .add-media-btn:hover {
            background: var(--gold-hover);
            transform: translateY(-2px);
        }
        .media-count-badge {
            font-size: 0.8rem;
            color: var(--dim);
            background: var(--surface);
            padding: 0.4rem 1rem;
            border-radius: 20px;
            border: 1px solid var(--border);
        }

        .hero-section {
            text-align: center;
            padding: 3rem 0;
        }
        .hero-title {
            font-size: 3.5rem;
            color: var(--gold);
            font-weight: 900;
            letter-spacing: -1px;
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
        }
        .live-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 1.2rem;
        }
        .live-header-left {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        .live-badge {
            background: #e74c3c;
            color: #fff;
            padding: 0.4rem 1rem;
            border-radius: 20px;
            font-size: 0.8rem;
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
        .live-video-container iframe {
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

        /* LIGHTBOX */
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
            height: 75vh;
            transition: transform 0.3s;
        }
        .lightbox img {
            max-width: 90vw;
            max-height: 100%;
            border-radius: 8px;
            user-select: none;
            pointer-events: none;
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
            transition: var(--transition);
        }
        .lb-close-btn {
            right: 25px;
        }
        .lb-download-btn {
            right: 80px;
        }
        .lb-close-btn:hover {
            background: #e74c3c;
        }
        .lb-download-btn:hover {
            background: var(--gold);
            color: #000;
        }
        .lb-nav-btn {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid var(--border);
            color: #fff;
            font-size: 1.5rem;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            cursor: pointer;
            z-index: 20;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .lb-nav-btn:hover {
            background: var(--gold);
            color: #000;
        }
        .lb-nav-prev {
            left: 20px;
        }
        .lb-nav-next {
            right: 20px;
        }
        .lb-counter-text {
            position: absolute;
            bottom: 90px;
            color: var(--dim);
            font-size: 0.95rem;
            z-index: 20;
        }
        .lb-action-bar {
            position: absolute;
            bottom: 25px;
            display: flex;
            gap: 1rem;
            z-index: 20;
        }
        .lb-action-bar button {
            padding: 0.7rem 1.5rem;
            border-radius: 25px;
            border: 1px solid var(--border);
            background: rgba(0, 0, 0, 0.5);
            color: #fff;
            cursor: pointer;
            font-size: 0.9rem;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .lb-action-bar button:hover {
            background: var(--gold);
            color: #000;
        }

        /* VIDEO FEED */
        .video-feed {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
            max-width: 1000px;
            margin: 0 auto;
        }
        .video-card-yt {
            display: flex;
            gap: 1.5rem;
            background: var(--surface);
            border-radius: 16px;
            overflow: hidden;
            border: 1px solid var(--border);
            transition: var(--transition);
        }
        .video-card-yt:hover {
            border-color: rgba(255, 255, 255, 0.2);
        }
        .video-thumb-yt {
            width: 320px;
            min-width: 280px;
            aspect-ratio: 16/9;
            background: #050505;
            position: relative;
            flex-shrink: 0;
            border-right: 1px solid var(--border);
        }
        .video-thumb-yt iframe {
            width: 100%;
            height: 100%;
            border: none;
            pointer-events: none;
        }
        .video-info-yt {
            padding: 1.5rem 1.5rem 1.5rem 0;
            flex: 1;
        }
        .video-info-yt h3 {
            font-size: 1.1rem;
            margin-bottom: 8px;
            color: #fff;
        }
        .video-meta {
            font-size: 0.85rem;
            color: var(--dim);
            margin-bottom: 12px;
        }
        .video-actions-yt {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        .video-actions-yt button {
            padding: 0.5rem 1rem;
            border-radius: 20px;
            border: 1px solid var(--border);
            background: transparent;
            color: #fff;
            cursor: pointer;
            font-size: 0.8rem;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .video-actions-yt button:hover {
            background: rgba(255, 255, 255, 0.08);
        }
        .video-actions-yt button.primary-btn-yt {
            background: var(--gold);
            border: none;
            color: #000;
            font-weight: 600;
        }
        .video-actions-yt button.primary-btn-yt:hover {
            background: var(--gold-hover);
        }

        /* DOC LIST */
        .doc-list {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }
        .doc-item {
            background: var(--surface);
            border: 1px solid var(--border);
            padding: 1.2rem 1.5rem;
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transition: var(--transition);
        }
        .doc-item:hover {
            border-color: var(--gold);
            background: var(--surface-hover);
        }
        .doc-info {
            display: flex;
            align-items: center;
            gap: 15px;
            overflow: hidden;
            flex: 1;
        }
        .doc-info i {
            font-size: 1.8rem;
            color: #e74c3c;
            background: rgba(231, 76, 60, 0.1);
            padding: 12px;
            border-radius: 10px;
            flex-shrink: 0;
        }
        .doc-info span {
            font-weight: 500;
            font-size: 1.05rem;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            max-width: 400px;
        }
        .doc-actions-group {
            display: flex;
            gap: 10px;
            flex-shrink: 0;
        }

        /* DOC FULL LIGHTBOX */
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
        .doc-lightbox-full .doc-header {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            padding: 1rem 2rem;
            background: linear-gradient(to bottom, rgba(0, 0, 0, 0.95), transparent);
            z-index: 10;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        .doc-lightbox-full .doc-title {
            color: #fff;
            font-weight: 600;
            font-size: 1.1rem;
            max-width: 60%;
        }
        .doc-lightbox-full .doc-download-btn {
            background: var(--gold);
            color: #000;
            border: none;
            padding: 0.6rem 1.5rem;
            border-radius: 25px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: var(--transition);
        }
        .doc-lightbox-full .doc-download-btn:hover {
            background: #fff;
        }
        .doc-lightbox-full .doc-close-btn {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            color: #fff;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .doc-lightbox-full .doc-content {
            width: 100%;
            height: 100vh;
            border: none;
            background: #111;
        }

        /* MODALS */
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
            padding: 2.5rem;
            width: 90%;
            max-width: 420px;
            border: 1px solid var(--border);
            position: relative;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.8);
        }
        .modal-dialog h2 {
            color: var(--gold);
            text-align: center;
            margin-bottom: 1.5rem;
            font-size: 1.5rem;
            font-weight: 700;
        }
        .modal-dialog input,
        .modal-dialog textarea {
            width: 100%;
            padding: 0.9rem 1.2rem;
            margin: 0.5rem 0;
            border-radius: 12px;
            border: 1px solid var(--border);
            background: #000;
            color: #fff;
            outline: none;
            font-size: 0.95rem;
            font-family: inherit;
            resize: vertical;
        }
        .modal-dialog input:focus,
        .modal-dialog textarea:focus {
            border-color: var(--gold);
        }
        .modal-dialog .modal-submit {
            width: 100%;
            padding: 0.9rem;
            margin-top: 1.2rem;
            border-radius: 12px;
            border: none;
            background: var(--gold);
            color: #000;
            font-weight: 700;
            font-size: 1rem;
            cursor: pointer;
            transition: var(--transition);
        }
        .modal-dialog .modal-submit:hover {
            background: var(--gold-hover);
        }
        .modal-close {
            position: absolute;
            top: 16px;
            right: 20px;
            background: none;
            border: none;
            color: var(--dim);
            font-size: 1.2rem;
            cursor: pointer;
        }
        .modal-close:hover {
            color: #fff;
        }
        .modal-link {
            color: var(--gold);
            cursor: pointer;
            font-weight: 500;
        }
        .modal-link:hover {
            color: #fff;
        }
        .forgot-link {
            display: block;
            text-align: right;
            margin-top: 8px;
            font-size: 0.8rem;
            color: var(--dim);
            cursor: pointer;
        }
        .forgot-link:hover {
            color: var(--gold);
        }
        .hidden {
            display: none !important;
        }
        .modal-subtitle {
            text-align: center;
            color: var(--dim);
            font-size: 0.85rem;
            margin-bottom: 1.2rem;
        }
        .modal-dialog label {
            display: block;
            color: var(--dim);
            font-size: 0.8rem;
            font-weight: 600;
            margin-bottom: 2px;
            margin-top: 10px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        @media (max-width: 900px) {
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
                padding: 1.2rem;
            }
        }
        @media (max-width: 768px) {
            .navbar {
                padding: 0.8rem 1.2rem;
            }
            .nav-links {
                display: none;
            }
            .hamburger {
                display: flex;
            }
            .main-content {
                padding: 1.2rem;
            }
            .hero-title {
                font-size: 2.5rem;
            }
            .gallery-grid {
                grid-template-columns: repeat(2, 1fr);
                gap: 0.8rem;
            }
            .lb-nav-btn {
                display: none;
            }
            .quick-links {
                gap: 10px;
            }
            .quick-link-card {
                min-width: calc(50% - 5px);
                padding: 1rem;
            }
            .doc-info span {
                max-width: 150px;
            }
            .doc-item {
                flex-wrap: wrap;
                gap: 10px;
            }
        }
    </style>
</head>
<body>

    <div class="toast-container" id="toastContainer"></div>
    <div class="overlay" id="mobileOverlay"></div>

    <!-- PHOTO LIGHTBOX -->
    <div class="lightbox" id="lightbox">
        <button class="lb-download-btn" id="lbDownloadBtn" title="Download Image"><i class="fas fa-download"></i></button>
        <button class="lb-close-btn" onclick="closeLB()">✕</button>
        <button class="lb-nav-btn lb-nav-prev" onclick="lbNav(-1)"><i class="fas fa-chevron-left"></i></button>
        <button class="lb-nav-btn lb-nav-next" onclick="lbNav(1)"><i class="fas fa-chevron-right"></i></button>
        <div class="lb-image-wrap" id="lbImageWrap"><img id="lbImage" src="" alt=""></div>
        <div class="lb-counter-text" id="lbCounter"></div>
        <div class="lb-action-bar">
            <button id="lbCopyBtn"><i class="fas fa-link"></i> Copy Link</button>
        </div>
    </div>

    <!-- DOC FULL LIGHTBOX -->
    <div class="doc-lightbox-full" id="docFullLightbox">
        <div class="doc-header">
            <span class="doc-title" id="docFullTitle">Document</span>
            <div class="doc-actions" style="display:flex;gap:12px;align-items:center;">
                <button class="doc-download-btn" id="docFullDownloadBtn"><i class="fas fa-download"></i> Download</button>
                <button class="doc-close-btn" onclick="closeDocFullLB()">✕</button>
            </div>
        </div>
        <iframe class="doc-content" id="docFullIframe" src=""></iframe>
    </div>

    <!-- NAVBAR -->
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
            <span id="desktopAuthBtns">
                <button class="nav-btn" onclick="showAuth('login')">Log In</button>
                <button class="nav-btn primary" onclick="showAuth('signup')">Sign Up</button>
            </span>
            <span class="profile-chip hidden" id="profileChip">
                <span id="profileEmailText"></span>
                <i class="fas fa-chevron-down" style="font-size:0.7rem;"></i>
            </span>
            <div class="profile-dropdown" id="profileDropdown">
                <a onclick="doLogout()"><i class="fas fa-sign-out-alt"></i> Logout</a>
            </div>
            <button class="hamburger" id="hamburgerBtn"><span></span><span></span><span></span></button>
        </div>
    </nav>

    <!-- MOBILE MENU -->
    <div class="mobile-menu" id="mobileMenu">
        <a onclick="navigateTo('home')"><i class="fas fa-home fa-fw"></i> Home</a>
        <a onclick="navigateTo('gallery')"><i class="fas fa-image fa-fw"></i> Photos</a>
        <a onclick="navigateTo('videos')"><i class="fas fa-video fa-fw"></i> Videos</a>
        <a onclick="navigateTo('documents')"><i class="fas fa-file-alt fa-fw"></i> Documents</a>
        <a onclick="navigateTo('about')"><i class="fas fa-info-circle fa-fw"></i> Contact</a>
        <hr class="mobile-divider">
        <div id="mobileLoggedOut">
            <a onclick="showAuth('login')"><i class="fas fa-sign-in-alt fa-fw"></i> Log In</a>
            <a onclick="showAuth('signup')" style="color: var(--gold);"><i class="fas fa-user-plus fa-fw"></i> Sign Up</a>
        </div>
        <div id="mobileLoggedIn" class="hidden">
            <a onclick="doLogout()"><i class="fas fa-sign-out-alt fa-fw"></i> Logout</a>
        </div>
    </div>

    <!-- MAIN CONTENT -->
    <div class="main-content">
        <!-- HOME -->
        <div class="page show" id="page-home">
            <div class="hero-section">
                <h1 class="hero-title">princexit_</h1>
                <p class="hero-subtitle">Photography • Cinematography • Creative</p>
            </div>
            <div class="live-section" id="liveSection">
                <div class="live-header">
                    <div class="live-header-left">
                        <span class="live-badge offline" id="liveBadge"><i class="fas fa-circle"></i> OFFLINE</span>
                        <h3 style="font-size:1.3rem;font-weight:600;">Live Broadcast</h3>
                    </div>
                </div>
                <div class="live-video-container" id="liveVideoContainer">
                    <div class="coming-soon-overlay" id="liveOverlay">
                        <i class="fas fa-video-slash"></i>
                        <h3>STREAM OFFLINE</h3>
                        <p style="color:#666;">Waiting for host...</p>
                    </div>
                </div>
            </div>
            <div class="quick-links">
                <div class="quick-link-card" onclick="navigateTo('gallery')"><i class="fas fa-camera-retro"></i><span>Photos</span></div>
                <div class="quick-link-card" onclick="navigateTo('videos')"><i class="fas fa-film"></i><span>Videos</span></div>
                <div class="quick-link-card" onclick="navigateTo('documents')"><i class="fas fa-folder-open"></i><span>Documents</span></div>
            </div>
        </div>

        <!-- PHOTOS -->
        <div class="page" id="page-gallery">
            <h2 class="section-title"><i class="fas fa-images" style="color:var(--gold);"></i> Photos</h2>
            <div class="add-media-bar" id="photoAddBar" style="display:none;">
                <button class="add-media-btn" onclick="openAddMediaModal('photo')"><i class="fas fa-plus-circle"></i> Add Photo</button>
                <span class="media-count-badge" id="photoCountBadge">0 photos</span>
            </div>
            <div class="search-container"><i class="fas fa-search"></i><input type="text" id="searchPhotos" placeholder="Search photos..." onkeyup="renderPhotos()"></div>
            <div class="gallery-grid" id="photoGrid"></div>
        </div>

        <!-- VIDEOS -->
        <div class="page" id="page-videos">
            <h2 class="section-title"><i class="fas fa-play-circle" style="color:var(--gold);"></i> Videos</h2>
            <div class="add-media-bar" id="videoAddBar" style="display:none;">
                <button class="add-media-btn" onclick="openAddMediaModal('video')"><i class="fas fa-plus-circle"></i> Add Video</button>
                <span class="media-count-badge" id="videoCountBadge">0 videos</span>
            </div>
            <div class="search-container"><i class="fas fa-search"></i><input type="text" id="searchVideos" placeholder="Search videos..." onkeyup="renderVideos()"></div>
            <div class="video-feed" id="videoFeed"></div>
        </div>

        <!-- DOCUMENTS -->
        <div class="page" id="page-documents">
            <h2 class="section-title"><i class="fas fa-file-pdf" style="color:var(--gold);"></i> Documents</h2>
            <div class="add-media-bar" id="docAddBar" style="display:none;">
                <button class="add-media-btn" onclick="openAddMediaModal('doc')"><i class="fas fa-plus-circle"></i> Add Document</button>
                <span class="media-count-badge" id="docCountBadge">0 docs</span>
            </div>
            <div class="search-container"><i class="fas fa-search"></i><input type="text" id="searchDocs" placeholder="Search documents..." onkeyup="renderDocs()"></div>
            <div class="doc-list" id="docList"></div>
        </div>

        <!-- CONTACT -->
        <div class="page" id="page-about">
            <div style="text-align:center;padding:4rem 2rem;background:var(--surface);border-radius:var(--radius);border:1px solid var(--border);max-width:600px;margin:0 auto;">
                <h2 style="color:var(--gold);font-size:2rem;margin-bottom:1rem;">Get in Touch</h2>
                <p style="color:var(--dim);margin-bottom:2rem;">princekvishwakarma@yahoo.com</p>
                <div style="font-size:1.8rem;">
                    <a href="https://instagram.com/princexit_" target="_blank" style="color:#fff;"><i class="fab fa-instagram"></i></a>
                </div>
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
            <span class="forgot-link" id="forgotPassBtn" onclick="showAuth('reset')">Forgot Password?</span>
            <button class="modal-submit" id="authSubmit">Log In</button>
            <p style="text-align:center;margin-top:1.5rem;font-size:0.9rem;color:var(--dim);" id="authSwitch">
                New here? <span class="modal-link" id="swLink" onclick="showAuth('signup')">Create account</span>
            </p>
        </div>
    </div>

    <!-- ADD MEDIA MODAL -->
    <div class="modal-backdrop" id="addMediaModal">
        <div class="modal-dialog">
            <button class="modal-close" onclick="closeModal('addMediaModal')">✕</button>
            <h2 id="addMediaTitle">Add Media Link</h2>
            <p class="modal-subtitle">Paste a direct link (Google Drive, YouTube, image URL, etc.)</p>
            <label>Title <span style="color:#e74c3c;">*</span></label>
            <input type="text" id="addMediaName" placeholder="e.g., Sunset Portrait">
            <label>Link / URL <span style="color:#e74c3c;">*</span></label>
            <textarea id="addMediaUrl" placeholder="Paste your link here..." rows="3"></textarea>
            <button class="modal-submit" id="addMediaSubmit">Add Media</button>
            <input type="hidden" id="addMediaType" value="photo">
        </div>
    </div>

    <script>
        // ==========================================
        // SUPABASE + ADMIN
        // ==========================================
        const SB = window.supabase.createClient(
            'https://wvlvamuehbyfdsozjczk.supabase.co',
            'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Ind2bHZhbXVlaGJ5ZmRzb3pqY3prIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzU1NTM4MDAsImV4cCI6MjA5MTEyOTgwMH0.oaF4wymSu0ePwQSp3moV0sKZVgz5f50ILun5iaU816A'
        );
        const ADMIN_EMAIL = "helloworldd1224@gmail.com";

        let USER = null,
            AUTH_MODE = 'login';
        let ALL_PHOTOS = [],
            ALL_VIDEOS = [],
            ALL_DOCS = [];

        // ============ TOAST ============
        function TOAST(m, t = 'info') {
            const b = document.getElementById('toastContainer');
            const d = document.createElement('div');
            d.className = 'toast ' + t;
            d.innerHTML = (t === 'success' ? '<i class="fas fa-check-circle" style="color:#2ecc71;margin-right:8px;"></i>' :
                t === 'error' ? '<i class="fas fa-exclamation-circle" style="color:#e74c3c;margin-right:8px;"></i>' :
                '<i class="fas fa-info-circle" style="color:#3498db;margin-right:8px;"></i>') + m;
            b.appendChild(d);
            setTimeout(() => {
                d.style.animation = 'toastIn 0.4s ease reverse forwards';
                setTimeout(() => d.remove(), 400);
            }, 3500);
        }

        function isAdmin() { return USER && USER.email === ADMIN_EMAIL; }

        function updateAdminUI() {
            const admin = isAdmin();
            document.getElementById('photoAddBar').style.display = admin ? 'flex' : 'none';
            document.getElementById('videoAddBar').style.display = admin ? 'flex' : 'none';
            document.getElementById('docAddBar').style.display = admin ? 'flex' : 'none';
            renderPhotos();
            renderVideos();
            renderDocs();
        }

        // ============ URL PROCESSING ============
        function extractDriveId(url) {
            const m = url.match(/\/d\/([a-zA-Z0-9_-]+)/) || url.match(/id=([a-zA-Z0-9_-]+)/);
            return m ? m[1] : null;
        }

        function isYouTube(url) { return /(youtube\.com|youtu\.be)/i.test(url); }

        function getYouTubeEmbed(url) {
            const m = url.match(/(?:v=|youtu\.be\/|embed\/|shorts\/)([a-zA-Z0-9_-]{11})/);
            return m ? `https://www.youtube.com/embed/${m[1]}` : url;
        }

        function isVimeo(url) { return /vimeo\.com/i.test(url); }

        function getVimeoEmbed(url) {
            const m = url.match(/vimeo\.com\/(\d+)/);
            return m ? `https://player.vimeo.com/video/${m[1]}` : url;
        }

        function processMediaUrl(url, type) {
            const driveId = extractDriveId(url);
            if (driveId) {
                if (type === 'photo') {
                    return {
                        displayUrl: `https://drive.google.com/uc?export=view&id=${driveId}`,
                            downloadUrl: `https://drive.google.com/uc?export=download&id=${driveId}`,
                            originalLink: `https://drive.google.com/file/d/${driveId}/view`,
                            isDrive: true
                    };
                } else if (type === 'video') {
                    return {
                        displayUrl: `https://drive.google.com/file/d/${driveId}/preview`,
                            downloadUrl: `https://drive.google.com/uc?export=download&id=${driveId}`,
                            originalLink: `https://drive.google.com/file/d/${driveId}/view`,
                            isDrive: true
                    };
                } else {
                    return {
                        displayUrl: `https://drive.google.com/file/d/${driveId}/preview`,
                            downloadUrl: `https://drive.google.com/uc?export=download&id=${driveId}`,
                            originalLink: `https://drive.google.com/file/d/${driveId}/view`,
                            isDrive: true
                    };
                }
            }
            if (type === 'video' && isYouTube(url)) {
                const embed = getYouTubeEmbed(url);
                return { displayUrl: embed, downloadUrl: url, originalLink: url, isYouTube: true };
            }
            if (type === 'video' && isVimeo(url)) {
                const embed = getVimeoEmbed(url);
                return { displayUrl: embed, downloadUrl: url, originalLink: url, isVimeo: true };
            }
            return { displayUrl: url, downloadUrl: url, originalLink: url, isDirect: true };
        }

        // ============ SUPABASE DB FUNCTIONS ============
        async function fetchAllMedia() {
            const { data, error } = await SB.from('media').select('*').order('created_at', { ascending: false });
            if (error) {
                if (error.code === 'PGRST205') {
                    TOAST('Table "media" not found. Run the SQL setup in Supabase SQL Editor.', 'error');
                } else {
                    TOAST('Error loading media: ' + error.message, 'error');
                }
                return [];
            }
            return data || [];
        }

        async function addMediaToDB(type, title, url) {
            const { data, error } = await SB.from('media').insert([{ type, title, url }]).select();
            if (error) {
                TOAST(error.message || 'Failed to add', 'error');
                return null;
            }
            return data;
        }

        async function deleteMediaFromDB(id) {
            const { error } = await SB.from('media').delete().eq('id', id);
            if (error) {
                TOAST(error.message || 'Delete failed', 'error');
                return false;
            }
            return true;
        }

        async function loadAllMediaFromDB() {
            const all = await fetchAllMedia();
            ALL_PHOTOS = [];
            ALL_VIDEOS = [];
            ALL_DOCS = [];
            all.forEach(item => {
                const p = processMediaUrl(item.url, item.type);
                const obj = {
                    id: item.id,
                    title: item.title,
                    displayUrl: p.displayUrl,
                    downloadUrl: p.downloadUrl,
                    originalLink: p.originalLink,
                    type: item.type,
                    isYouTube: p.isYouTube || false,
                    isVimeo: p.isVimeo || false,
                    isDrive: p.isDrive || false
                };
                if (item.type === 'photo') ALL_PHOTOS.push(obj);
                else if (item.type === 'video') ALL_VIDEOS.push(obj);
                else ALL_DOCS.push(obj);
            });
            updateCountBadges();
            renderPhotos();
            renderVideos();
            renderDocs();
        }

        function updateCountBadges() {
            document.getElementById('photoCountBadge').textContent =
                ALL_PHOTOS.length + ' photo' + (ALL_PHOTOS.length !== 1 ? 's' : '');
            document.getElementById('videoCountBadge').textContent =
                ALL_VIDEOS.length + ' video' + (ALL_VIDEOS.length !== 1 ? 's' : '');
            document.getElementById('docCountBadge').textContent =
                ALL_DOCS.length + ' doc' + (ALL_DOCS.length !== 1 ? 's' : '');
        }

        // ============ ADD MEDIA MODAL ============
        function openAddMediaModal(type) {
            if (!isAdmin()) return TOAST('Only admin can add media', 'error');
            document.getElementById('addMediaType').value = type;
            const labels = { photo: 'Photo', video: 'Video', doc: 'Document' };
            document.getElementById('addMediaTitle').textContent = 'Add ' + labels[type] + ' Link';
            document.getElementById('addMediaName').value = '';
            document.getElementById('addMediaUrl').value = '';
            document.getElementById('addMediaModal').classList.add('show');
            setTimeout(() => document.getElementById('addMediaName').focus(), 300);
        }

        document.getElementById('addMediaSubmit').onclick = async () => {
            const type = document.getElementById('addMediaType').value;
            const title = document.getElementById('addMediaName').value.trim();
            const url = document.getElementById('addMediaUrl').value.trim();
            if (!title) return TOAST('Enter a title', 'error');
            if (!url) return TOAST('Paste a link', 'error');
            if (!url.startsWith('http') && !url.includes('drive.google.com') && !url.includes('youtu')) {
                return TOAST('Enter a valid URL', 'error');
            }
            const result = await addMediaToDB(type, title, url);
            if (result) {
                TOAST('Added!', 'success');
                closeModal('addMediaModal');
                await loadAllMediaFromDB();
            }
        };

        // ============ AUTH ============
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
            USER = u;
            const loggedIn = !!u;
            document.getElementById('desktopAuthBtns').classList.toggle('hidden', loggedIn);
            document.getElementById('profileChip').classList.toggle('hidden', !loggedIn);
            document.getElementById('mobileLoggedOut').classList.toggle('hidden', loggedIn);
            document.getElementById('mobileLoggedIn').classList.toggle('hidden', !loggedIn);
            if (u) document.getElementById('profileEmailText').textContent = u.email.split('@')[0];
            updateAdminUI();
        }

        function showAuth(mode) {
            AUTH_MODE = mode;
            const title = document.getElementById('authTitle');
            const submit = document.getElementById('authSubmit');
            const switchEl = document.getElementById('authSwitch');
            const forgot = document.getElementById('forgotPassBtn');
            const emailInp = document.getElementById('authEmail');
            const passInp = document.getElementById('authPass');

            emailInp.style.display = 'block';
            passInp.style.display = 'block';
            forgot.style.display = 'none';
            emailInp.value = '';
            passInp.value = '';

            if (mode === 'login') {
                title.textContent = 'Welcome Back';
                submit.textContent = 'Log In';
                switchEl.innerHTML =
                    'New here? <span class="modal-link" onclick="showAuth(\'signup\')">Create account</span>';
                forgot.style.display = 'block';
            } else if (mode === 'signup') {
                title.textContent = 'Create Account';
                submit.textContent = 'Sign Up';
                switchEl.innerHTML =
                    'Have account? <span class="modal-link" onclick="showAuth(\'login\')">Log In</span>';
            } else if (mode === 'reset') {
                title.textContent = 'Reset Password';
                submit.textContent = 'Send Reset Link';
                passInp.style.display = 'none';
                switchEl.innerHTML = '<span class="modal-link" onclick="showAuth(\'login\')">Back to Login</span>';
            }
            document.getElementById('authModal').classList.add('show');
        }

        function closeModal(id) {
            document.getElementById(id).classList.remove('show');
        }

        document.getElementById('authSubmit').onclick = async () => {
            const email = document.getElementById('authEmail').value.trim();
            const pass = document.getElementById('authPass').value.trim();
            if (AUTH_MODE !== 'reset' && !email) return TOAST('Enter email', 'error');
            if (AUTH_MODE !== 'reset' && !pass) return TOAST('Enter password', 'error');
            if (AUTH_MODE === 'reset' && !email) return TOAST('Enter email', 'error');

            document.getElementById('authSubmit').textContent = 'Please wait...';
            try {
                if (AUTH_MODE === 'reset') {
                    const { error } = await SB.auth.resetPasswordForEmail(email);
                    if (error) throw error;
                    TOAST('Reset link sent! Check your email.', 'success');
                    closeModal('authModal');
                    return;
                }
                const r = AUTH_MODE === 'signup' ?
                    await SB.auth.signUp({ email, password: pass }) :
                    await SB.auth.signInWithPassword({ email, password: pass });
                if (r.error) throw r.error;
                if (AUTH_MODE === 'signup' && r.data.user && !r.data.session) {
                    TOAST('Check your email for confirmation link!', 'success');
                } else {
                    TOAST(AUTH_MODE === 'signup' ? 'Account created!' : 'Logged in!', 'success');
                }
                closeModal('authModal');
                updateUI(r.data.user);
                await loadAllMediaFromDB();
            } catch (e) {
                TOAST(e.message || 'Error', 'error');
            } finally {
                document.getElementById('authSubmit').textContent =
                    AUTH_MODE === 'login' ? 'Log In' : AUTH_MODE === 'signup' ? 'Sign Up' : 'Send Reset Link';
            }
        };

        async function doLogout() {
            await SB.auth.signOut();
            document.getElementById('profileDropdown').classList.remove('show');
            ALL_PHOTOS = [];
            ALL_VIDEOS = [];
            ALL_DOCS = [];
            updateCountBadges();
            renderPhotos();
            renderVideos();
            renderDocs();
            TOAST('Logged out', 'info');
        }

        // ============ NAVIGATION ============
        function navigateTo(page, push = true) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('show'));
            const target = document.getElementById('page-' + page);
            if (target) target.classList.add('show');
            document.querySelectorAll('#desktopNavLinks a').forEach(a => a.classList.remove('active'));
            const link = document.querySelector(`a[data-page="${page}"]`);
            if (link) link.classList.add('active');
            if (push) history.pushState({ page }, "", "#" + page);
            document.getElementById('mobileMenu').classList.remove('open');
            document.getElementById('mobileOverlay').classList.remove('show');
            window.scrollTo({ top: 0, behavior: 'smooth' });
            updateAdminUI();
        }
        window.onpopstate = (e) => {
            if (document.getElementById('lightbox').classList.contains('show')) { closeLB(); return; }
            if (document.getElementById('docFullLightbox').classList.contains('show')) { closeDocFullLB(); return; }
            if (document.getElementById('authModal').classList.contains('show')) { closeModal('authModal'); return; }
            if (document.getElementById('addMediaModal').classList.contains('show')) { closeModal(
                'addMediaModal'); return; }
            navigateTo(e.state?.page || 'home', false);
        };

        // ============ RENDER PHOTOS ============
        function renderPhotos() {
            const q = (document.getElementById('searchPhotos')?.value || '').toLowerCase();
            const filtered = ALL_PHOTOS.filter(p => (p.title || '').toLowerCase().includes(q));
            const grid = document.getElementById('photoGrid');
            if (ALL_PHOTOS.length === 0) {
                grid.innerHTML =
                    '<div style="text-align:center;padding:4rem;grid-column:1/-1;background:var(--surface);border-radius:14px;border:1px solid var(--border);color:var(--dim);"><i class="fas fa-images" style="font-size:3rem;margin-bottom:1rem;display:block;"></i>No photos yet</div>';
                return;
            }
            if (!filtered.length) {
                grid.innerHTML =
                    '<div style="text-align:center;padding:2rem;grid-column:1/-1;color:var(--dim);">No match</div>';
                return;
            }
            const admin = isAdmin();
            grid.innerHTML = filtered.map((p, i) => {
                const idx = ALL_PHOTOS.indexOf(p);
                return `
            <div class="gallery-item" onclick="openLB(${idx})">
              <img src="${p.displayUrl}" loading="lazy" alt="${p.title}" onerror="this.style.opacity='0.3'">
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

        // ============ RENDER VIDEOS ============
        function renderVideos() {
            const q = (document.getElementById('searchVideos')?.value || '').toLowerCase();
            const filtered = ALL_VIDEOS.filter(v => (v.title || '').toLowerCase().includes(q));
            const feed = document.getElementById('videoFeed');
            if (ALL_VIDEOS.length === 0) {
                feed.innerHTML =
                    '<div style="text-align:center;padding:4rem;background:var(--surface);border-radius:14px;border:1px solid var(--border);color:var(--dim);"><i class="fas fa-video" style="font-size:3rem;margin-bottom:1rem;display:block;"></i>No videos yet</div>';
                return;
            }
            if (!filtered.length) {
                feed.innerHTML = '<div style="text-align:center;padding:2rem;color:var(--dim);">No match</div>';
                return;
            }
            const admin = isAdmin();
            feed.innerHTML = filtered.map(v => {
                return `
            <div class="video-card-yt">
              <div class="video-thumb-yt"><iframe src="${v.displayUrl}" allowfullscreen loading="lazy"></iframe></div>
              <div class="video-info-yt">
                <h3>${v.title}</h3>
                <div class="video-meta">${v.isYouTube?'YouTube':v.isVimeo?'Vimeo':'Video'}</div>
                <div class="video-actions-yt">
                  <button class="primary-btn-yt" onclick="downloadMedia('${v.downloadUrl.replace(/'/g,"\\'")}','${v.title.replace(/'/g,"\\'")}')"><i class="fas fa-download"></i> Download</button>
                  <button onclick="navigator.clipboard.writeText('${v.originalLink}');TOAST('Link copied','success')"><i class="fas fa-share"></i> Share</button>
                  ${admin ? `<button onclick="deleteMediaById('${v.id}')" style="color:#e74c3c;"><i class="fas fa-trash"></i> Remove</button>` : ''}
                </div>
              </div>
            </div>`;
            }).join('');
        }

        // ============ RENDER DOCS ============
        function renderDocs() {
            const q = (document.getElementById('searchDocs')?.value || '').toLowerCase();
            const filtered = ALL_DOCS.filter(d => (d.title || '').toLowerCase().includes(q));
            const list = document.getElementById('docList');
            if (ALL_DOCS.length === 0) {
                list.innerHTML =
                    '<div style="text-align:center;padding:4rem;background:var(--surface);border-radius:14px;border:1px solid var(--border);color:var(--dim);"><i class="fas fa-file-alt" style="font-size:3rem;margin-bottom:1rem;display:block;"></i>No documents yet</div>';
                return;
            }
            if (!filtered.length) {
                list.innerHTML = '<div style="text-align:center;padding:2rem;color:var(--dim);">No match</div>';
                return;
            }
            const admin = isAdmin();
            list.innerHTML = filtered.map(d => {
                let icon = 'fa-file';
                const t = d.title.toLowerCase();
                if (t.includes('pdf')) icon = 'fa-file-pdf';
                else if (t.includes('doc')) icon = 'fa-file-word';
                else if (t.includes('xls') || t.includes('sheet')) icon = 'fa-file-excel';
                else if (t.includes('ppt') || t.includes('slide')) icon = 'fa-file-powerpoint';
                return `
            <div class="doc-item">
              <div class="doc-info"><i class="fas ${icon}"></i><span title="${d.title}">${d.title}</span></div>
              <div class="doc-actions-group">
                <button class="nav-btn primary" onclick="openDocFull('${d.displayUrl}','${d.title.replace(/'/g,"\\'")}')"><i class="fas fa-eye"></i> View</button>
                <button class="nav-btn" onclick="downloadMedia('${d.downloadUrl.replace(/'/g,"\\'")}','${d.title.replace(/'/g,"\\'")}')"><i class="fas fa-download"></i></button>
                ${admin ? `<button class="nav-btn" onclick="deleteMediaById('${d.id}')" style="color:#e74c3c;"><i class="fas fa-trash"></i></button>` : ''}
              </div>
            </div>`;
            }).join('');
        }

        // ============ DOWNLOAD (STAYS ON-SITE) ============
        function downloadMedia(url, filename) {
            // Use fetch to download via browser without leaving the site
            const a = document.createElement('a');
            a.href = url;
            a.download = filename || '';
            a.target = '_blank';
            a.rel = 'noopener';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            TOAST('Downloading...', 'success');
        }

        // ============ DELETE ============
        async function deleteMediaById(id) {
            if (!isAdmin()) return TOAST('Only admin can delete', 'error');
            if (!confirm('Delete this media permanently?')) return;
            const ok = await deleteMediaFromDB(id);
            if (ok) {
                TOAST('Deleted', 'success');
                await loadAllMediaFromDB();
            }
        }

        // ============ LIGHTBOX ============
        let LB_IDX = 0;

        function openLB(idx) {
            if (!ALL_PHOTOS.length) return;
            LB_IDX = idx;
            updateLB();
            document.getElementById('lightbox').classList.add('show');
            document.body.classList.add('no-scroll');
        }

        function closeLB() {
            document.getElementById('lightbox').classList.remove('show');
            document.body.classList.remove('no-scroll');
        }

        function updateLB() {
            const p = ALL_PHOTOS[LB_IDX];
            if (!p) return;
            document.getElementById('lbImage').src = p.displayUrl;
            document.getElementById('lbCounter').textContent = `${LB_IDX+1} / ${ALL_PHOTOS.length} - ${p.title}`;
        }

        function lbNav(dir) {
            if (ALL_PHOTOS.length <= 1) return;
            LB_IDX = (LB_IDX + dir + ALL_PHOTOS.length) % ALL_PHOTOS.length;
            updateLB();
        }
        document.getElementById('lbDownloadBtn').onclick = () => {
            const p = ALL_PHOTOS[LB_IDX];
            if (p) downloadMedia(p.downloadUrl, p.title);
        };
        document.getElementById('lbCopyBtn').onclick = () => {
            const p = ALL_PHOTOS[LB_IDX];
            if (p) { navigator.clipboard.writeText(p.originalLink);
                TOAST('Link copied', 'success'); }
        };

        // Swipe
        const lbWrap = document.getElementById('lbImageWrap');
        let sx = 0,
            sy = 0;
        lbWrap.addEventListener('touchstart', e => {
            if (e.touches.length) { sx = e.touches[0].clientX;
                sy = e.touches[0].clientY;
                lbWrap.style.transition = 'none'; }
        }, { passive: true });
        lbWrap.addEventListener('touchmove', e => {
            if (e.touches.length) {
                const dx = e.touches[0].clientX - sx,
                    dy = e.touches[0].clientY - sy;
                if (dy > 0 && Math.abs(dy) > Math.abs(dx)) lbWrap.style.transform =
                    `translateY(${dy}px) scale(${1-dy/2000})`;
                else if (Math.abs(dx) > Math.abs(dy)) lbWrap.style.transform = `translateX(${dx}px)`;
            }
        }, { passive: true });
        lbWrap.addEventListener('touchend', e => {
            lbWrap.style.transition = 'transform 0.3s';
            if (e.changedTouches.length) {
                const dx = e.changedTouches[0].clientX - sx,
                    dy = e.changedTouches[0].clientY - sy;
                if (dy > 120) closeLB();
                else if (Math.abs(dx) > 60) lbNav(dx > 0 ? -1 : 1);
                else lbWrap.style.transform = '';
            }
        });

        // ============ DOC FULL VIEWER ============
        function openDocFull(url, title) {
            document.getElementById('docFullTitle').textContent = title;
            document.getElementById('docFullIframe').src = url;
            document.getElementById('docFullLightbox').classList.add('show');
            document.body.classList.add('no-scroll');
            document.getElementById('docFullDownloadBtn').onclick = () => downloadMedia(url, title);
        }

        function closeDocFullLB() {
            document.getElementById('docFullLightbox').classList.remove('show');
            document.body.classList.remove('no-scroll');
            document.getElementById('docFullIframe').src = '';
        }

        // ============ CONTEXT MENUS ============
        function toggleMenu(e, id) {
            e.stopPropagation();
            document.querySelectorAll('.context-menu').forEach(m => m.classList.remove('show'));
            document.getElementById(id).classList.add('show');
        }
        document.addEventListener('click', e => {
            if (!e.target.closest('#profileChip') && !e.target.closest('#profileDropdown'))
                document.getElementById('profileDropdown').classList.remove('show');
            if (!e.target.closest('.menu-btn') && !e.target.closest('.context-menu'))
                document.querySelectorAll('.context-menu').forEach(m => m.classList.remove('show'));
            if (e.target.closest('#profileChip')) document.getElementById('profileDropdown').classList.toggle(
            'show');
        });
        document.getElementById('authModal').addEventListener('click', function(e) { if (e.target === this)
            closeModal('authModal'); });
        document.getElementById('addMediaModal').addEventListener('click', function(e) { if (e.target === this)
            closeModal('addMediaModal'); });

        // Mobile
        document.getElementById('hamburgerBtn').onclick = () => {
            document.getElementById('mobileMenu').classList.add('open');
            document.getElementById('mobileOverlay').classList.add('show');
        };
        document.getElementById('mobileOverlay').onclick = () => {
            document.getElementById('mobileMenu').classList.remove('open');
            document.getElementById('mobileOverlay').classList.remove('show');
        };

        // Live Stream
        function initLiveStream() {
            const url = "";
            const badge = document.getElementById('liveBadge');
            const overlay = document.getElementById('liveOverlay');
            const container = document.getElementById('liveVideoContainer');
            if (url && url.trim()) {
                badge.classList.remove('offline');
                badge.innerHTML = '<i class="fas fa-circle"></i> LIVE';
                overlay.style.display = 'none';
                if (!document.getElementById('streamIframe')) {
                    const iframe = document.createElement('iframe');
                    iframe.id = 'streamIframe';
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

        // Init
        window.onload = () => {
            initAuth();
            initLiveStream();
            const hash = window.location.hash.replace('#', '');
            navigateTo(hash || 'home', false);
        };
    </script>
</body>
</html>
# All-in-one
