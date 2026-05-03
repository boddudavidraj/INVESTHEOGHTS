# INVESTHEOGHTS
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

code:
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>InvestHeights — Your Financial Journey</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=DM+Sans:wght@300;400;500;600&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
:root{--gold:#F4C430;--gold-light:#FFE066;--gold-dark:#B8860B;--green:#00C896;--red:#FF4757;--blue:#6496FF;--dark:#0A0A0F;--dark2:#12121A;--dark3:#1E1E2E;--white:#F5F5F0;--muted:#8888AA;}
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:'DM Sans',sans-serif;background:var(--dark);color:var(--white);overflow-x:hidden;}
.page{display:none;min-height:100vh;position:relative;}
.page.active{display:flex;flex-direction:column;}
.progress-bar{position:fixed;top:0;left:0;height:3px;background:linear-gradient(90deg,var(--gold),var(--green));z-index:9999;transition:width .6s ease;}
#star-canvas{position:fixed;inset:0;z-index:0;pointer-events:none;}

/* PAGE 1 */
#page-lang{align-items:center;justify-content:center;background:var(--dark);}
.lang-wrap{text-align:center;z-index:10;position:relative;padding:2rem;}
.lang-title{font-family:'Playfair Display',serif;font-size:clamp(2rem,5vw,3.2rem);color:var(--gold);margin-bottom:.4rem;animation:fadeDown .8s ease both;}
.lang-sub{color:var(--muted);margin-bottom:2.5rem;animation:fadeDown .8s .2s ease both;}
.lang-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:.9rem;max-width:580px;animation:fadeUp .8s .4s ease both;}
.lang-btn{background:var(--dark3);border:1px solid #333;color:var(--white);padding:.9rem 1.2rem;border-radius:14px;cursor:pointer;font-size:.9rem;font-family:'DM Sans',sans-serif;transition:all .3s;}
.lang-btn:hover,.lang-btn.sel{border-color:var(--gold);color:var(--gold);background:rgba(244,196,48,.08);transform:translateY(-2px);}
.lang-flag{font-size:1.4rem;display:block;margin-bottom:.25rem;}
.lang-confirm{margin-top:2rem;padding:1rem 3rem;background:var(--gold);color:var(--dark);border:none;border-radius:50px;font-size:1rem;font-weight:700;cursor:pointer;font-family:'DM Sans',sans-serif;transition:all .3s;animation:fadeUp .8s .6s ease both;}
.lang-confirm:hover{background:var(--gold-light);transform:scale(1.05);}

/* PAGE 2 */
#page-intro{background:var(--dark);overflow:hidden;}
#bg-canvas{position:fixed;top:0;left:0;width:100%;height:100%;z-index:0;pointer-events:none;}
.intro-content{position:relative;z-index:10;max-width:900px;margin:0 auto;padding:4rem 2rem 3rem;flex:1;}
.typing-block{margin-bottom:2rem;background:rgba(10,10,15,.88);backdrop-filter:blur(12px);border:1px solid rgba(244,196,48,.2);border-radius:20px;padding:2.5rem;}
.typing-label{font-family:'JetBrains Mono',monospace;font-size:.72rem;color:var(--gold);text-transform:uppercase;letter-spacing:.2em;margin-bottom:1rem;}
#typing-text{font-family:'Playfair Display',serif;font-size:clamp(1.15rem,2.8vw,1.7rem);line-height:1.65;min-height:3em;}
.cursor{display:inline-block;width:3px;height:1.1em;background:var(--gold);margin-left:2px;vertical-align:middle;animation:blink .7s infinite;}
@keyframes blink{0%,100%{opacity:1}50%{opacity:0}}
.info-blocks{display:grid;grid-template-columns:1fr 1fr;gap:1.4rem;margin-bottom:2rem;}
.info-block{background:rgba(10,10,15,.88);backdrop-filter:blur(12px);border:1px solid rgba(255,255,255,.07);border-radius:20px;padding:1.8rem;opacity:0;transform:translateY(28px);transition:all .6s ease;}
.info-block.vis{opacity:1;transform:translateY(0);}
.info-block:hover{border-color:rgba(244,196,48,.25);transform:translateY(-4px);}
.block-icon{font-size:1.9rem;margin-bottom:.7rem;}
.block-title{font-family:'Playfair Display',serif;font-size:1.15rem;color:var(--gold);margin-bottom:.6rem;}
.block-body{color:var(--muted);font-size:.88rem;line-height:1.65;}
.invest-block{grid-column:1/-1;background:rgba(10,10,15,.88);backdrop-filter:blur(12px);border:1px solid rgba(244,196,48,.18);border-radius:20px;padding:2rem;opacity:0;transform:translateY(28px);transition:all .6s .3s ease;}
.invest-block.vis{opacity:1;transform:translateY(0);}
.invest-grid{display:grid;grid-template-columns:repeat(6,1fr);gap:.9rem;margin-top:1.1rem;}
.invest-pill{text-align:center;padding:.75rem .4rem;background:rgba(244,196,48,.07);border:1px solid rgba(244,196,48,.18);border-radius:12px;font-size:.78rem;transition:all .3s;}
.invest-pill:hover{background:rgba(244,196,48,.18);border-color:var(--gold);transform:scale(1.06);}
.pill-icon{font-size:1.4rem;display:block;margin-bottom:.25rem;}
.enter-wrap{text-align:center;margin:2rem 0 3rem;opacity:0;transition:opacity .8s;}
.enter-wrap.vis{opacity:1;}
.enter-btn{display:inline-flex;align-items:center;gap:.8rem;padding:1.15rem 3rem;background:linear-gradient(135deg,var(--gold),var(--gold-dark));color:var(--dark);border:none;border-radius:50px;font-size:1.05rem;font-weight:700;cursor:pointer;font-family:'DM Sans',sans-serif;transition:all .3s;animation:pulse-glow 2s infinite;}
@keyframes pulse-glow{0%,100%{box-shadow:0 0 20px rgba(244,196,48,.3)}50%{box-shadow:0 0 50px rgba(244,196,48,.65)}}
.enter-btn:hover{transform:scale(1.05);background:var(--gold-light);}

/* PAGE 3 */
#page-goals{background:linear-gradient(135deg,#0d1117 0%,#1a1a2e 50%,#0d1117 100%);align-items:center;justify-content:center;overflow:hidden;}
.scene-el{position:absolute;font-size:4rem;opacity:.055;animation:float-scene 6s ease-in-out infinite;pointer-events:none;user-select:none;}
@keyframes float-scene{0%,100%{transform:translateY(0) rotate(0deg)}50%{transform:translateY(-18px) rotate(5deg)}}
.goals-card{background:rgba(255,255,255,.03);backdrop-filter:blur(20px);border:1px solid rgba(255,255,255,.1);border-radius:24px;padding:3rem;max-width:540px;width:90%;text-align:center;position:relative;z-index:10;animation:fadeUp .8s ease forwards;}
.goals-q{font-family:'Playfair Display',serif;font-size:clamp(1.3rem,3vw,2rem);margin-bottom:.5rem;}
.goals-sub{color:var(--muted);font-size:.88rem;margin-bottom:1.8rem;}
.goals-input{width:100%;background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.13);border-radius:12px;padding:1rem 1.4rem;color:var(--white);font-size:.95rem;font-family:'DM Sans',sans-serif;resize:vertical;min-height:100px;outline:none;transition:border-color .3s;}
.goals-input:focus{border-color:var(--gold);}

