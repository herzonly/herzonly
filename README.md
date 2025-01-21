<!DOCTYPE html>
<html lang="id" data-theme="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Herza's Portfolio</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        :root {
            --bg-color: #ffffff;
            --text-color: #333333;
            --card-bg: #f5f5f5;
            --hover-color: #e0e0e0;
            --accent-color: #ff8c66;
            --gradient-start: #ff8c66;
            --gradient-end: #ff8c66;
            --notification-bg: rgba(32, 32, 32, 0.75);
            --notification-text: #ffffff;
        }
        [data-theme="dark"] {
            --bg-color: #0f172a;
            --text-color: #e2e8f0;
            --card-bg: #1e293b;
            --hover-color: #334155;
            --accent-color: #3b82f6;
            --gradient-start: #2563eb;
            --gradient-end: #3b82f6;
            --notification-bg: rgba(255, 255, 255, 0.4);
            --notification-text: #000000;
        }
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            transition: all 0.3s ease;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
        }
        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
        }
        .whatsapp-notification {
            display: none;
            position: fixed;
            top: 10px;
            left: 10px;
            right: 10px;
            max-width: 400px;
            background: var(--notification-bg);
            backdrop-filter: blur(500px);
            -webkit-backdrop-filter: blur(500px);
            color: var(--notification-text);
            padding: 12px 15px;
            border-radius: 15px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            z-index: 1000;
            opacity: 0;
            animation: slideIn 0.5s ease forwards, slideOut 0.5s ease forwards 4.5s;
        }
        @keyframes slideIn {
            from { transform: translateY(-100%); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        @keyframes slideOut {
            from { transform: translateY(0); opacity: 1; }
            to { transform: translateY(-100%); opacity: 0; }
        }
        .whatsapp-notification.show { display: block; }
        .notification-content {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        .whatsapp-icon {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            overflow: hidden;
        }
        .whatsapp-icon img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .notification-text-content { flex: 1; }
        .notification-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 2px;
        }
        .notification-name {
            font-weight: 600;
            font-size: 0.95rem;
        }
        .notification-time {
            font-size: 0.75rem;
            opacity: 0.7;
        }
        .notification-text {
            font-size: 0.9rem;
            opacity: 0.9;
        }
        .popup-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: 1000;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        .popup-content {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.3);
            background: var(--card-bg);
            padding: 2rem;
            border-radius: 15px;
            text-align: center;
            z-index: 1001;
            opacity: 0;
            transition: all 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }
        .popup-overlay.active { display: block; opacity: 1; }
        .popup-content.active {
            opacity: 1;
            transform: translate(-50%, -50%) scale(1);
        }
        .popup-text {
            font-size: 1.5rem;
            color: var(--accent-color);
            font-weight: bold;
        }
        header {
            background: linear-gradient(135deg, var(--gradient-start), var(--gradient-end));
            padding: 4rem 2rem;
            text-align: center;
            position: relative;
            margin-bottom: 2rem;
        }
        .theme-toggle {
            position: absolute;
            top: 1rem;
            right: 1rem;
            padding: 0.5rem 1rem;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            background-color: var(--card-bg);
            color: var(--text-color);
            font-size: 0.9rem;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 2rem;
        }
        .about-section {
            background-color: var(--card-bg);
            border-radius: 15px;
            padding: 2rem;
            margin-bottom: 3rem;
            text-align: center;
        }
        .about-section img {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            margin-bottom: 1.5rem;
            border: 4px solid var(--accent-color);
            cursor: pointer;
            transition: transform 0.3s ease;
        }
        .about-section img:hover { transform: scale(1.05); }
        .projects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }
        .project-card {
            background-color: var(--card-bg);
            border-radius: 15px;
            padding: 1.5rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .project-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
        }
        .project-icon {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            color: var(--accent-color);
        }
        .try-me-button {
            display: block;
            width: fit-content;
            margin: 1rem auto 0;
            padding: 0.8rem 1.5rem;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            text-decoration: none;
            font-weight: 500;
            transition: transform 0.3s ease, background-color 0.3s ease;
        }
        .try-me-button:hover {
            transform: translateY(-2px);
            background-color: var(--gradient-end);
        }
        .contact-section {
            margin-top: 3rem;
            text-align: center;
            padding: 2rem;
            background-color: var(--card-bg);
            border-radius: 15px;
        }
        .social-links {
            display: flex;
            justify-content: center;
            gap: 1.5rem;
            margin-top: 1.5rem;
        }
        .social-link {
            display: inline-flex;
            align-items: center;
            padding: 0.8rem 1.5rem;
            border-radius: 25px;
            text-decoration: none;
            color: var(--text-color);
            background-color: var(--hover-color);
            font-weight: 500;
            gap: 0.5rem;
        }
        .social-link:hover {
            transform: translateY(-2px);
            background-color: var(--accent-color);
            color: white;
        }
        h1 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            color: white;
        }
        h2 {
            font-size: 1.8rem;
            margin-bottom: 0.5rem;
            color: var(--accent-color);
        }
        .section-title {
            text-align: center;
            margin-bottom: 2rem;
            font-size: 2rem;
            color: var(--accent-color);
        }
        .short-desc {
            font-weight: bold;
            margin-bottom: 1rem;
            color: var(--accent-color);
        }
        .long-desc {
            font-size: 0.9rem;
            margin-top: 1rem;
        }
        @media (max-width: 768px) {
            .projects-grid { grid-template-columns: 1fr; }
            .social-links { 
                flex-direction: column;
                align-items: center;
            }
            .whatsapp-notification {
                width: 90%;
                right: 5%;
                left: 5%;
            }
        }
    </style>
