# CampusPilot AI 🎓

### Turn campus circulars into clear checklists and deadlines.

CampusPilot AI is an academic action center for students. Paste or upload a campus notice (an exam circular, workshop announcement, fee notice) and it extracts the event, venue, deadline, fees, and a step-by-step checklist of what you need to do. Save those steps to a personal task list, track what is urgent, and export deadlines to your calendar.

Built for **GitHub Copilot Dev Days — OSEN Noida 2026**.

## ✨ Key Features

- **Notice Analyzer:** Extracts event, venue, deadline, fees, issuing department, and action items from a notice. A built-in local rule engine works offline; Gemini can be enabled for higher-quality extraction.
- **Gemini-Powered Parsing:** Handles PDF and image notices (PNG, JPG, WEBP) through a server-side Gemini call. Fields not present in the notice are reported as "Not stated" rather than guessed.
- **Action Center:** Save extracted steps as tasks, mark them urgent or complete, add your own tasks, and clear finished ones.
- **Circulars & Archive:** Keep parsed notices and re-open the original notice text.
- **Notifications:** A drawer of campus alerts with unread and urgent states.
- **Calendar Export:** Download your deadlines as an `.ics` file for Google Calendar, Outlook, or Apple Calendar.
- **Local Persistence:** Tasks, notices, and alerts are stored in your browser's `localStorage`.

## 🛠️ Tech Stack

| Layer | Technology |
| --- | --- |
| Frontend | React 19, TypeScript, Vite |
| Styling | Tailwind CSS 4, Motion (animations), Lucide React (icons) |
| Backend | Node.js, Express 4, run with `tsx` |
| AI | Google Gemini via `@google/genai` (server-side only) |
| File handling | `fflate` for reading `.docx` uploads |
| Config | `dotenv` |
| Dev tools | Visual Studio Code, GitHub Copilot |

The Vite dev server runs as middleware inside the Express server, so one command starts both the app and the API.

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (current LTS, 22 or newer recommended)
- npm (included with Node.js)

### Installation

1. Clone the repository and move into it:

   ```bash
   git clone <YOUR_GITHUB_REPOSITORY_URL>
   cd CampusPilot-AI
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. (Optional) Enable Gemini parsing. Create a key in [Google AI Studio](https://aistudio.google.com/apikey), copy `.env.example` to `.env`, and set your key:

   ```env
   GEMINI_API_KEY=paste_your_key_here
   ```

   Keep the key private. Never commit it or put it in frontend code; `.env` is listed in `.gitignore`. Without a key, the app still runs and PDF/image analysis returns a "not configured" message.

4. Start the development server:

   ```bash
   npm run dev
   ```

5. Open <http://localhost:3000>.

## 📎 Notice Uploads

- Text (`.txt`, `.md`) and Word (`.docx`) files are read in the browser as text.
- PDF and image files (`.pdf`, `.png`, `.jpg`, `.jpeg`, `.webp`) are sent to the Node server and analyzed by Gemini, so they need `GEMINI_API_KEY`.
- Uploads are limited to 8 MB. Legacy `.doc` files are not supported; save them as `.docx` or PDF first.

## 📦 Scripts

| Command | What it does |
| --- | --- |
| `npm run dev` | Starts the Express server with the Vite dev server (port 3000) |
| `npm run build` | Builds the frontend into `dist/` |
| `npm start` | Runs the server; set `NODE_ENV=production` to serve `dist/` (port from `PORT`, default 8080) |
| `npm run lint` | Type-checks the project with `tsc --noEmit` |
| `npm run clean` | Removes `dist/` and `server.js` |

## ☁️ Deployment

Deploy it as a Node service, not a static site, because the Gemini calls run in `server.ts`.

1. `npm install && npm run build`
2. Set `NODE_ENV=production` and `GEMINI_API_KEY` in your host's environment or secrets settings.
3. Start with `npm start`.

A local `.env` file only applies to your own machine, so add the key on the host and redeploy.

## 🎯 Project Objective

College notices are scattered, long, and easy to misread. CampusPilot AI turns them into short, trustworthy checklists with the deadlines that matter, so students spend less time decoding circulars and miss fewer deadlines.

## 🔮 Future Improvements

- Parse real deadline dates so calendar events use the actual due date.
- Add more notice presets and department-specific rules.
- Sync tasks across devices with a backend database.
- Improve accessibility and responsive design.

## 👨‍💻 Author

**Aryan Sharma**  
First-year Computer Science Engineering student  
Galgotias College of Engineering and Technology

## 📄 License

Released under the [MIT License](LICENSE).