/* PAGE 4 */
#page-profile{background:linear-gradient(135deg,#0a0a0f 0%,#1a1025 100%);align-items:center;justify-content:center;}
.profile-card{background:rgba(255,255,255,.03);backdrop-filter:blur(20px);border:1px solid rgba(255,255,255,.08);border-radius:24px;padding:2.8rem;max-width:580px;width:90%;z-index:10;animation:fadeUp .6s ease forwards;}
.profile-title{font-family:'Playfair Display',serif;font-size:1.75rem;color:var(--gold);margin-bottom:.4rem;}
.profile-sub{color:var(--muted);font-size:.88rem;margin-bottom:1.8rem;}
.form-grid{display:grid;grid-template-columns:1fr 1fr;gap:1.1rem;margin-bottom:1.4rem;}
.form-group{display:flex;flex-direction:column;gap:.35rem;}
.form-label{font-size:.72rem;text-transform:uppercase;letter-spacing:.12em;color:var(--muted);font-family:'JetBrains Mono',monospace;}
.form-input{background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.11);border-radius:10px;padding:.78rem 1rem;color:var(--white);font-size:.93rem;font-family:'DM Sans',sans-serif;outline:none;transition:border-color .3s;}
.form-input:focus{border-color:var(--gold);}
.form-input::placeholder{color:rgba(136,136,170,.45);}
.next-btn{padding:1rem 2.5rem;background:var(--gold);color:var(--dark);border:none;border-radius:50px;font-size:1rem;font-weight:700;cursor:pointer;font-family:'DM Sans',sans-serif;transition:all .3s;margin-top:.8rem;}
.next-btn:hover{background:var(--gold-light);transform:scale(1.03);}