</head>
<body>
    <div class="whatsapp-notification" id="waNotification">
        <div class="notification-content">
            <div class="whatsapp-icon">
                <img src="https://cdn.notmebot.us.kg/file/149be6d784.jpg" alt="WhatsApp Profile">
            </div>
            <div class="notification-text-content">
                <div class="notification-header">
                    <span class="notification-name">Herza</span>
                    <span class="notification-time">Now</span>
                </div>
                <div class="notification-text">Halo kak, Selamat Datang Di Portofolio ku</div>
            </div>
        </div>
    </div>

    <audio id="notificationSound" preload="auto">
        <source src="https://cdn.notmebot.us.kg/file/a1333018e4.opus" type="audio/opus">
        <source src="https://cdn.notmebot.us.kg/file/a1333018e4.opus" type="audio/ogg; codecs=opus">
        <source src="https://cdn.notmebot.us.kg/file/a1333018e4.mp3" type="audio/mpeg">
    </audio>

    <div class="popup-overlay" id="popupOverlay">
        <div class="popup-content" id="popupContent">
            <div class="popup-text">Hi There, Nice To Meet You :></div>
        </div>
    </div>

    <header>
        <h1>Herza's Portfolio</h1>
        <button class="theme-toggle" onclick="toggleTheme()">
            <i class="fas fa-moon"></i> Toggle Theme
        </button>
    </header>

    <div class="container">
        <div class="about-section">
            <img src="https://cdn.notmebot.us.kg/file/5a13409477.jpg" alt="Profile Picture" onclick="showPopup()">
            <h2>About Me</h2>
            <p>Hey! I'm Herza, a 15-year-old coding enthusiast. While I'm not a professional developer, I love exploring and creating with JavaScript and HTML. Programming is my passion, and I enjoy building various projects to learn and improve my skills.</p>
        </div>

        <h2 class="section-title">My Projects</h2>
        <div class="projects-grid">
            <div class="project-card">
                <i class="fas fa-robot project-icon"></i>
                <h2>NotMeBotz MD</h2>
                <p class="short-desc">WhatsApp Bot Automation Solution</p>
                <p class="long-desc">A powerful WhatsApp bot built with Node.js that helps automate responses and manage group interactions. Features include custom commands, group management, and automated responses.</p>
                <a href="https://mybot
                notmebot.us.kg" class="try-me-button">Try Me</a>
            </div>
            <div class="project-card">
                <i class="fas fa-server project-icon"></i>
                <h2>CDN Server</h2>
                <p class="short-desc">High-Performance Content Delivery Network</p>
                <p class="long-desc">A custom CDN solution designed to deliver content efficiently across different regions. Optimized for fast loading times and reliable content distribution.</p>
                <a href="https://cdn.notmebot.us.kg" class="try-me-button">Try Me</a>
            </div>
            <div class="project-card">
                <i class="fas fa-link project-icon"></i>
                <h2>Shortener URL</h2>
                <p class="short-desc">Simple URL Shortening Service</p>
                <p class="long-desc">A user-friendly URL shortening service that creates compact, shareable links. Includes click tracking and custom alias support.</p>
                <a href="https://shortmyurl.us.kg" class="try-me-button">Try Me</a>
            </div>
            <div class="project-card">
                <i class="fas fa-brain project-icon"></i>
                <h2>CiKo AI</h2>
                <p class="short-desc">Artificial Intelligence Assistant</p>
                <p class="long-desc">An AI-powered assistant that helps with various tasks. Built with modern AI technologies to provide helpful responses and automation capabilities.</p>
                <a href="https://ciko.notmebot.us.kg" class="try-me-button">Try Me</a>
            </div>
        </div>

        <div class="contact-section">
            <h2>Let's Connect!</h2>
            <p>Feel free to reach out to me through any of these platforms:</p>
            <div class="social-links">
                <a href="https://wa.me/6282393307733" class="social-link">
                    <i class="fab fa-whatsapp"></i> WhatsApp
                </a>
                <a href="https://t.me/herzaneyfra" class="social-link">
                    <i class="fab fa-telegram"></i> Telegram
                </a>
                <a href="https://discordapp.com/users/971562068622843917" class="social-link">
                    <i class="fab fa-discord"></i> Discord
                </a>
            </div>
        </div>
    </div>

    <script>
        function showWhatsAppNotification() {
            const notification = document.getElementById('waNotification');
            const sound = document.getElementById('notificationSound');
            notification.classList.add('show');
            sound.play().catch(error => console.log('Audio playback failed:', error));
            setTimeout(() => {
                notification.classList.remove('show');
            }, 5000);
        }

        window.addEventListener('load', () => {
            setTimeout(showWhatsAppNotification, 3000);
        });

        function toggleTheme() {
            const html = document.documentElement;
            if (html.getAttribute('data-theme') === 'dark') {
                html.removeAttribute('data-theme');
            } else {
                html.setAttribute('data-theme', 'dark');
            }
        }
function showPopup() {
            const overlay = document.getElementById('popupOverlay');
            const content = document.getElementById('popupContent');
            overlay.classList.add('active');
            setTimeout(() => {
                content.classList.add('active');
            }, 10);
        }
        function hidePopup() {
            const overlay = document.getElementById('popupOverlay');
            const content = document.getElementById('popupContent');
            content.classList.remove('active');
            setTimeout(() => {
                overlay.classList.remove('active');
            }, 500);
        }
        document.getElementById('popupOverlay').addEventListener('click', function(e) {
            if (e.target === this) {
                hidePopup();
            }
        });
            </script>
</body>
</html>
