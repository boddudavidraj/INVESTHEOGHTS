# INVESTHEIGHTS
InvestHeights is a personalised investing web app that walks you through your financial journey step by step. Enter your income and goals, get a safe investment amount, explore 13 investment types with full guides, and ask an AI advisor questions tailored to your exact profile.

🏔️ InvestHeights
--Your personalised financial journey — from zero to investor.

💡 What is InvestHeights?
So I built this project because I genuinely felt like most investing platforms out there are either too complicated or too boring. I wanted to create something that actually walks you through investing step by step — in a way that feels personal, not like you're reading a textbook.

InvestHeights is a multi-step web app that takes your income, your goals, and your profile — and turns it into a real, personalised investing guide. It even tells you the safest amount you can start investing right now (your monthly income ÷ 80), so there's no guessing.

🚀 What it does
I designed the whole thing as a journey — you don't just land on a page full of information. You go through it:
-Language selection — pick your preferred language first
-What is investing? — fast-typing animation that explains the basics while a live financial animation plays in the background (gold falling, stocks rising, candlestick charts)
-Why invest + ways to invest — two info blocks that reveal after the typing finishes, plus six investment options shown as pills
-Your financial goals — you type what you're working towards (home, retirement, education, etc.)
-Your profile — age, occupation, city, income, expenses, and savings
-Investment categories — four blocks (A, B, C, D) covering bank investments, share market, crypto, and physical assets. Tap any one to see the full list inside
-Full detail cards — every single investment option (Fixed Deposit, Mutual Funds, Index Funds, Stocks, ETF, Intraday Trading, Bitcoin, Venture Capital, Real    Estate, Gold, Silver, Luxury Assets) has a complete breakdown: what it is, expected returns, risk level, time horizon, pros, cons, and how to get started
-Safe investment amount page — calculates your personal safe daily and monthly investment amount based on your income
-AI Chatbot (powered by Claude) — there's a full AI advisor on the safe amount page AND a mini chatbot inside every single investment detail card. You can ask it   anything specific to that investment — "Is this right for me?", "How much should I put in?", "What are the tax rules?" — and it answers based on your actual       profile

🛠️ Tech Stack
-Pure HTML, CSS, JavaScript — no frameworks, no install needed
-Anthropic Claude API (claude-sonnet) — powers both the main AI advisor and the mini chatbots inside each investment card
-Canvas API — for the animated financial background (falling coins, rising charts, candlesticks)
 Google Fonts — Playfair Display, DM Sans, JetBrains Mono

📁 How to run it
It's just one file — seriously. No npm, no setup.
1.Download investheights.html
2.Open it in your browser
3.That's it
->If you want the AI chatbot to work, you'll need to plug in your Anthropic API key inside the fetch headers in the script section.

🗺️ Pages / Flow
Code
->Each investment card also has its own mini AI chatbot at the bottom — so you're never left with just static information.

🎯 Why I made this
I wanted investing to feel accessible. Most people I know either don't invest at all because they don't know where to start, or they put money in random places without understanding what they're doing. InvestHeights tries to fix that — it meets you where you are, uses your actual numbers, and gives you a personalised path forward.
The AI chatbot piece was important to me because static information only goes so far. Being able to ask "is Bitcoin right for me given my income?" and get an answer based on your actual profile is a different experience entirely.
📸 Features at a Glance
Feature - Details
🌐 Language Selection - 6 languages supported
✍️ Typing Animation - Fast typewriter effect with blinking cursor
🎬 Live Background - Canvas-animated gold, coins, stock charts
👤 User Profile - Age, income, expenses, savings, city, occupation
📊 Investment Categories - 4 categories, 13 investment types
📋 Full Detail Cards - Returns, risk meter, pros/cons, how-to steps
🧮 Safe Amount Calculator - Monthly income ÷ 80 = your safe daily investment
🤖 AI Advisor - Main chatbot + mini chatbot inside every detail card
📱 Responsive - Works on mobile and desktop
🤝 Contributing
Feel free to fork it, improve it, or adapt it for your own use. If you add features or fix something, a PR is always welcome.
📄 License
MIT — use it however you want.
Built with curiosity and a genuine belief that everyone deserves to understand their money.