/* PAGE 5 */
#page-invest{background:var(--dark);padding:2rem;}
.invest-header{text-align:center;padding:2rem 0 2.5rem;}
.invest-header h1{font-family:'Playfair Display',serif;font-size:clamp(1.8rem,4vw,2.8rem);color:var(--gold);margin-bottom:.4rem;}
.invest-header p{color:var(--muted);}
.cats-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:1.4rem;max-width:860px;margin:0 auto;}
.cat-card{background:var(--dark3);border:1px solid rgba(255,255,255,.06);border-radius:20px;padding:2rem;cursor:pointer;transition:all .4s;position:relative;overflow:hidden;}
.cat-card::before{content:'';position:absolute;inset:0;opacity:0;border-radius:20px;transition:opacity .4s;}
.cat-card.a::before{background:linear-gradient(135deg,rgba(0,200,150,.1),transparent);}
.cat-card.b::before{background:linear-gradient(135deg,rgba(244,196,48,.1),transparent);}
.cat-card.c::before{background:linear-gradient(135deg,rgba(255,71,87,.1),transparent);}
.cat-card.d::before{background:linear-gradient(135deg,rgba(100,150,255,.1),transparent);}
.cat-card:hover::before{opacity:1;}
.cat-card:hover{transform:translateY(-6px);border-color:rgba(255,255,255,.14);}
.cat-letter{font-family:'Playfair Display',serif;font-size:3rem;font-weight:900;opacity:.13;position:absolute;top:1rem;right:1.4rem;transition:opacity .3s;}
.cat-card:hover .cat-letter{opacity:.28;}
.cat-icon{font-size:2.3rem;margin-bottom:.7rem;}
.cat-name{font-family:'Playfair Display',serif;font-size:1.22rem;margin-bottom:.45rem;}
.cat-card.a{border-left:3px solid var(--green);}.cat-card.a .cat-name{color:var(--green);}
.cat-card.b{border-left:3px solid var(--gold);}.cat-card.b .cat-name{color:var(--gold);}
.cat-card.c{border-left:3px solid var(--red);}.cat-card.c .cat-name{color:var(--red);}
.cat-card.d{border-left:3px solid var(--blue);}.cat-card.d .cat-name{color:var(--blue);}
.cat-preview{color:var(--muted);font-size:.82rem;line-height:1.55;}
.to-advisor-btn{display:block;margin:2.5rem auto 0;padding:1rem 2.5rem;background:linear-gradient(135deg,var(--gold),var(--gold-dark));color:var(--dark);border:none;border-radius:50px;font-size:1rem;font-weight:700;cursor:pointer;font-family:'DM Sans',sans-serif;transition:all .3s;box-shadow:0 0 25px rgba(244,196,48,.25);}
.to-advisor-btn:hover{transform:scale(1.05);background:var(--gold-light);}

