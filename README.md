# 💌 Say It For You — sayitforyou.fun

**Say It For You** is a mobile-first, privacy-focused web application designed to help shy, introverted, or emotionally reserved individuals express unsaid feelings anonymously—especially over Instagram. 

This project is handcrafted using the traditional web tech stack: `HTML`, `CSS`, `Vanilla JavaScript`, and `Google Apps Script` (for backend handling). No libraries. No dependencies. Just pure, human-crafted simplicity.

---

## 🎯 Project Objective

To provide a safe, expressive digital space for those who struggle to say things out loud—whether it's a:

- Confession of love 💘  
- Guilt-filled apology 💔  
- Quiet appreciation 🫶  
- Unspoken truth 😔  

Messages are submitted anonymously and delivered either via Instagram Reel, DM, or static post—through our IG handle [@sayitforyou.fun](https://instagram.com/sayitforyou.fun).

---

## 🔧 Tech Stack

| Layer       | Tech                              |
|------------|------------------------------------|
| Frontend   | HTML5 + CSS3 + Vanilla JS          |
| Backend    | Google Apps Script + Google Sheets |
| Hosting    | Vercel (Static Hosting)            |
| Database   | Google Sheets (as a message log)   |

---

## 📱 Features

- 💌 Emotion-first UI/UX inspired by iOS/Instagram style
- 📱 Mobile-first responsive layout
- 📝 Anonymous message form with dropdowns
- 🔐 Manual review of all content (no automation)
- 💬 Soft CTA, minimal color palette, emoji-supported
- ✅ No login / no signup required
- 🎯 100% Free + Human-powered platform

---

## 🚀 Pages & Structure

📁 sayitforyou/
│
├── index.html # Single-page app with embedded HTML/CSS/JS
├── assets/
│ ├── favicon.ico # Browser tab icon
│ ├── icons/ # SVG UI icons (send, heart, close, etc.)
│ └── images/ # Optional backgrounds / screenshots
└── Code.gs # Google Apps Script backend handler



---

## 📩 How the App Works

1. **User lands on homepage**
2. Taps “We say it for you” → Opens message form
3. Fills in:
   - Sender IG handle (optional)
   - Receiver IG handle (required)
   - Message content
   - Message type (Confession, Apology, etc.)
   - Anonymous option
   - Delivery method
4. Message is submitted via Google Apps Script
5. Team reviews & delivers the message via Instagram (Reel, DM, or Post)

---

## 🔐 Privacy & Safety

- No personal emails or logins collected
- Only IG handles are used for message delivery
- Anonymity is optional
- Every message is manually reviewed before delivery
- No automation, no AI, no data selling

---

## 🧠 Philosophy

Say It For You is a voice for the quiet—those who carry emotions they can’t always speak. We believe everyone deserves to be heard, even silently.

---

## 🛠 Setup Instructions (For Developers)

1. **Clone the repo**
   ```bash
   git clone https://github.com/yourusername/sayitforyou.git
   cd sayitforyou
Set up Google Apps Script:

Create a Google Sheet → Open Apps Script → Paste Code.gs

Deploy as Web App (Execute as: Me, Access: Anyone)

Copy Web App URL

Update index.html

Find const SCRIPT_URL = '' and paste the Web App URL.

Deploy the site on Vercel (or any static host)

🧪 Testing Checklist
✅ Mobile responsiveness
✅ IG handle validation
✅ Message length checks
✅ Submission success feedback
✅ Backend connectivity
✅ Fallback messages

🌐 Live Demo
Live URL: https://sayitforyou.fun
Instagram: @sayitforyou.fun

🧩 Future Scope
In-app message tracker (delivered/read status)

AI-assisted content styling (optional)

Dashboard for users (for sent/received messages)

Themed campaigns like "Apology Week", "Closure Days"

Community stories & healing threads

🧑‍💻 Author
Abhishek Singh Shekhawat
Portfolio
GitHub
LinkedIn

⭐ Contributions
This is a solo project for now. If you feel connected to the mission or want to support with content, dev, or testing—reach out!

📄 License
MIT License — free to use, remix, and contribute with proper credit.

🙏 Support Us
If you like this initiative, help us grow:

Follow our Instagram

Share the project with your friends

Submit your own anonymous message 🫶



---

### ✅ What's next?

Let me know if you'd like:
- `Code.gs` (Apps Script backend)  
- `README` translated into Hindi for local audiences  
- CI/CD setup instructions for Vercel

I'll generate any next file instantly on your signal.
