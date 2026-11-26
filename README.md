<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Happy Birthday, My Love ❤️</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Canvas Confetti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&family=Montserrat:wght@300;400;500;600&family=Playfair+Display:ital,wght@0,500;0,700;1,400&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        :root {
            --primary: #e8889c;
            --primary-dark: #b84964;
            --accent: #fcd34d;
            --bg-dark: #120914;
        }

        body {
            font-family: 'Montserrat', sans-serif;
            background: linear-gradient(135deg, #18091a 0%, #2a0826 50%, #120914 100%);
            color: #fce7f3;
            overflow-x: hidden;
            touch-action: manipulation;
        }

        .font-serif-custom {
            font-family: 'Playfair Display', serif;
        }

        .font-cursive {
            font-family: 'Dancing Script', cursive;
        }

        /* Floating Hearts, Lilies, Capybara with Balloons & Sparkle Stars Canvas */
        #bgCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        /* Glassmorphism styling */
        .glass-card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 182, 193, 0.18);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }

        /* Shake animation for incorrect password */
        .shake {
            animation: shake 0.4s cubic-bezier(.36,.07,.19,.97) both;
        }

        @keyframes shake {
            10%, 90% { transform: translate3d(-1px, 0, 0); }
            20%, 80% { transform: translate3d(2px, 0, 0); }
            30%, 50%, 70% { transform: translate3d(-4px, 0, 0); }
            40%, 60% { transform: translate3d(4px, 0, 0); }
        }

        /* PAGE SWITCHER & SLIDE ANIMATION STYLES */
        .page-view {
            transition: opacity 0.5s ease-in-out, transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            width: 100%;
        }

        .page-view.hidden-page {
            opacity: 0;
            pointer-events: none;
            position: absolute;
            top: 0;
            left: 0;
            transform: translateX(50px) scale(0.98);
        }

        .page-view.active-page {
            opacity: 1;
            pointer-events: auto;
            position: relative;
            transform: translateX(0) scale(1);
        }

        /* REALISTIC 3D LILIES CAKE STYLING & ANIMATIONS */
        .cake-container {
            position: relative;
            width: 280px;
            height: 250px;
            margin: 0 auto;
            cursor: pointer;
            perspective: 1000px;
        }

        .cake-stand {
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 260px;
            height: 16px;
            background: linear-gradient(to right, #e2e8f0, #cbd5e1, #94a3b8);
            border-radius: 50%;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
        }

        .cake-tier {
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            border-radius: 18px 18px 10px 10px;
            box-shadow: inset 0 -10px 20px rgba(0,0,0,0.25), 0 10px 25px rgba(0,0,0,0.4);
            overflow: visible;
            transition: transform 0.8s cubic-bezier(0.34, 1.56, 0.64, 1);
        }

        .cake-bottom {
            bottom: 12px;
            width: 230px;
            height: 90px;
            background: radial-gradient(circle at 50% 30%, #fbcfe8 0%, #f472b6 65%, #db2777 100%);
            border-bottom: 6px solid #9f1239;
        }

        .cake-top {
            bottom: 102px;
            width: 170px;
            height: 75px;
            background: radial-gradient(circle at 50% 30%, #ffffff 0%, #fce7f3 65%, #f472b6 100%);
            border-bottom: 6px solid #be185d;
        }

        /* Piped Icing Swirls */
        .icing-drip {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 22px;
            background: #ffffff;
            border-radius: 0 0 14px 14px;
            box-shadow: 0 3px 8px rgba(0,0,0,0.15);
        }

        .icing-drip::after {
            content: '';
            position: absolute;
            bottom: -8px;
            left: 10px;
            right: 10px;
            height: 10px;
            background: radial-gradient(circle, #ffffff 60%, transparent 61%);
            background-size: 16px 12px;
        }

        .pearl-border {
            position: absolute;
            bottom: 8px;
            left: 0;
            width: 100%;
            height: 8px;
            background: radial-gradient(circle, #fff 55%, transparent 56%) repeat-x;
            background-size: 14px 14px;
            opacity: 0.9;
        }

        /* Cake Cut Animation when clicked */
        .cake-container.cut .cake-top {
            transform: translateX(-65%) translateY(10px) rotate(-8deg);
        }
        .cake-container.cut .cake-bottom {
            transform: translateX(-35%) translateY(5px) rotate(5deg);
        }
        .cake-container.cut .cake-slice-pulled {
            opacity: 1;
            transform: translateX(35px) translateY(25px) scale(1.05);
        }

        .cake-slice-pulled {
            position: absolute;
            bottom: 30px;
            left: 50%;
            width: 50px;
            height: 80px;
            background: linear-gradient(135deg, #fbcfe8, #f472b6);
            border-radius: 8px;
            opacity: 0;
            transform: translateX(0) translateY(0) scale(0.5);
            transition: all 0.8s cubic-bezier(0.34, 1.56, 0.64, 1);
            z-index: 20;
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
        }

        .candle {
            position: absolute;
            bottom: 177px;
            width: 10px;
            height: 48px;
            background: linear-gradient(to right, #fef08a, #f59e0b, #d97706);
            border-radius: 5px 5px 2px 2px;
            box-shadow: 0 0 10px rgba(251, 191, 36, 0.7);
            z-index: 30;
        }

        .candle-1 { left: 35%; }
        .candle-2 { left: 50%; transform: translateX(-50%); }
        .candle-3 { left: 65%; }

        .flame {
            position: absolute;
            top: -22px;
            left: 50%;
            transform: translateX(-50%);
            width: 16px;
            height: 26px;
            background: radial-gradient(ellipse at bottom, #fef08a 0%, #f97316 60%, rgba(239, 68, 68, 0.8) 100%);
            border-radius: 50% 50% 20% 20%;
            box-shadow: 0 0 16px #f97316, 0 0 30px #fef08a;
            animation: flicker 1.1s infinite alternate ease-in-out;
            transform-origin: center bottom;
        }

        @keyframes flicker {
            0% { transform: translateX(-50%) scale(1) rotate(-3deg); opacity: 0.9; }
            50% { transform: translateX(-50%) scale(1.18) rotate(3deg); opacity: 1; }
            100% { transform: translateX(-50%) scale(0.92) rotate(-2deg); opacity: 0.85; }
        }

        .flame.extinguished {
            display: none !important;
        }

        .smoke {
            position: absolute;
            top: -28px;
            left: 50%;
            transform: translateX(-50%);
            width: 8px;
            height: 8px;
            background: rgba(230, 230, 230, 0.75);
            border-radius: 50%;
            animation: rise 2s forwards ease-out;
            opacity: 0;
        }

        @keyframes rise {
            0% { opacity: 0.85; transform: translateX(-50%) translateY(0) scale(1); }
            100% { opacity: 0; transform: translateX(-50%) translateY(-50px) scale(4); }
        }

        /* Card Flip Effect */
        .flip-card {
            perspective: 1000px;
            height: 180px;
        }

        .flip-card-inner {
            position: relative;
            width: 100%;
            height: 100%;
            text-align: center;
            transition: transform 0.6s cubic-bezier(0.4, 0.2, 0.2, 1);
            transform-style: preserve-3d;
        }

        .flip-card.flipped .flip-card-inner {
            transform: rotateY(180deg);
        }

        .flip-card-front, .flip-card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
            border-radius: 1rem;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1.25rem;
        }

        .flip-card-back {
            transform: rotateY(180deg);
        }

        /* Letter Envelope Animation */
        .letter-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.8s cubic-bezier(0, 1, 0, 1);
        }

        .letter-content.open {
            max-height: 3000px;
            transition: max-height 1.2s cubic-bezier(0.85, 0, 0.15, 1);
        }

        .glow-pulse {
            animation: glowPulse 2s infinite alternate;
        }

        @keyframes glowPulse {
            0% { box-shadow: 0 0 15px rgba(244, 114, 182, 0.4); }
            100% { box-shadow: 0 0 30px rgba(244, 114, 182, 0.8), 0 0 15px rgba(254, 240, 138, 0.6); }
        }

        .animate-float {
            animation: float 3s ease-in-out infinite;
        }
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        .ear-wiggle-left {
            animation: earWiggleL 3s infinite ease-in-out;
            transform-origin: bottom right;
        }
        .ear-wiggle-right {
            animation: earWiggleR 3s infinite ease-in-out;
            transform-origin: bottom left;
        }
        @keyframes earWiggleL {
            0%, 90%, 100% { transform: rotate(0deg); }
            93% { transform: rotate(-10deg); }
            96% { transform: rotate(5deg); }
        }
        @keyframes earWiggleR {
            0%, 90%, 100% { transform: rotate(0deg); }
            93% { transform: rotate(10deg); }
            96% { transform: rotate(-5deg); }
        }
    </style>
</head>
<body class="relative min-h-screen pb-20 select-none">

    <!-- GLOBAL AUDIO ELEMENT FOR BACKGROUND MUSIC -->
    <audio id="bgAudioPlayer" loop preload="auto"></audio>

    <!-- WEBSITE UNLOCK OVERLAY SCREEN -->
    <div id="siteUnlockOverlay" class="fixed inset-0 z-[100] flex items-center justify-center p-4 bg-gradient-to-br from-[#18091a] via-[#2a0826] to-[#120914] backdrop-blur-xl transition-all duration-700">
        <div id="siteUnlockBox" class="glass-card w-full max-w-md p-8 sm:p-10 rounded-3xl border border-rose-300/30 text-rose-100 text-center space-y-6 shadow-2xl relative overflow-hidden">
            
            <div class="relative w-20 h-20 mx-auto flex items-center justify-center">
                <div class="absolute inset-0 bg-rose-500/20 rounded-full blur-xl animate-pulse"></div>
                <div class="w-16 h-16 bg-gradient-to-tr from-rose-500 to-pink-600 rounded-2xl flex items-center justify-center text-amber-200 text-2xl shadow-lg border border-rose-300/40">
                    <i class="fa-solid fa-lock"></i>
                </div>
            </div>

            <div class="space-y-2">
                <h2 class="text-2xl sm:text-3xl font-serif-custom font-bold text-transparent bg-clip-text bg-gradient-to-r from-rose-200 via-pink-300 to-amber-200">
                    A Special Surprise Awaits ❤️
                </h2>
                <p class="text-xs sm:text-sm text-rose-200/70 font-light">
                    Enter passcode to unlock your birthday website!
                </p>
            </div>

            <div class="space-y-4 pt-2">
                <div class="relative">
                    <input type="password" id="sitePasswordInput" placeholder="Enter Passcode" class="w-full bg-rose-950/60 border border-rose-300/30 rounded-2xl px-5 py-3.5 text-center text-lg tracking-widest text-rose-100 placeholder-rose-300/30 focus:outline-none focus:border-rose-400/80 transition shadow-inner" onkeyup="if(event.key==='Enter') unlockWebsite()">
                </div>
                
                <p id="siteUnlockError" class="text-xs text-rose-400 hidden font-medium flex items-center justify-center gap-1">
                    <i class="fa-solid fa-circle-exclamation"></i>
                    <span>Incorrect Passcode! Try again.</span>
                </p>

                <button onclick="unlockWebsite()" class="w-full glow-pulse bg-gradient-to-r from-rose-500 to-pink-600 hover:from-rose-600 hover:to-pink-700 text-white font-semibold py-3.5 rounded-2xl text-sm transition transform active:scale-95 flex items-center justify-center gap-2 shadow-xl">
                    <span>Unlock Website</span>
                    <i class="fa-solid fa-key text-amber-200"></i>
                </button>
            </div>
        </div>
    </div>

    <!-- Background Animated Canvas (Hearts, Lilies, Capybara with Balloons & Sparkle Stars) -->
    <canvas id="bgCanvas"></canvas>

    <!-- Navigation Header & Page Switcher -->
    <div class="fixed top-4 left-0 right-0 z-50 px-4 max-w-4xl mx-auto flex items-center justify-between gap-2 flex-wrap pointer-events-none">
        <!-- Navigation Tabs -->
        <div class="glass-card p-1.5 rounded-full flex items-center gap-1 border border-rose-300/30 shadow-2xl pointer-events-auto bg-rose-950/60 backdrop-blur-md">
            <button id="navHomeBtn" onclick="switchPage('home')" class="px-4 py-1.5 rounded-full text-xs font-semibold transition-all duration-300 bg-gradient-to-r from-rose-500 to-pink-600 text-white shadow-md flex items-center gap-1.5">
                <i class="fa-solid fa-heart text-rose-200"></i>
                <span>Birthday Wish</span>
            </button>
            <button id="navQuizBtn" onclick="switchPage('quiz')" class="px-4 py-1.5 rounded-full text-xs font-semibold transition-all duration-300 text-rose-200 hover:text-white flex items-center gap-1.5">
                <i class="fa-solid fa-gamepad text-pink-300"></i>
                <span>How Well Do You Know Us?</span>
            </button>
        </div>

        <!-- Management Toolbar Buttons -->
        <div class="flex items-center gap-2 pointer-events-auto flex-wrap justify-end">
            <button id="patternManagerBtn" onclick="requestHostAccess(togglePatternModal)" class="glass-card px-3 py-1.5 rounded-full flex items-center gap-1.5 text-xs font-medium border border-rose-300/30 text-rose-200 hover:bg-rose-900/40 transition active:scale-95 shadow-lg">
                <i class="fa-solid fa-wand-magic-sparkles text-amber-300"></i>
                <span class="hidden sm:inline">Pattern</span>
            </button>

            <button id="letterManagerBtn" onclick="requestHostAccess(toggleLetterModal)" class="glass-card px-3 py-1.5 rounded-full flex items-center gap-1.5 text-xs font-medium border border-rose-300/30 text-rose-200 hover:bg-rose-900/40 transition active:scale-95 shadow-lg">
                <i class="fa-solid fa-envelope-open-text text-amber-300"></i>
                <span class="hidden sm:inline">Letter</span>
            </button>

            <button id="reasonsManagerBtn" onclick="requestHostAccess(toggleReasonsModal)" class="glass-card px-3 py-1.5 rounded-full flex items-center gap-1.5 text-xs font-medium border border-rose-300/30 text-rose-200 hover:bg-rose-900/40 transition active:scale-95 shadow-lg">
                <i class="fa-solid fa-heart-circle-plus text-rose-400"></i>
                <span class="hidden sm:inline">Reasons</span>
            </button>

            <button id="quizManagerBtn" onclick="requestHostAccess(toggleQuizModal)" class="glass-card px-3 py-1.5 rounded-full flex items-center gap-1.5 text-xs font-medium border border-rose-300/30 text-rose-200 hover:bg-rose-900/40 transition active:scale-95 shadow-lg">
                <i class="fa-solid fa-clipboard-question text-pink-300"></i>
                <span class="hidden sm:inline">Quiz</span>
            </button>

            <button id="photoManagerBtn" onclick="requestHostAccess(togglePhotoModal)" class="glass-card px-3 py-1.5 rounded-full flex items-center gap-1.5 text-xs font-medium border border-rose-300/30 text-rose-200 hover:bg-rose-900/40 transition active:scale-95 shadow-lg">
                <i class="fa-solid fa-images text-amber-300"></i>
                <span class="hidden sm:inline">Photos</span>
            </button>

            <!-- Visitor Audio Control Toggle -->
            <button id="musicToggle" class="glass-card px-3 py-1.5 rounded-full flex items-center gap-1.5 text-xs font-medium border border-rose-300/30 text-rose-200 hover:bg-rose-900/40 transition active:scale-95 shadow-lg">
                <i id="musicIcon" class="fa-solid fa-music text-rose-400"></i>
                <span id="musicText">Music</span>
            </button>
        </div>
    </div>

    <!-- MAIN CONTAINER WITH PAGE VIEWS -->
    <div class="relative z-10 max-w-4xl mx-auto px-4 pt-20 sm:pt-24 min-h-screen">

        <!-- PAGE 1: HOME / BIRTHDAY MAIN EXPERIENCE -->
        <div id="pageHome" class="page-view active-page space-y-20">

            <!-- HERO SECTION -->
            <section class="text-center space-y-6 pt-2">
                <div class="inline-block px-4 py-1.5 rounded-full glass-card text-rose-300 text-xs sm:text-sm font-medium tracking-widest uppercase mb-2 animate-bounce">
                    ✨ Today Is All About You ✨
                </div>
                
                <h1 class="text-4xl sm:text-6xl md:text-7xl font-bold font-serif-custom leading-tight tracking-wide text-transparent bg-clip-text bg-gradient-to-r from-rose-200 via-pink-300 to-amber-200 drop-shadow-sm">
                    Happy Birthday, <br class="sm:hidden"/>
                    <span id="girlfriendName" class="font-cursive text-5xl sm:text-7xl md:text-8xl text-rose-400 block mt-2 animate-float">My Favorite person Ning Ning❤️</span>
                </h1>

                <p class="max-w-xl mx-auto text-rose-100/80 text-sm sm:text-base font-light px-4 leading-relaxed">
                    I created this little space wrapped in your favorite blooming lilies, just to remind you how deeply loved, valued, and cherished you are every single day.
                </p>

                <div class="pt-4 flex flex-col sm:flex-row items-center justify-center gap-4">
                    <a href="#cake-section" class="glow-pulse inline-flex items-center gap-3 bg-gradient-to-r from-rose-500 to-pink-600 hover:from-rose-600 hover:to-pink-700 text-white font-semibold px-8 py-4 rounded-full shadow-xl transform transition hover:-translate-y-1 active:scale-95">
                        <span>Blow Out Candles</span>
                        <i class="fa-solid fa-cake-candles text-rose-200"></i>
                    </a>

                    <!-- Prominent Button to Switch to Quiz Page -->
                    <button onclick="switchPage('quiz')" class="glass-card inline-flex items-center gap-3 bg-rose-900/30 hover:bg-rose-900/60 border border-rose-300/40 text-rose-100 font-semibold px-8 py-4 rounded-full shadow-xl transform transition hover:-translate-y-1 active:scale-95">
                        <span>How Well Do You Know Us?</span>
                        <i class="fa-solid fa-gamepad text-pink-300"></i>
                    </button>
                </div>
            </section>

            <!-- INTERACTIVE REALISTIC LILIES CAKE SECTION WITH MIC BLOWOUT -->
            <section id="cake-section" class="scroll-mt-10">
                <div class="glass-card rounded-3xl p-6 sm:p-10 text-center relative overflow-hidden">
                    <div class="absolute -top-24 -left-24 w-48 h-48 bg-rose-500/20 rounded-full blur-3xl pointer-events-none"></div>
                    
                    <h2 class="text-2xl sm:text-3xl font-serif-custom font-bold text-rose-200 mb-2">Make A Wish</h2>
                    <p id="cakeInstructions" class="text-xs sm:text-sm text-rose-200/70 mb-4">
                        Blow into your microphone ("fuuu") or tap the realistic lily cake below to cut a slice! 🌸🍰
                    </p>

                    <!-- Mic Control Button -->
                    <div class="mb-6">
                        <button id="micBtn" onclick="initMicBlowout()" class="glass-card px-4 py-2 rounded-full text-xs font-semibold text-rose-200 hover:bg-rose-900/50 border border-rose-400/30 transition flex items-center gap-2 mx-auto">
                            <i class="fa-solid fa-microphone text-rose-400"></i>
                            <span id="micBtnText">Enable Mic Blow Detection</span>
                        </button>
                        <p id="micStatus" class="text-[11px] text-pink-300/70 mt-1 hidden"></p>
                    </div>

                    <!-- Realistic 3D Lilies Birthday Cake -->
                    <div class="py-8">
                        <div id="cake" class="cake-container">
                            <div class="cake-stand"></div>
                            
                            <!-- Candles -->
                            <div class="candle candle-1">
                                <div class="flame"></div>
                            </div>
                            <div class="candle candle-2">
                                <div class="flame"></div>
                            </div>
                            <div class="candle candle-3">
                                <div class="flame"></div>
                            </div>

                            <!-- Top Tier: Frosted White & 3D Lily Blossoms -->
                            <div class="cake-tier cake-top">
                                <div class="icing-drip"></div>
                                <div class="pearl-border"></div>
                                
                                <!-- 3D Realistic Lily Flower on Top -->
                                <div class="absolute top-2 left-1/2 -translate-x-1/2 w-14 h-14 pointer-events-none z-20">
                                    <svg viewBox="0 0 100 100" class="w-full h-full drop-shadow-md">
                                        <g transform="translate(50,50)">
                                            <!-- White Petals -->
                                            <path d="M 0 -35 Q 15 -18 0 0 Q -15 -18 0 -35" fill="#ffffff" opacity="0.95"/>
                                            <path d="M 0 35 Q 15 18 0 0 Q -15 18 0 35" fill="#fdf2f8" opacity="0.95"/>
                                            <path d="M -35 0 Q -18 15 0 0 Q -18 -15 -35 0" fill="#ffffff" opacity="0.95"/>
                                            <path d="M 35 0 Q 18 15 0 0 Q 18 -15 35 0" fill="#fdf2f8" opacity="0.95"/>
                                            <path d="M -25 -25 Q -10 -10 0 0 Q -10 10 -25 -25" fill="#fbcfe8" opacity="0.9"/>
                                            <path d="M 25 25 Q 10 10 0 0 Q 10 -10 25 25" fill="#fbcfe8" opacity="0.9"/>
                                            <!-- Golden Stamens -->
                                            <circle cx="0" cy="0" r="5" fill="#fde047"/>
                                            <line x1="0" y1="0" x2="-8" y2="-12" stroke="#d97706" stroke-width="1.5"/>
                                            <line x1="0" y1="0" x2="8" y2="-12" stroke="#d97706" stroke-width="1.5"/>
                                            <line x1="0" y1="0" x2="-10" y2="4" stroke="#d97706" stroke-width="1.5"/>
                                            <line x1="0" y1="0" x2="10" y2="4" stroke="#d97706" stroke-width="1.5"/>
                                        </g>
                                    </svg>
                                </div>
                            </div>

                            <!-- Bottom Tier: Pink Gradient with Piped Swirls -->
                            <div class="cake-tier cake-bottom">
                                <div class="icing-drip"></div>
                                <div class="pearl-border"></div>
                                <div class="absolute bottom-2 w-full flex justify-around px-6 opacity-80">
                                    <div class="w-4 h-4 rounded-full bg-white shadow-inner"></div>
                                    <div class="w-4 h-4 rounded-full bg-white shadow-inner"></div>
                                    <div class="w-4 h-4 rounded-full bg-white shadow-inner"></div>
                                    <div class="w-4 h-4 rounded-full bg-white shadow-inner"></div>
                                </div>
                            </div>

                            <!-- Cut Cake Slice Pulled Forward -->
                            <div class="cake-slice-pulled">
                                <div class="absolute top-0 w-full h-3 bg-white rounded-t-lg"></div>
                            </div>
                        </div>
                    </div>

                    <!-- Wish Revealed Message -->
                    <div id="wishMessage" class="hidden mt-6 p-6 rounded-2xl bg-rose-950/50 border border-rose-500/30 transition-all duration-700 transform translate-y-4">
                        <i class="fa-solid fa-wand-magic-sparkles text-3xl text-amber-300 mb-3 block animate-bounce"></i>
                        <p class="text-lg sm:text-2xl font-serif-custom italic text-rose-200 mb-2">
                            "Make a wish, my love... mine already came true because I have you."
                        </p>
                        <p class="text-xs sm:text-sm text-pink-300/80">
                            May every single dream you hold in your heart bloom as gracefully as a garden of lilies! ❤️
                        </p>
                    </div>
                </div>
            </section>

            <!-- PHOTO GALLERY SECTION -->
            <section class="space-y-8">
                <div class="text-center space-y-2">
                    <h2 class="text-3xl sm:text-4xl font-serif-custom font-bold text-rose-200">Happiest Birthday To You Once Again</h2>
                    <p class="text-xs sm:text-sm text-rose-200/60">A glimpse of our cherished moments ❤️</p>
                </div>

                <div id="photoGrid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6 pt-4">
                    <!-- Initialized dynamically -->
                </div>
            </section>

            <!-- REASONS WHY YOU ARE SPECIAL SECTION -->
            <section class="space-y-8">
                <div class="text-center space-y-2">
                    <h2 class="text-3xl sm:text-4xl font-serif-custom font-bold text-rose-200">Why You Are So Special</h2>
                    <p class="text-xs sm:text-sm text-rose-200/60">Tap any card to flip and reveal a secret reason</p>
                </div>

                <div id="reasonsGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-6">
                    <!-- Populated dynamically via JavaScript -->
                </div>
            </section>

            <!-- CUTE CAPYBARA WITH LILIES & LETTER SECTION -->
            <section class="space-y-6">
                <div class="text-center space-y-2">
                    <h2 class="text-3xl sm:text-4xl font-serif-custom font-bold text-rose-200">A Secret Letter For You</h2>
                    <p class="text-xs sm:text-sm text-rose-200/60">Tap the capybara's letter to unseal cutie 😉</p>
                </div>

                <!-- CUTE CAPYBARA VECTOR ILLUSTRATION -->
                <div class="relative max-w-xs mx-auto -mb-6 z-20 pointer-events-none animate-float">
                    <svg viewBox="0 0 300 240" class="w-full h-auto drop-shadow-2xl overflow-visible">
                        <path d="M 150 15 C 145 5, 130 5, 130 20 C 130 30, 150 40, 150 45 C 150 40, 170 30, 170 20 C 170 5, 155 5, 150 15 Z" fill="#f43f5e" class="animate-bounce" />
                        
                        <ellipse cx="95" cy="85" rx="12" ry="9" fill="#8c5833" class="ear-wiggle-left" />
                        <ellipse cx="95" cy="85" rx="7" ry="5" fill="#5c381e" class="ear-wiggle-left" />
                        <ellipse cx="205" cy="85" rx="12" ry="9" fill="#8c5833" class="ear-wiggle-right" />
                        <ellipse cx="205" cy="85" rx="7" ry="5" fill="#5c381e" class="ear-wiggle-right" />

                        <path d="M 90 100 C 80 130, 75 180, 85 220 C 110 230, 190 230, 215 220 C 225 180, 220 130, 210 100 C 200 70, 100 70, 90 100 Z" fill="#a66e38" />
                        <path d="M 115 105 C 115 85, 185 85, 185 105 C 185 135, 115 135, 115 105 Z" fill="#b87d43" />
                        <path d="M 130 110 C 130 100, 170 100, 170 110 C 170 125, 130 125, 130 110 Z" fill="#6e4320" />
                        <ellipse cx="143" cy="112" rx="3" ry="5" fill="#3d220f" />
                        <ellipse cx="157" cy="112" rx="3" ry="5" fill="#3d220f" />
                        
                        <path d="M 110 102 Q 118 108 126 102" stroke="#3d220f" stroke-width="3.5" stroke-linecap="round" fill="none" />
                        <path d="M 174 102 Q 182 108 190 102" stroke="#3d220f" stroke-width="3.5" stroke-linecap="round" fill="none" />
                        
                        <ellipse cx="108" cy="118" rx="10" ry="6" fill="#f472b6" opacity="0.6" />
                        <ellipse cx="192" cy="118" rx="10" ry="6" fill="#f472b6" opacity="0.6" />

                        <ellipse cx="115" cy="175" rx="14" ry="10" fill="#8c5833" />
                        <ellipse cx="185" cy="175" rx="14" ry="10" fill="#8c5833" />

                        <g transform="translate(70, 115) scale(0.5)">
                            <path d="M50 80 Q 70 110 90 130" stroke="#4ade80" stroke-width="5" stroke-linecap="round"/>
                            <path d="M50 70 Q 20 40 10 10 Q 40 30 50 70" fill="#ffffff" stroke="#f472b6" stroke-width="2"/>
                            <path d="M50 70 Q 80 40 90 10 Q 60 30 50 70" fill="#ffffff" stroke="#f472b6" stroke-width="2"/>
                            <path d="M50 70 Q 50 20 50 0 Q 50 30 50 70" fill="#fbcfe8" stroke="#f472b6" stroke-width="2"/>
                            <circle cx="50" cy="40" r="5" fill="#fde047" />
                        </g>
                        <g transform="translate(180, 115) scale(0.5) scale(-1, 1)">
                            <path d="M50 80 Q 70 110 90 130" stroke="#4ade80" stroke-width="5" stroke-linecap="round"/>
                            <path d="M50 70 Q 20 40 10 10 Q 40 30 50 70" fill="#ffffff" stroke="#f472b6" stroke-width="2"/>
                            <path d="M50 70 Q 80 40 90 10 Q 60 30 50 70" fill="#ffffff" stroke="#f472b6" stroke-width="2"/>
                            <path d="M50 70 Q 50 20 50 0 Q 50 30 50 70" fill="#fbcfe8" stroke="#f472b6" stroke-width="2"/>
                            <circle cx="50" cy="40" r="5" fill="#fde047" />
                        </g>

                        <circle cx="150" cy="70" r="12" fill="#f97316" />
                        <path d="M 150 58 Q 153 54 156 56" stroke="#15803d" stroke-width="2" fill="none" />
                        <circle cx="147" cy="67" r="1.5" fill="#ffedd5" />
                    </svg>
                </div>

                <!-- SECRET LETTER CONTAINER -->
                <div class="max-w-2xl mx-auto relative z-10">
                    <div id="envelope" class="envelope-wrapper glass-card p-6 sm:p-10 rounded-3xl border border-rose-300/40 text-center relative overflow-hidden cursor-pointer hover:border-rose-200/80 transition duration-500 shadow-2xl" onclick="toggleLetter()">
                        
                        <div id="envelopeClosed" class="space-y-5 py-6 pt-10">
                            <div class="relative w-28 h-28 mx-auto flex items-center justify-center transform transition duration-500 hover:scale-110">
                                <div class="absolute inset-0 bg-gradient-to-tr from-pink-500/30 to-amber-200/30 rounded-full blur-xl"></div>
                                <i class="fa-solid fa-envelope-open-text text-6xl text-rose-300 drop-shadow-md"></i>
                            </div>

                            <p class="font-cursive text-2xl text-rose-200">"A special message from your capybara messenger..."</p>
                            <span class="inline-block text-xs text-pink-300/80 bg-rose-950/70 px-4 py-1.5 rounded-full border border-rose-400/30 shadow-md">
                                Tap to unseal letter ✉️
                            </span>
                        </div>

                        <div id="letterContent" class="letter-content text-left space-y-4">
                            <div class="border-b border-rose-300/20 pb-4 text-center relative">
                                <div class="text-xs text-amber-200/70 tracking-widest uppercase font-light mb-1">❀ Wrapped in Lilies & Love ❀</div>
                                <span id="letterRecipientDisplay" class="font-cursive text-3xl sm:text-4xl text-rose-300">My Dearest Ning Ning,</span>
                            </div>

                            <div id="letterBodyDisplay" class="space-y-4 text-sm sm:text-base leading-relaxed text-rose-100/90 font-light">
                                <!-- Dynamically loaded -->
                            </div>

                            <div class="pt-6 text-right border-t border-rose-300/20 flex items-center justify-between">
                                <div class="text-rose-300/40 text-lg">🌸 🪷 🌸</div>
                                <div>
                                    <p id="letterSignoffDisplay" class="font-cursive text-2xl text-amber-200">Forever & Always,</p>
                                    <p id="letterSenderDisplay" class="text-xs text-rose-300/70 mt-1">Yours Truly ❤️</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
        </div>

        <!-- PAGE 2: QUIZ & GAME PAGE ("HOW WELL DO YOU KNOW US?") -->
        <div id="pageQuiz" class="page-view hidden-page space-y-12">
            <!-- HEADER SECTION -->
            <div class="text-center space-y-4 pt-4">
                <div class="inline-block px-4 py-1.5 rounded-full glass-card text-pink-300 text-xs sm:text-sm font-medium tracking-widest uppercase animate-pulse">
                    🎮 Fun & Games Center
                </div>
                
                <h1 class="text-3xl sm:text-5xl font-bold font-serif-custom text-transparent bg-clip-text bg-gradient-to-r from-rose-200 via-pink-300 to-amber-200">
                    How Well Do You Know Us & Others?
                </h1>
                <p class="max-w-md mx-auto text-rose-200/70 text-xs sm:text-sm">
                    Answer these fun questions to test your knowledge about our favorite memories, tiny details, and secrets!
                </p>
            </div>

            <!-- MAIN QUIZ CARD CONTAINER -->
            <div class="glass-card max-w-xl mx-auto rounded-3xl p-6 sm:p-10 border border-rose-300/30 text-center relative shadow-2xl">
                <div id="quizContainer">
                    <div class="flex items-center justify-between text-xs text-rose-300/70 mb-6 pb-3 border-b border-rose-200/10">
                        <span id="quizProgress" class="font-medium">Question 1 of 3</span>
                        <span id="quizScore" class="font-semibold text-amber-300">Score: 0</span>
                    </div>

                    <h3 id="quizQuestion" class="text-xl sm:text-2xl font-serif-custom text-rose-100 font-semibold mb-8 leading-snug">
                        Loading question...
                    </h3>

                    <div id="quizOptions" class="grid grid-cols-1 gap-3">
                        <!-- Populated dynamically -->
                    </div>

                    <div id="quizFeedback" class="mt-6 p-3.5 rounded-xl text-xs sm:text-sm font-medium hidden transition-all"></div>
                </div>

                <!-- QUIZ COMPLETED SCREEN -->
                <div id="quizResult" class="hidden space-y-6 py-6">
                    <div class="relative w-20 h-20 mx-auto">
                        <div class="absolute inset-0 bg-amber-400/20 rounded-full blur-xl animate-pulse"></div>
                        <i class="fa-solid fa-trophy text-5xl text-amber-300 animate-bounce relative z-10"></i>
                    </div>

                    <h3 class="text-3xl font-serif-custom text-rose-200 font-bold">Quiz Complete!</h3>
                    <p id="quizResultMessage" class="text-sm sm:text-base text-rose-100/90 leading-relaxed"></p>
                    
                    <div class="flex items-center justify-center gap-4 pt-2">
                        <button onclick="restartQuiz()" class="bg-gradient-to-r from-rose-500 to-pink-600 text-white font-semibold text-xs sm:text-sm px-6 py-3 rounded-full shadow-lg hover:from-rose-600 hover:to-pink-700 transition transform active:scale-95">
                            Play Again 🔄
                        </button>
                        <button onclick="switchPage('home')" class="glass-card text-rose-200 hover:text-white font-semibold text-xs sm:text-sm px-6 py-3 rounded-full border border-rose-300/30 transition transform active:scale-95">
                            Back to Birthday Main ✨
                        </button>
                    </div>
                </div>
            </div>

            <!-- FOOTER BACK BUTTON -->
            <div class="text-center pt-6">
                <button onclick="switchPage('home')" class="inline-flex items-center gap-2 text-xs text-rose-300/80 hover:text-rose-100 transition hover:underline">
                    <i class="fa-solid fa-arrow-left"></i>
                    <span>Return to Birthday Wish Page</span>
                </button>
            </div>
        </div>

        <!-- FOOTER -->
        <footer class="text-center pt-16 pb-6 border-t border-rose-900/30 text-rose-300/60 text-xs sm:text-sm space-y-2">
            <p class="font-cursive text-xl text-rose-300">Made with all my heart, surrounded by lilies just for you ✨</p>
            <p>© Happy Birthday, My Love!</p>
        </footer>
    </div>

    <!-- HOST PASSWORD AUTHENTICATION MODAL -->
    <div id="hostAuthModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/85 backdrop-blur-md hidden">
        <div class="glass-card w-full max-w-sm p-6 rounded-3xl border border-rose-300/30 text-rose-100 space-y-4 text-center">
            <div class="w-12 h-12 bg-rose-500/20 border border-rose-400/30 rounded-full flex items-center justify-center mx-auto text-amber-300 text-xl">
                <i class="fa-solid fa-lock"></i>
            </div>
            
            <h3 class="text-lg font-serif-custom font-bold text-rose-200">Host Access Restricted</h3>
            <p class="text-xs text-rose-200/70">Enter host key to customize website content or manage passcode.</p>

            <div class="space-y-3 pt-2">
                <input type="password" id="hostPasswordInput" placeholder="Enter Host Key" class="w-full bg-rose-950/60 border border-rose-300/30 rounded-xl px-4 py-2.5 text-center text-sm text-rose-100 focus:outline-none focus:border-rose-400">
                <p id="hostAuthError" class="text-[11px] text-rose-400 hidden">Incorrect Host Key!</p>
                
                <div class="flex gap-2">
                    <button onclick="closeHostAuthModal()" class="w-1/2 bg-rose-950/60 border border-rose-400/30 text-rose-300 font-medium py-2 rounded-xl text-xs hover:bg-rose-900/40 transition">
                        Cancel
                    </button>
                    <button onclick="submitHostAuth()" class="w-1/2 bg-gradient-to-r from-rose-500 to-pink-600 text-white font-semibold py-2 rounded-xl text-xs hover:from-rose-600 hover:to-pink-700 transition">
                        Unlock
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- PATTERN / STARS & HOST BACKGROUND MUSIC CUSTOMIZATION MODAL -->
    <div id="patternModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden">
        <div class="glass-card w-full max-w-lg p-6 rounded-3xl border border-rose-300/30 max-h-[90vh] overflow-y-auto text-rose-100 space-y-5">
            <div class="flex items-center justify-between border-b border-rose-200/20 pb-4">
                <h3 class="text-xl font-serif-custom font-bold text-rose-200 flex items-center gap-2">
                    <i class="fa-solid fa-wand-magic-sparkles text-amber-300"></i>
                    <span>Pattern & Music Customization</span>
                </h3>
                <button onclick="togglePatternModal()" class="text-rose-300 hover:text-white text-xl">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Stars & Pattern Element Count</label>
                    <input type="range" id="patternCount" min="10" max="80" value="30" class="w-full accent-pink-500">
                    <div class="flex justify-between text-[10px] text-rose-300/60"><span>10 (Sparse)</span><span id="patternCountVal">30</span><span>80 (Dense)</span></div>
                </div>

                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Floating Speed</label>
                    <input type="range" id="patternSpeed" min="1" max="10" value="4" class="w-full accent-pink-500">
                    <div class="flex justify-between text-[10px] text-rose-300/60"><span>Slow</span><span id="patternSpeedVal">4</span><span>Fast</span></div>
                </div>

                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Star & Lily Particle Size</label>
                    <input type="range" id="patternSize" min="5" max="25" value="12" class="w-full accent-pink-500">
                    <div class="flex justify-between text-[10px] text-rose-300/60"><span>Small</span><span id="patternSizeVal">12px</span><span>Large</span></div>
                </div>

                <!-- HOST EXCLUSIVE: BACKGROUND SONG CUSTOMIZATION -->
                <div class="pt-3 border-t border-rose-300/20 space-y-3">
                    <label class="block text-xs font-semibold uppercase tracking-wider text-amber-300 flex items-center gap-1.5">
                        <i class="fa-solid fa-music"></i>
                        <span>Customize Background Song (Host Only)</span>
                    </label>

                    <!-- Option A: Direct Audio URL -->
                    <div>
                        <span class="block text-[11px] text-rose-200/70 mb-1">Option 1: Online Audio Direct URL (.mp3 / .m4a)</span>
                        <div class="flex gap-2">
                            <input type="url" id="musicUrlInput" placeholder="https://example.com/song.mp3" class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl px-3 py-2 text-xs text-rose-100 focus:outline-none focus:border-rose-400">
                            <button onclick="setMusicFromUrl()" class="bg-gradient-to-r from-rose-500 to-pink-600 text-white font-semibold px-4 py-2 rounded-xl text-xs hover:from-rose-600 hover:to-pink-700 transition flex-shrink-0">
                                Apply URL
                            </button>
                        </div>
                    </div>

                    <!-- Option B: Local Gallery Upload -->
                    <div>
                        <span class="block text-[11px] text-rose-200/70 mb-1">Option 2: Choose Audio File from Device / Gallery</span>
                        <input type="file" id="musicFileInput" accept="audio/*" onchange="setMusicFromFile()" class="block w-full text-xs text-rose-300 file:mr-3 file:py-2 file:px-3 file:rounded-xl file:border-0 file:text-xs file:font-semibold file:bg-amber-500/20 file:text-amber-200 hover:file:bg-amber-500/30 transition cursor-pointer">
                    </div>
                </div>

                <!-- HOST EXCLUSIVE: WEBSITE PASSCODE CONFIGURATION -->
                <div class="pt-3 border-t border-rose-300/20">
                    <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Change Website Unlock Passcode (Host Only)</label>
                    <div class="flex gap-2">
                        <input type="password" id="newSitePasscodeInput" placeholder="Set New Passcode" class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl px-3 py-2 text-xs text-rose-100 focus:outline-none">
                        <button onclick="changeSitePasscode()" class="bg-rose-500/20 border border-rose-400/40 text-rose-200 font-semibold px-4 py-2 rounded-xl text-xs hover:bg-rose-500/40 transition flex-shrink-0">
                            Update Passcode
                        </button>
                    </div>
                </div>

                <!-- HOST EXCLUSIVE: HOST KEY CONFIGURATION -->
                <div class="pt-2 border-t border-rose-300/20">
                    <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Host Security Key Configuration</label>
                    <div class="flex gap-2">
                        <input type="password" id="newHostPasswordInput" placeholder="Set New Host Key" class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl px-3 py-2 text-xs text-rose-100 focus:outline-none">
                        <button onclick="changeHostKey()" class="bg-amber-500/20 border border-amber-400/40 text-amber-200 font-semibold px-4 py-2 rounded-xl text-xs hover:bg-amber-500/40 transition flex-shrink-0">
                            Update Key
                        </button>
                    </div>
                </div>

                <div class="flex items-center justify-between pt-2">
                    <button onclick="resetDefaultPattern()" class="text-xs text-amber-300 hover:underline">Reset Defaults</button>
                    <button onclick="savePatternSettings()" class="bg-gradient-to-r from-rose-500 to-pink-600 text-white font-semibold px-6 py-2.5 rounded-xl text-xs hover:from-rose-600 hover:to-pink-700 transition">
                        Save Pattern
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- LETTER CUSTOMIZATION MODAL -->
    <div id="letterModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden">
        <div class="glass-card w-full max-w-lg p-6 rounded-3xl border border-rose-300/30 max-h-[90vh] overflow-y-auto text-rose-100 space-y-5">
            <div class="flex items-center justify-between border-b border-rose-200/20 pb-4">
                <h3 class="text-xl font-serif-custom font-bold text-rose-200 flex items-center gap-2">
                    <i class="fa-solid fa-pen-nib text-amber-300"></i>
                    <span>Customize Secret Letter</span>
                </h3>
                <button onclick="toggleLetterModal()" class="text-rose-300 hover:text-white text-xl">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Recipient Greeting</label>
                    <input type="text" id="editRecipient" placeholder="e.g., My Dearest Ning Ning," class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl px-4 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none focus:border-rose-400">
                </div>

                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Letter Paragraphs (Separate paragraphs with newlines)</label>
                    <textarea id="editLetterBody" rows="8" placeholder="Write your heartfelt letter here..." class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl p-3 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none focus:border-rose-400 leading-relaxed"></textarea>
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Sign-off Phrase</label>
                        <input type="text" id="editSignoff" placeholder="e.g., Forever & Always," class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl px-3 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Sender Name</label>
                        <input type="text" id="editSender" placeholder="e.g., Yours Truly ❤️" class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl px-3 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none">
                    </div>
                </div>

                <div class="flex items-center justify-between pt-2">
                    <button onclick="resetDefaultLetter()" class="text-xs text-amber-300 hover:underline">Reset Default Letter</button>
                    <button onclick="saveCustomLetter()" class="bg-gradient-to-r from-rose-500 to-pink-600 text-white font-semibold px-6 py-2.5 rounded-xl text-xs hover:from-rose-600 hover:to-pink-700 transition">
                        Save Letter Changes
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- REASONS MANAGEMENT MODAL -->
    <div id="reasonsModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden">
        <div class="glass-card w-full max-w-lg p-6 rounded-3xl border border-rose-300/30 max-h-[90vh] overflow-y-auto text-rose-100 space-y-6">
            <div class="flex items-center justify-between border-b border-rose-200/20 pb-4">
                <h3 class="text-xl font-serif-custom font-bold text-rose-200 flex items-center gap-2">
                    <i class="fa-solid fa-heart text-rose-400"></i>
                    <span>Customize Special Reasons</span>
                </h3>
                <button onclick="toggleReasonsModal()" class="text-rose-300 hover:text-white text-xl">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="space-y-4">
                <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300">Add New Reason Card</label>
                
                <div class="flex flex-col gap-3">
                    <textarea id="newReasonText" rows="3" placeholder="Enter reason (e.g., You make every moment feel magical...)" class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl p-3 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none focus:border-rose-400"></textarea>
                    
                    <button onclick="addNewReason()" class="w-full bg-gradient-to-r from-rose-500 to-pink-600 text-white font-semibold py-2.5 rounded-xl text-xs hover:from-rose-600 hover:to-pink-700 transition">
                        Add Reason
                    </button>
                </div>
            </div>

            <div class="space-y-3 pt-2">
                <div class="flex items-center justify-between">
                    <label class="text-xs font-semibold uppercase tracking-wider text-rose-300">Existing Reasons</label>
                    <button onclick="resetDefaultReasons()" class="text-[10px] text-amber-300 hover:underline">Reset Defaults</button>
                </div>
                
                <div id="modalReasonsList" class="space-y-2 max-h-48 overflow-y-auto pr-1">
                    <!-- Populated via JavaScript -->
                </div>
            </div>

            <button onclick="toggleReasonsModal()" class="w-full bg-rose-950/80 border border-rose-400/30 text-rose-200 font-medium py-2.5 rounded-xl text-xs hover:bg-rose-900/60 transition">
                Close & Save
            </button>
        </div>
    </div>

    <!-- PHOTO MANAGEMENT MODAL -->
    <div id="photoModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden">
        <div class="glass-card w-full max-w-lg p-6 rounded-3xl border border-rose-300/30 max-h-[90vh] overflow-y-auto text-rose-100 space-y-6">
            <div class="flex items-center justify-between border-b border-rose-200/20 pb-4">
                <h3 class="text-xl font-serif-custom font-bold text-rose-200 flex items-center gap-2">
                    <i class="fa-solid fa-images text-rose-400"></i>
                    <span>Customize Photos</span>
                </h3>
                <button onclick="togglePhotoModal()" class="text-rose-300 hover:text-white text-xl">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="space-y-4">
                <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300">Add New Photo</label>
                
                <div class="flex flex-col gap-3">
                    <input type="file" id="imageInput" accept="image/*" class="block w-full text-xs text-rose-300 file:mr-4 file:py-2.5 file:px-4 file:rounded-full file:border-0 file:text-xs file:font-semibold file:bg-rose-500 file:text-white hover:file:bg-rose-600 transition cursor-pointer">
                    
                    <input type="text" id="captionInput" placeholder="Enter romantic caption (e.g., Our First Trip)" class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl px-4 py-2.5 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none focus:border-rose-400">
                    
                    <button onclick="addPhotoFromUpload()" class="w-full bg-gradient-to-r from-rose-500 to-pink-600 text-white font-semibold py-2.5 rounded-xl text-xs hover:from-rose-600 hover:to-pink-700 transition">
                        Upload & Add Photo
                    </button>
                </div>
            </div>

            <div class="space-y-3 pt-2">
                <div class="flex items-center justify-between">
                    <label class="text-xs font-semibold uppercase tracking-wider text-rose-300">Manage Current Photos</label>
                    <button onclick="resetDefaultPhotos()" class="text-[10px] text-amber-300 hover:underline">Reset Defaults</button>
                </div>
                
                <div id="modalPhotoList" class="space-y-2 max-h-48 overflow-y-auto pr-1">
                    <!-- Populated via JavaScript -->
                </div>
            </div>

            <button onclick="togglePhotoModal()" class="w-full bg-rose-950/80 border border-rose-400/30 text-rose-200 font-medium py-2.5 rounded-xl text-xs hover:bg-rose-900/60 transition">
                Close & Save Changes
            </button>
        </div>
    </div>

    <!-- QUIZ EDITING MODAL -->
    <div id="quizModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden">
        <div class="glass-card w-full max-w-lg p-6 rounded-3xl border border-rose-300/30 max-h-[90vh] overflow-y-auto text-rose-100 space-y-6">
            <div class="flex items-center justify-between border-b border-rose-200/20 pb-4">
                <h3 class="text-xl font-serif-custom font-bold text-rose-200 flex items-center gap-2">
                    <i class="fa-solid fa-pen-to-square text-pink-300"></i>
                    <span>Customize Quiz</span>
                </h3>
                <button onclick="toggleQuizModal()" class="text-rose-300 hover:text-white text-xl">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="space-y-3">
                <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300">Add New Question</label>
                
                <input type="text" id="newQuestionText" placeholder="Enter Question (e.g., Where was our 1st date?)" class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl px-4 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none focus:border-rose-400">
                
                <div class="grid grid-cols-2 gap-2">
                    <input type="text" id="opt0" placeholder="Option A (Correct Answer)" class="bg-rose-950/50 border border-emerald-400/50 rounded-xl px-3 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none">
                    <input type="text" id="opt1" placeholder="Option B" class="bg-rose-950/50 border border-rose-300/30 rounded-xl px-3 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none">
                    <input type="text" id="opt2" placeholder="Option C" class="bg-rose-950/50 border border-rose-300/30 rounded-xl px-3 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none">
                    <input type="text" id="opt3" placeholder="Option D" class="bg-rose-950/50 border border-rose-300/30 rounded-xl px-3 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none">
                </div>

                <button onclick="addNewQuizQuestion()" class="w-full bg-gradient-to-r from-pink-500 to-rose-600 text-white font-semibold py-2 rounded-xl text-xs hover:from-pink-600 hover:to-rose-700 transition">
                    Add Question
                </button>
            </div>

            <div class="space-y-3 pt-2">
                <div class="flex items-center justify-between">
                    <label class="text-xs font-semibold uppercase tracking-wider text-rose-300">Existing Questions</label>
                    <button onclick="resetDefaultQuiz()" class="text-[10px] text-amber-300 hover:underline">Reset Defaults</button>
                </div>
                
                <div id="modalQuizList" class="space-y-2 max-h-48 overflow-y-auto pr-1">
                    <!-- Populated via JavaScript -->
                </div>
            </div>

            <button onclick="toggleQuizModal()" class="w-full bg-rose-950/80 border border-rose-400/30 text-rose-200 font-medium py-2.5 rounded-xl text-xs hover:bg-rose-900/60 transition">
                Done & Save Quiz
            </button>
        </div>
    </div>

    <script>
        /* ----------------------------------------------------
           PAGE SWITCHING & SLIDE ANIMATION LOGIC
        ---------------------------------------------------- */
        function switchPage(page) {
            const pageHome = document.getElementById('pageHome');
            const pageQuiz = document.getElementById('pageQuiz');
            const navHomeBtn = document.getElementById('navHomeBtn');
            const navQuizBtn = document.getElementById('navQuizBtn');

            window.scrollTo({ top: 0, behavior: 'smooth' });

            if (page === 'quiz') {
                pageHome.classList.remove('active-page');
                pageHome.classList.add('hidden-page');
                
                pageQuiz.classList.remove('hidden-page');
                pageQuiz.classList.add('active-page');

                navQuizBtn.className = "px-4 py-1.5 rounded-full text-xs font-semibold transition-all duration-300 bg-gradient-to-r from-rose-500 to-pink-600 text-white shadow-md flex items-center gap-1.5";
                navHomeBtn.className = "px-4 py-1.5 rounded-full text-xs font-semibold transition-all duration-300 text-rose-200 hover:text-white flex items-center gap-1.5";
            } else {
                pageQuiz.classList.remove('active-page');
                pageQuiz.classList.add('hidden-page');

                pageHome.classList.remove('hidden-page');
                pageHome.classList.add('active-page');

                navHomeBtn.className = "px-4 py-1.5 rounded-full text-xs font-semibold transition-all duration-300 bg-gradient-to-r from-rose-500 to-pink-600 text-white shadow-md flex items-center gap-1.5";
                navQuizBtn.className = "px-4 py-1.5 rounded-full text-xs font-semibold transition-all duration-300 text-rose-200 hover:text-white flex items-center gap-1.5";
            }
        }

        /* ----------------------------------------------------
           0. WEBSITE UNLOCK PASSWORD LOGIC (STORED SECURELY)
        ---------------------------------------------------- */
        const DEFAULT_SITE_PASSWORD = "1234";

        function getStoredSitePasscode() {
            try {
                return localStorage.getItem('birthday_site_passcode') || DEFAULT_SITE_PASSWORD;
            } catch (e) {
                return DEFAULT_SITE_PASSWORD;
            }
        }

        function changeSitePasscode() {
            const newCode = document.getElementById('newSitePasscodeInput').value.trim();
            if (!newCode) {
                alert('Please enter a valid passcode!');
                return;
            }
            try {
                localStorage.setItem('birthday_site_passcode', newCode);
                alert('Website unlock passcode updated successfully!');
                document.getElementById('newSitePasscodeInput').value = '';
            } catch (e) {
                console.warn('Storage error for site passcode');
            }
        }

        function unlockWebsite() {
            const inputField = document.getElementById('sitePasswordInput');
            const pwd = inputField.value;
            const errorMsg = document.getElementById('siteUnlockError');
            const overlay = document.getElementById('siteUnlockOverlay');
            const box = document.getElementById('siteUnlockBox');

            const validPasscode = getStoredSitePasscode();

            if (pwd === validPasscode) {
                overlay.classList.add('opacity-0', 'pointer-events-none');
                playCelebrationSound();
                autoStartMusic();
                
                if (typeof confetti === 'function') {
                    confetti({
                        particleCount: 100,
                        spread: 70,
                        origin: { y: 0.6 }
                    });
                }
                
                setTimeout(() => {
                    overlay.classList.add('hidden');
                }, 700);
            } else {
                errorMsg.classList.remove('hidden');
                box.classList.add('shake');
                inputField.value = '';
                setTimeout(() => box.classList.remove('shake'), 400);
            }
        }

        /* ----------------------------------------------------
           1. HOST KEY & SECURITY AUTHORIZATION LOGIC
        ---------------------------------------------------- */
        const DEFAULT_HOST_KEY = "1234";
        let pendingHostCallback = null;

        function getStoredHostKey() {
            try {
                return localStorage.getItem('birthday_host_key') || DEFAULT_HOST_KEY;
            } catch (e) {
                return DEFAULT_HOST_KEY;
            }
        }

        function requestHostAccess(callback) {
            pendingHostCallback = callback;
            document.getElementById('hostPasswordInput').value = '';
            document.getElementById('hostAuthError').classList.add('hidden');
            document.getElementById('hostAuthModal').classList.remove('hidden');
        }

        function closeHostAuthModal() {
            document.getElementById('hostAuthModal').classList.add('hidden');
            pendingHostCallback = null;
        }

        function submitHostAuth() {
            const inputKey = document.getElementById('hostPasswordInput').value;
            const validKey = getStoredHostKey();

            if (inputKey === validKey) {
                document.getElementById('hostAuthModal').classList.add('hidden');
                if (pendingHostCallback) {
                    pendingHostCallback();
                    pendingHostCallback = null;
                }
            } else {
                document.getElementById('hostAuthError').classList.remove('hidden');
            }
        }

        function changeHostKey() {
            const newKey = document.getElementById('newHostPasswordInput').value.trim();
            if (!newKey) {
                alert('Please enter a valid key!');
                return;
            }
            try {
                localStorage.setItem('birthday_host_key', newKey);
                alert('Host key updated successfully!');
                document.getElementById('newHostPasswordInput').value = '';
            } catch (e) {
                console.warn('Storage error for host key');
            }
        }

        /* ----------------------------------------------------
           2. PHOTO STORAGE & MANAGEMENT (LocalStorage)
        ---------------------------------------------------- */
        const DEFAULT_PHOTOS = [
            {
                url: 'https://images.unsplash.com/photo-1518199266791-5375a83190b7?auto=format&fit=crop&w=600&q=80',
                caption: 'Our Favorite Memories'
            },
            {
                url: 'https://images.unsplash.com/photo-1522673607200-164d1b6ce486?auto=format&fit=crop&w=600&q=80',
                caption: 'Quiet Sunset Moments'
            },
            {
                url: 'https://images.unsplash.com/photo-1516589178581-6cd7833ae3b2?auto=format&fit=crop&w=600&q=80',
                caption: 'To Infinite Adventures'
            }
        ];

        function getStoredPhotos() {
            try {
                const saved = localStorage.getItem('birthday_photos');
                return saved ? JSON.parse(saved) : DEFAULT_PHOTOS;
            } catch (e) {
                return DEFAULT_PHOTOS;
            }
        }

        function savePhotos(photos) {
            try {
                localStorage.setItem('birthday_photos', JSON.stringify(photos));
            } catch (e) {
                console.warn('Storage quota exceeded');
            }
            renderPhotoGallery();
            renderModalPhotoList();
        }

        function renderPhotoGallery() {
            const photos = getStoredPhotos();
            const grid = document.getElementById('photoGrid');
            grid.innerHTML = '';

            photos.forEach((photo, idx) => {
                const rotations = ['-rotate-2', 'rotate-2', '-rotate-1', 'rotate-3', '-rotate-3'];
                const rotClass = rotations[idx % rotations.length];

                const card = document.createElement('div');
                card.className = `bg-amber-50/10 p-4 rounded-xl glass-card border border-rose-200/20 transform ${rotClass} hover:rotate-0 transition duration-300 hover:scale-105 shadow-xl flex flex-col justify-between`;
                
                card.innerHTML = `
                    <div class="aspect-square rounded-lg overflow-hidden border border-rose-300/20 relative group bg-rose-950/40">
                        <img src="${photo.url}" alt="${photo.caption}" class="w-full h-full object-cover group-hover:scale-110 transition duration-500" onerror="this.src='https://placehold.co/400x400/2a0826/fce7f3?text=Memory+Photo'">
                    </div>
                    <div class="pt-3 text-center">
                        <p class="font-cursive text-xl text-rose-200 truncate px-1">${photo.caption}</p>
                        <p class="text-[10px] text-rose-300/50 uppercase tracking-widest mt-1">Memory #${idx + 1}</p>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function renderModalPhotoList() {
            const photos = getStoredPhotos();
            const list = document.getElementById('modalPhotoList');
            list.innerHTML = '';

            photos.forEach((photo, idx) => {
                const item = document.createElement('div');
                item.className = 'flex items-center justify-between bg-rose-950/40 p-2 rounded-xl border border-rose-300/20';
                item.innerHTML = `
                    <div class="flex items-center gap-3 overflow-hidden pr-2">
                        <img src="${photo.url}" class="w-10 h-10 object-cover rounded-lg flex-shrink-0" onerror="this.src='https://placehold.co/100x100/2a0826/fce7f3?text=Photo'">
                        <span class="text-xs text-rose-200 truncate">${photo.caption}</span>
                    </div>
                    <button onclick="deletePhoto(${idx})" class="text-rose-400 hover:text-rose-200 text-sm px-2 flex-shrink-0">
                        <i class="fa-solid fa-trash-can"></i>
                    </button>
                `;
                list.appendChild(item);
            });
        }

        function addPhotoFromUpload() {
            const fileInput = document.getElementById('imageInput');
            const captionInput = document.getElementById('captionInput');
            const file = fileInput.files[0];
            const caption = captionInput.value.trim() || 'Beautiful Memory';

            if (!file) {
                alert('Please select an image file first!');
                return;
            }

            const reader = new FileReader();
            reader.onload = function(e) {
                const photos = getStoredPhotos();
                photos.push({
                    url: e.target.result,
                    caption: caption
                });
                savePhotos(photos);
                
                fileInput.value = '';
                captionInput.value = '';
            };
            reader.readAsDataURL(file);
        }

        function deletePhoto(index) {
            const photos = getStoredPhotos();
            photos.splice(index, 1);
            savePhotos(photos);
        }

        function resetDefaultPhotos() {
            savePhotos(DEFAULT_PHOTOS);
        }

        function togglePhotoModal() {
            const modal = document.getElementById('photoModal');
            modal.classList.toggle('hidden');
            if (!modal.classList.contains('hidden')) {
                renderModalPhotoList();
            }
        }

        /* ----------------------------------------------------
           3. SECRET LETTER STORAGE & CUSTOMIZATION
        ---------------------------------------------------- */
        const DEFAULT_LETTER = {
            recipient: "My Dearest Ning Ning,",
            body: [
                "I want you to know why this day matters so much to me—not just because it’s your birthday, but because today is the reason my world is so much brighter. Like a bouquet of white lilies bringing light, purity, and beauty into a room, your presence gently transformed my entire life the moment you walked into it.",
                "Before you came along, ordinary days were just dates on a calendar. But today marks the day the universe gave me the person who became my peace, my favorite smile, and my absolute favorite part of every single day.",
                "Celebrating today isn't just about the gifts or the candles; it’s about honoring everything you are and every beautiful memory we've bloomed together. Every laugh we’ve shared, every quiet moment where just holding your hand was enough, and every little habit of yours that makes me fall for you a little more—it all started today.",
                "Today gave me YOU, and for that, it will forever be the most special day of my year."
            ],
            signoff: "Forever & Always,",
            sender: "Yours Truly ❤️"
        };

        function getStoredLetter() {
            try {
                const saved = localStorage.getItem('birthday_letter');
                return saved ? JSON.parse(saved) : DEFAULT_LETTER;
            } catch (e) {
                return DEFAULT_LETTER;
            }
        }

        function renderLetterContent() {
            const letter = getStoredLetter();
            document.getElementById('letterRecipientDisplay').textContent = letter.recipient;
            document.getElementById('letterSignoffDisplay').textContent = letter.signoff;
            document.getElementById('letterSenderDisplay').textContent = letter.sender;

            const bodyContainer = document.getElementById('letterBodyDisplay');
            bodyContainer.innerHTML = '';
            letter.body.forEach(para => {
                const p = document.createElement('p');
                p.className = 'leading-relaxed';
                p.textContent = para;
                bodyContainer.appendChild(p);
            });
        }

        function toggleLetterModal() {
            const modal = document.getElementById('letterModal');
            modal.classList.toggle('hidden');
            if (!modal.classList.contains('hidden')) {
                const letter = getStoredLetter();
                document.getElementById('editRecipient').value = letter.recipient;
                document.getElementById('editLetterBody').value = letter.body.join('\n\n');
                document.getElementById('editSignoff').value = letter.signoff;
                document.getElementById('editSender').value = letter.sender;
            }
        }

        function saveCustomLetter() {
            const recipient = document.getElementById('editRecipient').value.trim() || DEFAULT_LETTER.recipient;
            const bodyRaw = document.getElementById('editLetterBody').value.trim();
            const signoff = document.getElementById('editSignoff').value.trim() || DEFAULT_LETTER.signoff;
            const sender = document.getElementById('editSender').value.trim() || DEFAULT_LETTER.sender;

            const paragraphs = bodyRaw ? bodyRaw.split(/\n\s*\n/).map(p => p.trim()).filter(Boolean) : DEFAULT_LETTER.body;

            const customLetter = {
                recipient: recipient,
                body: paragraphs,
                signoff: signoff,
                sender: sender
            };

            try {
                localStorage.setItem('birthday_letter', JSON.stringify(customLetter));
            } catch (e) {
                console.warn('Storage error for custom letter');
            }

            renderLetterContent();
            toggleLetterModal();
        }

        function resetDefaultLetter() {
            try {
                localStorage.setItem('birthday_letter', JSON.stringify(DEFAULT_LETTER));
            } catch (e) {}
            renderLetterContent();
            toggleLetterModal();
        }

        /* ----------------------------------------------------
           4. CUSTOMIZABLE QUIZ SYSTEM & STORAGE
        ---------------------------------------------------- */
        const DEFAULT_QUIZ = [
            {
                question: "What is my absolute favorite thing about you?",
                options: ["Your beautiful smile", "Your kind heart", "Your spirit 🐦‍🔥", "All of the above! ❤️"],
                correctIndex: 3
            },
            {
                question: "Where is my favorite place in the world?",
                options: ["Paris", "The Beach", "Right next to you", "In a cozy café"],
                correctIndex: 2
            },
            {
                question: "Who loves you more than anything in this universe?",
                options: ["Me!", "Definitely me!", "100% me!", "All options are correct ❤️"],
                correctIndex: 3
            }
        ];

        let currentQuizIndex = 0;
        let quizScore = 0;

        function getStoredQuiz() {
            try {
                const saved = localStorage.getItem('birthday_quiz');
                return saved ? JSON.parse(saved) : DEFAULT_QUIZ;
            } catch (e) {
                return DEFAULT_QUIZ;
            }
        }

        function saveQuiz(questions) {
            try {
                localStorage.setItem('birthday_quiz', JSON.stringify(questions));
            } catch (e) {
                console.warn('Storage error for quiz');
            }
            restartQuiz();
            renderModalQuizList();
        }

        function renderCurrentQuestion() {
            const questions = getStoredQuiz();
            const qContainer = document.getElementById('quizContainer');
            const rContainer = document.getElementById('quizResult');

            if (questions.length === 0) {
                document.getElementById('quizQuestion').textContent = "No questions added yet!";
                document.getElementById('quizOptions').innerHTML = '';
                return;
            }

            if (currentQuizIndex >= questions.length) {
                qContainer.classList.add('hidden');
                rContainer.classList.remove('hidden');
                document.getElementById('quizResultMessage').textContent = 
                    `You scored ${quizScore} out of ${questions.length}! You're absolute perfection! ❤️`;
                
                if (typeof confetti === 'function') {
                    confetti({ particleCount: 80, spread: 70, origin: { y: 0.6 } });
                }
                return;
            }

            qContainer.classList.remove('hidden');
            rContainer.classList.add('hidden');

            const current = questions[currentQuizIndex];
            document.getElementById('quizProgress').textContent = `Question ${currentQuizIndex + 1} of ${questions.length}`;
            document.getElementById('quizScore').textContent = `Score: ${quizScore}`;
            document.getElementById('quizQuestion').textContent = current.question;

            const optionsBox = document.getElementById('quizOptions');
            optionsBox.innerHTML = '';

            const feedback = document.getElementById('quizFeedback');
            feedback.classList.add('hidden');

            current.options.forEach((opt, idx) => {
                const btn = document.createElement('button');
                btn.className = 'w-full bg-rose-950/40 hover:bg-rose-900/60 border border-rose-300/20 text-rose-100 text-xs sm:text-sm py-3 px-4 rounded-xl transition text-left font-medium flex items-center justify-between group';
                btn.innerHTML = `
                    <span>${opt}</span>
                    <i class="fa-solid fa-heart text-rose-400/0 group-hover:text-rose-400 transition-all"></i>
                `;
                btn.onclick = () => handleAnswer(idx, current.correctIndex);
                optionsBox.appendChild(btn);
            });
        }

        function handleAnswer(selectedIndex, correctIndex) {
            const feedback = document.getElementById('quizFeedback');
            feedback.classList.remove('hidden');

            if (selectedIndex === correctIndex) {
                quizScore++;
                feedback.className = "mt-4 p-3 rounded-xl text-xs font-semibold bg-emerald-950/60 border border-emerald-500/40 text-emerald-200";
                feedback.innerHTML = '<i class="fa-solid fa-circle-check mr-1"></i> Correct! You know me so well ❤️';
                playCelebrationSound();
            } else {
                feedback.className = "mt-4 p-3 rounded-xl text-xs font-semibold bg-rose-950/60 border border-rose-500/40 text-rose-200";
                feedback.innerHTML = '<i class="fa-solid fa-circle-xmark mr-1"></i> Aww, close! But I love you anyway 💕';
            }

            const btns = document.querySelectorAll('#quizOptions button');
            btns.forEach(b => b.disabled = true);

            setTimeout(() => {
                currentQuizIndex++;
                renderCurrentQuestion();
            }, 1200);
        }

        function restartQuiz() {
            currentQuizIndex = 0;
            quizScore = 0;
            renderCurrentQuestion();
        }

        function toggleQuizModal() {
            const modal = document.getElementById('quizModal');
            modal.classList.toggle('hidden');
            if (!modal.classList.contains('hidden')) {
                renderModalQuizList();
            }
        }

        function renderModalQuizList() {
            const questions = getStoredQuiz();
            const list = document.getElementById('modalQuizList');
            list.innerHTML = '';

            questions.forEach((q, idx) => {
                const item = document.createElement('div');
                item.className = 'flex items-center justify-between bg-rose-950/40 p-2.5 rounded-xl border border-rose-300/20';
                item.innerHTML = `
                    <div class="overflow-hidden pr-2">
                        <p class="text-xs text-rose-200 font-medium truncate">${idx + 1}. ${q.question}</p>
                        <p class="text-[10px] text-pink-300/60 truncate">Ans: ${q.options[q.correctIndex]}</p>
                    </div>
                    <button onclick="deleteQuizQuestion(${idx})" class="text-rose-400 hover:text-rose-200 text-sm px-2 flex-shrink-0">
                        <i class="fa-solid fa-trash-can"></i>
                    </button>
                `;
                list.appendChild(item);
            });
        }

        function addNewQuizQuestion() {
            const qText = document.getElementById('newQuestionText').value.trim();
            const o0 = document.getElementById('opt0').value.trim();
            const o1 = document.getElementById('opt1').value.trim();
            const o2 = document.getElementById('opt2').value.trim();
            const o3 = document.getElementById('opt3').value.trim();

            if (!qText || !o0 || !o1) {
                alert('Please provide a question and at least 2 option choices!');
                return;
            }

            const options = [o0, o1];
            if (o2) options.push(o2);
            if (o3) options.push(o3);

            const questions = getStoredQuiz();
            questions.push({
                question: qText,
                options: options,
                correctIndex: 0
            });

            saveQuiz(questions);

            document.getElementById('newQuestionText').value = '';
            document.getElementById('opt0').value = '';
            document.getElementById('opt1').value = '';
            document.getElementById('opt2').value = '';
            document.getElementById('opt3').value = '';
        }

        function deleteQuizQuestion(index) {
            const questions = getStoredQuiz();
            questions.splice(index, 1);
            saveQuiz(questions);
        }

        function resetDefaultQuiz() {
            saveQuiz(DEFAULT_QUIZ);
        }

        /* ----------------------------------------------------
           5. REASONS WHY YOU ARE SPECIAL - STORAGE & EDITING
        ---------------------------------------------------- */
        const DEFAULT_REASONS = [
            {
                icon: 'fa-solid fa-heart text-2xl text-rose-400 animate-pulse',
                text: "You are my instant peace. No matter how crazy the world gets, seeing your face settles everything."
            },
            {
                icon: 'fa-solid fa-face-smile-beam text-2xl text-amber-300',
                text: "Your laugh is my absolute favorite sound in the whole world. It brightens my worst days instantly."
            },
            {
                icon: 'fa-solid fa-house-chimney-heart text-2xl text-pink-400',
                text: "Home used to be a physical place for me—until I met you. Now, home is wherever you are."
            },
            {
                icon: 'fa-solid fa-sparkles text-2xl text-amber-200',
                text: "You notice the little things that everyone else misses. Your kindness and warmth are unmatched."
            },
            {
                icon: 'fa-solid fa-gem text-2xl text-cyan-300',
                text: "You make me want to be a better person every day just by being around your incredible light."
            },
            {
                icon: 'fa-solid fa-infinity text-2xl text-rose-300',
                text: "Simply because you are YOU. Out of everyone on this planet, my heart picked you, and it always will."
            }
        ];

        function getStoredReasons() {
            try {
                const saved = localStorage.getItem('birthday_reasons');
                return saved ? JSON.parse(saved) : DEFAULT_REASONS;
            } catch (e) {
                return DEFAULT_REASONS;
            }
        }

        function saveReasons(reasons) {
            try {
                localStorage.setItem('birthday_reasons', JSON.stringify(reasons));
            } catch (e) {
                console.warn('Storage error for reasons');
            }
            renderReasonsGrid();
            renderModalReasonsList();
        }

        function renderReasonsGrid() {
            const reasons = getStoredReasons();
            const grid = document.getElementById('reasonsGrid');
            grid.innerHTML = '';

            const defaultIcons = [
                'fa-solid fa-heart text-2xl text-rose-400 animate-pulse',
                'fa-solid fa-face-smile-beam text-2xl text-amber-300',
                'fa-solid fa-house-chimney-heart text-2xl text-pink-400',
                'fa-solid fa-sparkles text-2xl text-amber-200',
                'fa-solid fa-gem text-2xl text-cyan-300',
                'fa-solid fa-infinity text-2xl text-rose-300'
            ];

            reasons.forEach((reason, idx) => {
                const iconClass = reason.icon || defaultIcons[idx % defaultIcons.length];
                const card = document.createElement('div');
                card.className = 'flip-card cursor-pointer';
                card.onclick = function() { flipCard(this); };

                card.innerHTML = `
                    <div class="flip-card-inner">
                        <div class="flip-card-front glass-card border-rose-400/20 text-rose-200">
                            <div class="space-y-2">
                                <i class="${iconClass}"></i>
                                <h3 class="font-semibold text-base">Reason #${idx + 1}</h3>
                                <p class="text-xs text-rose-300/60">Tap to flip ✨</p>
                            </div>
                        </div>
                        <div class="flip-card-back bg-gradient-to-br from-rose-900/90 to-purple-900/90 border border-rose-400/40 text-rose-100">
                            <p class="text-xs sm:text-sm font-medium leading-relaxed">
                                "${reason.text}"
                            </p>
                        </div>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function renderModalReasonsList() {
            const reasons = getStoredReasons();
            const list = document.getElementById('modalReasonsList');
            list.innerHTML = '';

            reasons.forEach((r, idx) => {
                const item = document.createElement('div');
                item.className = 'flex items-center justify-between bg-rose-950/40 p-2.5 rounded-xl border border-rose-300/20';
                item.innerHTML = `
                    <div class="overflow-hidden pr-2">
                        <p class="text-xs text-rose-200 font-medium truncate">#${idx + 1}: ${r.text}</p>
                    </div>
                    <button onclick="deleteReason(${idx})" class="text-rose-400 hover:text-rose-200 text-sm px-2 flex-shrink-0">
                        <i class="fa-solid fa-trash-can"></i>
                    </button>
                `;
                list.appendChild(item);
            });
        }

        function addNewReason() {
            const text = document.getElementById('newReasonText').value.trim();
            if (!text) {
                alert('Please enter a reason text!');
                return;
            }

            const reasons = getStoredReasons();
            reasons.push({ text: text });
            saveReasons(reasons);

            document.getElementById('newReasonText').value = '';
        }

        function deleteReason(index) {
            const reasons = getStoredReasons();
            reasons.splice(index, 1);
            saveReasons(reasons);
        }

        function resetDefaultReasons() {
            saveReasons(DEFAULT_REASONS);
        }

        function toggleReasonsModal() {
            const modal = document.getElementById('reasonsModal');
            modal.classList.toggle('hidden');
            if (!modal.classList.contains('hidden')) {
                renderModalReasonsList();
            }
        }

        /* ----------------------------------------------------
           6. CANVAS FLOATING HEARTS, LILIES, CAPYBARA WITH BALLOONS & SPARKLE STARS PATTERN
        ---------------------------------------------------- */
        const canvas = document.getElementById('bgCanvas');
        const ctx = canvas.getContext('2d');
        let width = canvas.width = window.innerWidth;
        let height = canvas.height = window.innerHeight;

        const DEFAULT_PATTERN = { count: 30, speed: 4, size: 12 };

        function getStoredPattern() {
            try {
                const saved = localStorage.getItem('birthday_pattern');
                return saved ? JSON.parse(saved) : DEFAULT_PATTERN;
            } catch (e) {
                return DEFAULT_PATTERN;
            }
        }

        let currentPatternConfig = getStoredPattern();

        window.addEventListener('resize', () => {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
        });

        class PatternParticle {
            constructor() { this.reset(); }
            reset() {
                this.x = Math.random() * width;
                this.y = height + Math.random() * 100;
                
                const rand = Math.random();
                if (rand < 0.25) {
                    this.type = 'heart';
                } else if (rand < 0.50) {
                    this.type = 'star';
                } else if (rand < 0.75) {
                    this.type = 'lily';
                } else {
                    this.type = 'capybaraBalloon';
                }

                this.baseSize = currentPatternConfig.size;
                this.size = this.type === 'capybaraBalloon' 
                    ? Math.random() * (this.baseSize * 1.5) + (this.baseSize * 1.8)
                    : Math.random() * (this.baseSize * 0.5) + (this.baseSize * 0.8);

                this.speedY = (Math.random() * 0.8 + 0.3) * (currentPatternConfig.speed / 4);
                this.speedX = Math.sin(Math.random() * Math.PI) * 0.5;
                this.rotation = Math.random() * Math.PI * 0.2 - 0.1;
                this.rotSpeed = (Math.random() - 0.5) * 0.01;
                this.opacity = this.type === 'capybaraBalloon' ? Math.random() * 0.4 + 0.5 : Math.random() * 0.5 + 0.2;
            }
            update() {
                this.y -= this.speedY;
                this.x += Math.sin(this.y * 0.01) * 0.6;
                this.rotation += this.rotSpeed;
                if (this.y < -80) this.reset();
            }
            draw() {
                ctx.save();
                ctx.translate(this.x, this.y);
                ctx.rotate(this.rotation);
                ctx.globalAlpha = this.opacity;

                if (this.type === 'heart') {
                    ctx.fillStyle = `hsla(${Math.random() * 20 + 330}, 80%, 75%, ${this.opacity})`;
                    ctx.beginPath();
                    const topCurve = this.size * 0.3;
                    ctx.moveTo(0, topCurve);
                    ctx.bezierCurveTo(0, 0, -this.size / 2, 0, -this.size / 2, topCurve);
                    ctx.bezierCurveTo(-this.size / 2, (this.size + topCurve) / 2, 0, this.size, 0, this.size);
                    ctx.bezierCurveTo(0, this.size, this.size / 2, (this.size + topCurve) / 2, this.size / 2, topCurve);
                    ctx.bezierCurveTo(this.size / 2, 0, 0, 0, 0, topCurve);
                    ctx.closePath();
                    ctx.fill();
                } else if (this.type === 'star') {
                    ctx.fillStyle = '#fde047';
                    ctx.beginPath();
                    for (let i = 0; i < 4; i++) {
                        ctx.rotate(Math.PI / 2);
                        ctx.lineTo(0, -this.size);
                        ctx.quadraticCurveTo(0, 0, this.size * 0.2, 0);
                    }
                    ctx.fill();
                } else if (this.type === 'lily') {
                    for (let i = 0; i < 6; i++) {
                        ctx.rotate(Math.PI / 3);
                        const grad = ctx.createLinearGradient(0, 0, 0, -this.size);
                        grad.addColorStop(0, '#f472b6');
                        grad.addColorStop(0.4, '#fbcfe8');
                        grad.addColorStop(1, '#ffffff');

                        ctx.beginPath();
                        ctx.moveTo(0, 0);
                        ctx.quadraticCurveTo(-this.size * 0.3, -this.size * 0.6, 0, -this.size);
                        ctx.quadraticCurveTo(this.size * 0.3, -this.size * 0.6, 0, 0);
                        ctx.fillStyle = grad;
                        ctx.fill();
                    }
                    ctx.beginPath();
                    ctx.arc(0, 0, this.size * 0.15, 0, Math.PI * 2);
                    ctx.fillStyle = '#fde047';
                    ctx.fill();
                } else if (this.type === 'capybaraBalloon') {
                    const s = this.size * 1.4;
                    ctx.strokeStyle = 'rgba(255, 255, 255, 0.6)';
                    ctx.lineWidth = 1;
                    ctx.beginPath();
                    ctx.moveTo(s * 0.1, s * 0.1); ctx.lineTo(-s * 0.25, -s * 0.6);
                    ctx.moveTo(s * 0.1, s * 0.1); ctx.lineTo(0, -s * 0.7);
                    ctx.moveTo(s * 0.1, s * 0.1); ctx.lineTo(s * 0.25, -s * 0.6);
                    ctx.stroke();

                    const colors = ['#f472b6', '#fde047', '#fb7185'];
                    const offsets = [{x: -s * 0.25, y: -s * 0.8}, {x: 0, y: -s * 0.9}, {x: s * 0.25, y: -s * 0.8}];
                    offsets.forEach((off, idx) => {
                        ctx.beginPath();
                        ctx.ellipse(off.x, off.y, s * 0.18, s * 0.24, 0, 0, Math.PI * 2);
                        ctx.fillStyle = colors[idx];
                        ctx.fill();
                    });

                    ctx.fillStyle = '#a66e38';
                    ctx.beginPath();
                    ctx.ellipse(0, s * 0.35, s * 0.3, s * 0.35, 0, 0, Math.PI * 2);
                    ctx.fill();

                    ctx.fillStyle = '#b87d43';
                    ctx.beginPath();
                    ctx.ellipse(0, s * 0.05, s * 0.25, s * 0.22, 0, 0, Math.PI * 2);
                    ctx.fill();

                    ctx.fillStyle = '#8c5833';
                    ctx.beginPath();
                    ctx.ellipse(-s * 0.22, -s * 0.08, s * 0.06, s * 0.04, -0.2, 0, Math.PI * 2);
                    ctx.ellipse(s * 0.22, -s * 0.08, s * 0.06, s * 0.04, 0.2, 0, Math.PI * 2);
                    ctx.fill();
                }

                ctx.restore();
            }
        }

        let particles = [];
        function initPatternParticles() {
            particles = Array.from({ length: currentPatternConfig.count }, () => new PatternParticle());
        }
        initPatternParticles();

        function animateParticles() {
            ctx.clearRect(0, 0, width, height);
            particles.forEach(p => { p.update(); p.draw(); });
            requestAnimationFrame(animateParticles);
        }
        animateParticles();

        function togglePatternModal() {
            const modal = document.getElementById('patternModal');
            modal.classList.toggle('hidden');
            if (!modal.classList.contains('hidden')) {
                document.getElementById('patternCount').value = currentPatternConfig.count;
                document.getElementById('patternSpeed').value = currentPatternConfig.speed;
                document.getElementById('patternSize').value = currentPatternConfig.size;

                document.getElementById('patternCountVal').textContent = currentPatternConfig.count;
                document.getElementById('patternSpeedVal').textContent = currentPatternConfig.speed;
                document.getElementById('patternSizeVal').textContent = currentPatternConfig.size + 'px';
                
                const currentSong = getStoredCustomSong();
                if (currentSong && currentSong.startsWith('http')) {
                    document.getElementById('musicUrlInput').value = currentSong;
                }
            }
        }

        document.getElementById('patternCount').addEventListener('input', (e) => {
            document.getElementById('patternCountVal').textContent = e.target.value;
        });
        document.getElementById('patternSpeed').addEventListener('input', (e) => {
            document.getElementById('patternSpeedVal').textContent = e.target.value;
        });
        document.getElementById('patternSize').addEventListener('input', (e) => {
            document.getElementById('patternSizeVal').textContent = e.target.value + 'px';
        });

        function savePatternSettings() {
            currentPatternConfig = {
                count: parseInt(document.getElementById('patternCount').value),
                speed: parseInt(document.getElementById('patternSpeed').value),
                size: parseInt(document.getElementById('patternSize').value)
            };
            try {
                localStorage.setItem('birthday_pattern', JSON.stringify(currentPatternConfig));
            } catch (e) {}

            initPatternParticles();
            togglePatternModal();
        }

        function resetDefaultPattern() {
            currentPatternConfig = DEFAULT_PATTERN;
            try {
                localStorage.setItem('birthday_pattern', JSON.stringify(DEFAULT_PATTERN));
            } catch (e) {}
            initPatternParticles();
            togglePatternModal();
        }

        /* ----------------------------------------------------
           7. INTERACTIVE REALISTIC CAKE & MIC BLOWOUT LOGIC
        ---------------------------------------------------- */
        let candlesBlown = false;
        let micStream = null;

        document.getElementById('cake').addEventListener('click', blowCandles);

        function blowCandles() {
            if (candlesBlown) return;
            candlesBlown = true;

            const cakeEl = document.getElementById('cake');
            cakeEl.classList.add('cut');

            const flames = document.querySelectorAll('.flame');
            flames.forEach(flame => {
                flame.classList.add('extinguished');
                const smoke = document.createElement('div');
                smoke.className = 'smoke';
                flame.parentElement.appendChild(smoke);
            });

            if (typeof confetti === 'function') {
                confetti({
                    particleCount: 130,
                    spread: 85,
                    origin: { y: 0.6 },
                    colors: ['#f43f5e', '#fb7185', '#fde047', '#a855f7', '#ffffff']
                });
            }

            document.getElementById('cakeInstructions').textContent = '✨ Slice cut & wish sent to the stars! ✨';
            const wishMsg = document.getElementById('wishMessage');
            wishMsg.classList.remove('hidden');
            
            playCelebrationSound();

            if (micStream) {
                micStream.getTracks().forEach(track => track.stop());
            }
        }

        async function initMicBlowout() {
            const status = document.getElementById('micStatus');
            const btnText = document.getElementById('micBtnText');

            try {
                micStream = await navigator.mediaDevices.getUserMedia({ audio: true, video: false });
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                const analyser = audioContext.createAnalyser();
                const microphone = audioContext.createMediaStreamSource(micStream);
                
                analyser.fftSize = 256;
                microphone.connect(analyser);

                const bufferLength = analyser.frequencyBinCount;
                const dataArray = new Uint8Array(bufferLength);

                status.classList.remove('hidden');
                status.textContent = '🎙️ Mic Active! Blow hard into your microphone ("fuuu")...';
                btnText.textContent = 'Listening for blow...';

                function checkVolume() {
                    if (candlesBlown) return;

                    analyser.getByteFrequencyData(dataArray);
                    let sum = 0;
                    for (let i = 0; i < bufferLength; i++) {
                        sum += dataArray[i];
                    }
                    let average = sum / bufferLength;

                    if (average > 45) {
                        blowCandles();
                        status.textContent = '✨ Blow detected! Happy Birthday!';
                    } else {
                        requestAnimationFrame(checkVolume);
                    }
                }

                checkVolume();
            } catch (err) {
                status.classList.remove('hidden');
                status.textContent = '⚠️ Could not access mic. You can tap the cake to cut a slice!';
                console.warn('Microphone access denied or unsupported:', err);
            }
        }

        /* ----------------------------------------------------
           8. CARD FLIP INTERACTION
        ---------------------------------------------------- */
        function flipCard(cardElement) {
            cardElement.classList.toggle('flipped');
            if (typeof confetti === 'function' && cardElement.classList.contains('flipped')) {
                const rect = cardElement.getBoundingClientRect();
                confetti({
                    particleCount: 20,
                    spread: 50,
                    origin: {
                        x: (rect.left + rect.width / 2) / window.innerWidth,
                        y: (rect.top + rect.height / 2) / window.innerHeight
                    },
                    colors: ['#f472b6', '#fcd34d']
                });
            }
        }

        /* ----------------------------------------------------
           9. SECRET LETTER TOGGLE
        ---------------------------------------------------- */
        function toggleLetter() {
            const letter = document.getElementById('letterContent');
            const envelopeClosed = document.getElementById('envelopeClosed');
            
            letter.classList.toggle('open');
            
            if (letter.classList.contains('open')) {
                envelopeClosed.style.display = 'none';
                if (typeof confetti === 'function') {
                    confetti({
                        particleCount: 60,
                        spread: 70,
                        origin: { y: 0.7 },
                        colors: ['#ffffff', '#fbcfe8', '#f472b6', '#fde047']
                    });
                }
            }
        }

        /* ----------------------------------------------------
           10. HOST SONG CUSTOMIZATION & BACKGROUND MUSIC LOGIC
        ---------------------------------------------------- */
        const DEFAULT_SONG_URL = "https://cdn.pixabay.com/download/audio/2022/05/27/audio_1808fbf07a.mp3?filename=romantic-piano-112199.mp3";
        const bgAudioPlayer = document.getElementById('bgAudioPlayer');
        let audioCtx = null;
        let isAudioPlaying = false;

        function getStoredCustomSong() {
            try {
                return localStorage.getItem('birthday_custom_song') || DEFAULT_SONG_URL;
            } catch (e) {
                return DEFAULT_SONG_URL;
            }
        }

        function setAudioSource(source) {
            bgAudioPlayer.src = source;
            bgAudioPlayer.load();
        }

        function setMusicFromUrl() {
            const urlInput = document.getElementById('musicUrlInput').value.trim();
            if (!urlInput) {
                alert('Please enter a valid audio URL!');
                return;
            }
            try {
                localStorage.setItem('birthday_custom_song', urlInput);
                setAudioSource(urlInput);
                if (isAudioPlaying) bgAudioPlayer.play().catch(e => console.warn(e));
                alert('Background audio URL updated successfully!');
            } catch (e) {
                console.warn('Storage error for song URL');
            }
        }

        function setMusicFromFile() {
            const fileInput = document.getElementById('musicFileInput');
            const file = fileInput.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                const dataUrl = e.target.result;
                try {
                    localStorage.setItem('birthday_custom_song', dataUrl);
                    setAudioSource(dataUrl);
                    if (isAudioPlaying) bgAudioPlayer.play().catch(e => console.warn(e));
                    alert('Song file uploaded & saved successfully!');
                } catch (err) {
                    alert('Audio file size exceeds local storage limit. Try choosing a smaller file or using an online audio URL!');
                }
            };
            reader.readAsDataURL(file);
        }

        document.getElementById('musicToggle').addEventListener('click', toggleMusic);

        function toggleMusic() {
            const musicIcon = document.getElementById('musicIcon');
            const musicText = document.getElementById('musicText');

            if (!bgAudioPlayer.src || bgAudioPlayer.src === window.location.href) {
                setAudioSource(getStoredCustomSong());
            }

            if (!isAudioPlaying) {
                bgAudioPlayer.play().then(() => {
                    isAudioPlaying = true;
                    musicText.textContent = 'Pause';
                    musicIcon.classList.add('fa-spin');
                }).catch(err => {
                    console.warn('Audio play blocked:', err);
                });
            } else {
                bgAudioPlayer.pause();
                isAudioPlaying = false;
                musicText.textContent = 'Music';
                musicIcon.classList.remove('fa-spin');
            }
        }

        function autoStartMusic() {
            if (!bgAudioPlayer.src || bgAudioPlayer.src === window.location.href) {
                setAudioSource(getStoredCustomSong());
            }
            bgAudioPlayer.play().then(() => {
                isAudioPlaying = true;
                document.getElementById('musicText').textContent = 'Pause';
                document.getElementById('musicIcon').classList.add('fa-spin');
            }).catch(e => console.warn('Autoplay error:', e));
        }

        function initAudioContext() {
            if (!audioCtx) {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            }
        }

        function playCelebrationSound() {
            initAudioContext();
            if (audioCtx.state === 'suspended') audioCtx.resume();

            const freqs = [523.25, 659.25, 783.99, 1046.50];
            freqs.forEach((f, index) => {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();

                osc.type = 'triangle';
                osc.frequency.value = f;

                const startTime = audioCtx.currentTime + (index * 0.12);
                gain.gain.setValueAtTime(0.15, startTime);
                gain.gain.exponentialRampToValueAtTime(0.001, startTime + 0.6);

                osc.connect(gain);
                gain.connect(audioCtx.destination);

                osc.start(startTime);
                osc.stop(startTime + 0.6);
            });
        }

        window.addEventListener('DOMContentLoaded', () => {
            renderPhotoGallery();
            renderLetterContent();
            renderCurrentQuestion();
            renderReasonsGrid();
            setAudioSource(getStoredCustomSong());
        });
    </script>
</body>
</html>