/* PAGE 6 — SAFE AMOUNT + CHATBOT */
#page-advisor{background:radial-gradient(ellipse at 20% 20%,#0f1a0f 0%,#0a0a0f 60%,#0f0a1a 100%);padding:2rem;min-height:100vh;display:none;flex-direction:column;}
#page-advisor.active{display:flex;}

.advisor-hero{text-align:center;padding:3rem 1rem 2rem;max-width:800px;margin:0 auto;}
.advisor-eyebrow{font-family:'JetBrains Mono',monospace;font-size:.72rem;text-transform:uppercase;letter-spacing:.2em;color:var(--green);margin-bottom:1rem;}

.safe-amount-card{background:rgba(0,200,150,.06);border:1px solid rgba(0,200,150,.25);border-radius:24px;padding:2.5rem 2rem;margin:0 auto 2.5rem;max-width:680px;width:95%;text-align:center;position:relative;overflow:hidden;}
.safe-amount-card::before{content:'';position:absolute;inset:0;background:radial-gradient(ellipse at 50% 0%,rgba(0,200,150,.08),transparent 70%);pointer-events:none;}
.safe-tag{font-family:'JetBrains Mono',monospace;font-size:.7rem;text-transform:uppercase;letter-spacing:.18em;color:var(--green);margin-bottom:.8rem;display:block;}
.safe-heading{font-family:'Playfair Display',serif;font-size:clamp(1.1rem,3vw,1.6rem);color:var(--white);line-height:1.5;margin-bottom:1.6rem;}
.safe-heading span{color:var(--green);}
.safe-formula{display:inline-flex;align-items:center;gap:.7rem;background:rgba(0,200,150,.1);border:1px solid rgba(0,200,150,.3);border-radius:14px;padding:.9rem 1.8rem;margin-bottom:1.6rem;font-family:'JetBrains Mono',monospace;font-size:1rem;color:var(--green);}
.safe-amount-display{background:var(--dark3);border-radius:16px;padding:1.4rem 2rem;display:inline-block;min-width:260px;}
.sad-label{font-family:'JetBrains Mono',monospace;font-size:.68rem;text-transform:uppercase;letter-spacing:.15em;color:var(--muted);margin-bottom:.4rem;}
.sad-value{font-family:'Playfair Display',serif;font-size:2.4rem;color:var(--green);letter-spacing:-.02em;}
.sad-month{font-size:.85rem;color:var(--muted);margin-top:.2rem;}

.breakdown-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:1rem;max-width:680px;margin:0 auto 2.5rem;width:95%;}
.breakdown-card{background:rgba(255,255,255,.03);border:1px solid rgba(255,255,255,.07);border-radius:16px;padding:1.2rem;text-align:center;transition:all .3s;}
.breakdown-card:hover{border-color:rgba(244,196,48,.2);transform:translateY(-3px);}
.bc-icon{font-size:1.6rem;margin-bottom:.5rem;}
.bc-label{font-size:.75rem;color:var(--muted);margin-bottom:.3rem;}
.bc-val{font-family:'Playfair Display',serif;font-size:1.1rem;color:var(--gold);}

/* ── CHATBOT ── */
.chatbot-section{max-width:760px;margin:0 auto;width:95%;padding-bottom:3rem;}
.chatbot-heading{font-family:'Playfair Display',serif;font-size:1.5rem;color:var(--white);margin-bottom:.3rem;display:flex;align-items:center;gap:.6rem;}
.chatbot-sub{color:var(--muted);font-size:.88rem;margin-bottom:1.2rem;}
.chatbot-box{background:rgba(255,255,255,.03);border:1px solid rgba(255,255,255,.09);border-radius:20px;overflow:hidden;display:flex;flex-direction:column;}
.chat-messages{height:360px;overflow-y:auto;padding:1.5rem;display:flex;flex-direction:column;gap:1rem;scroll-behavior:smooth;}
.chat-messages::-webkit-scrollbar{width:4px;}
.chat-messages::-webkit-scrollbar-track{background:transparent;}
.chat-messages::-webkit-scrollbar-thumb{background:rgba(255,255,255,.12);border-radius:4px;}
.msg{display:flex;gap:.8rem;max-width:88%;}
.msg.user{align-self:flex-end;flex-direction:row-reverse;}
.msg-avatar{width:32px;height:32px;border-radius:50%;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:.9rem;}
.msg.bot .msg-avatar{background:linear-gradient(135deg,var(--gold),var(--gold-dark));}
.msg.user .msg-avatar{background:linear-gradient(135deg,var(--green),#006650);}
.msg-bubble{padding:.75rem 1.1rem;border-radius:16px;font-size:.9rem;line-height:1.6;}
.msg.bot .msg-bubble{background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.07);color:var(--white);border-bottom-left-radius:4px;}
.msg.user .msg-bubble{background:rgba(0,200,150,.12);border:1px solid rgba(0,200,150,.2);color:var(--white);border-bottom-right-radius:4px;}
.msg-bubble.typing{display:flex;align-items:center;gap:.4rem;padding:.9rem 1.1rem;}
.dot{width:7px;height:7px;background:var(--muted);border-radius:50%;animation:dotbounce 1.2s infinite;}
.dot:nth-child(2){animation-delay:.2s;}
.dot:nth-child(3){animation-delay:.4s;}
@keyframes dotbounce{0%,80%,100%{transform:scale(.8);opacity:.5}40%{transform:scale(1.2);opacity:1}}

.chat-suggestions{display:flex;gap:.6rem;flex-wrap:wrap;padding:.9rem 1.2rem;border-top:1px solid rgba(255,255,255,.06);}
.chip{background:rgba(244,196,48,.08);border:1px solid rgba(244,196,48,.2);color:var(--gold);padding:.4rem .9rem;border-radius:50px;font-size:.8rem;cursor:pointer;transition:all .25s;white-space:nowrap;}
.chip:hover{background:rgba(244,196,48,.18);transform:scale(1.03);}

.chat-input-row{display:flex;gap:.6rem;padding:1rem 1.2rem;border-top:1px solid rgba(255,255,255,.06);}
.chat-input{flex:1;background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.1);border-radius:12px;padding:.75rem 1rem;color:var(--white);font-size:.9rem;font-family:'DM Sans',sans-serif;outline:none;transition:border-color .3s;}
.chat-input:focus{border-color:var(--gold);}
.chat-input::placeholder{color:rgba(136,136,170,.45);}
.send-btn{background:var(--gold);color:var(--dark);border:none;border-radius:12px;width:42px;height:42px;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:1.1rem;flex-shrink:0;transition:all .25s;}
.send-btn:hover{background:var(--gold-light);transform:scale(1.05);}
.send-btn:disabled{opacity:.5;cursor:not-allowed;transform:none;}

/* MODALS */
.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.82);backdrop-filter:blur(8px);z-index:1000;align-items:center;justify-content:center;}
.overlay.open{display:flex;animation:fadeIn .3s ease;}
.modal-box{background:var(--dark3);border:1px solid rgba(255,255,255,.11);border-radius:24px;padding:2.4rem;max-width:500px;width:92%;position:relative;animation:scaleIn .4s cubic-bezier(.34,1.56,.64,1);max-height:90vh;overflow-y:auto;}
.m-close{position:absolute;top:1rem;right:1rem;background:rgba(255,255,255,.06);border:none;color:var(--white);width:32px;height:32px;border-radius:50%;cursor:pointer;font-size:1rem;display:flex;align-items:center;justify-content:center;transition:background .2s;}
.m-close:hover{background:rgba(255,71,87,.35);}
.m-title{font-family:'Playfair Display',serif;font-size:1.55rem;margin-bottom:1.4rem;}
.m-list{list-style:none;display:flex;flex-direction:column;gap:.75rem;}
.m-list li{display:flex;align-items:center;gap:1rem;padding:.88rem 1.15rem;background:rgba(255,255,255,.03);border-radius:12px;border:1px solid rgba(255,255,255,.06);cursor:pointer;font-size:.93rem;transition:all .25s;}
.m-list li:hover{background:rgba(255,255,255,.08);transform:translateX(6px);}
.num{font-family:'JetBrains Mono',monospace;font-size:.72rem;color:var(--muted);min-width:18px;}

#detail-overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.88);backdrop-filter:blur(12px);z-index:2000;align-items:center;justify-content:center;}
#detail-overlay.open{display:flex;animation:fadeIn .25s ease;}
.detail-box{background:var(--dark3);border-radius:24px;padding:2.5rem;max-width:580px;width:93%;position:relative;animation:scaleIn .38s cubic-bezier(.34,1.56,.64,1);max-height:90vh;overflow-y:auto;border:1px solid rgba(255,255,255,.1);}
.d-close{position:absolute;top:1rem;right:1rem;background:rgba(255,255,255,.06);border:none;color:var(--white);width:32px;height:32px;border-radius:50%;cursor:pointer;font-size:1rem;display:flex;align-items:center;justify-content:center;transition:background .2s;z-index:10;}
.d-close:hover{background:rgba(255,71,87,.35);}
.d-badge{display:inline-block;font-size:.7rem;font-family:'JetBrains Mono',monospace;letter-spacing:.12em;text-transform:uppercase;padding:.3rem .8rem;border-radius:50px;margin-bottom:1rem;}
.d-name{font-family:'Playfair Display',serif;font-size:1.7rem;margin-bottom:.5rem;}
.d-tagline{color:var(--muted);font-size:.9rem;margin-bottom:1.8rem;line-height:1.55;}
.d-grid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:.9rem;margin-bottom:1.4rem;}
.d-stat{background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.07);border-radius:14px;padding:1rem;text-align:center;}
.d-stat-label{font-size:.65rem;font-family:'JetBrains Mono',monospace;color:var(--muted);text-transform:uppercase;letter-spacing:.1em;margin-bottom:.4rem;}
.d-stat-val{font-family:'Playfair Display',serif;font-size:1rem;line-height:1.3;}
.d-section{margin-bottom:1.4rem;}
.d-section-title{font-size:.68rem;font-family:'JetBrains Mono',monospace;text-transform:uppercase;letter-spacing:.15em;color:var(--muted);margin-bottom:.7rem;padding-bottom:.4rem;border-bottom:1px solid rgba(255,255,255,.06);}
.d-desc{font-size:.9rem;line-height:1.72;color:rgba(245,245,240,.85);}
.risk-bar-wrap{height:8px;background:rgba(255,255,255,.08);border-radius:4px;overflow:hidden;}
.risk-bar{height:100%;border-radius:4px;width:0%;transition:width 1s ease;}
.pros-cons{display:grid;grid-template-columns:1fr 1fr;gap:1rem;margin-bottom:1.4rem;}
.pros,.cons{background:rgba(255,255,255,.03);border-radius:14px;padding:1rem;}
.pros{border-top:2px solid var(--green);}
.cons{border-top:2px solid var(--red);}
.pc-title{font-size:.68rem;font-family:'JetBrains Mono',monospace;text-transform:uppercase;letter-spacing:.12em;margin-bottom:.7rem;}
.pros .pc-title{color:var(--green);}.cons .pc-title{color:var(--red);}
.pc-list{list-style:none;font-size:.82rem;color:rgba(245,245,240,.75);display:flex;flex-direction:column;gap:.45rem;}
.pc-list li{padding-left:1rem;position:relative;}
.pc-list li::before{content:'•';position:absolute;left:0;opacity:.5;}
.how-steps{list-style:none;counter-reset:steps;display:flex;flex-direction:column;g
