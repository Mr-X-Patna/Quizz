# QuizzMaster

QuizzMaster is a full-stack quiz learning application. Users can create an account, explore quizzes, track their results, and compare scores on a leaderboard. The app also includes profile tools, an AI-powered chatbot, and a resume builder.

## Features

- Account registration, login, email verification, and password reset
- Quiz catalog and quiz generation
- Quiz submissions, results, and personal performance summaries
- User profiles and avatar uploads
- Leaderboard
- AI chatbot powered by Google Gemini, ChatGpt (under processing)
- Resume builder
- Responsive React interface with light/dark theme support

## Technology

- **Frontend:** React, Vite, React Router, Axios
- **Backend:** Node.js, Express
- **Database:** MongoDB with Mongoose
- **Authentication:** JSON Web Tokens
- **Integrations:** Google Gemini, Nodemailer, ChatGpt

## Project structure

```text
.
├── Back/
│   ├── controllers/
│   ├── data/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── seeds/
│   ├── utils/
│   ├── app.js
│   └── server.js
└── Front/
    ├── public/
    └── src/
        ├── components/
        ├── pages/
        ├── services/
        └── styles/
```

## Prerequisites

- Node.js (a current LTS release is recommended)
- npm
- A MongoDB database (local or MongoDB Atlas)
- Optional: Google Gemini and OpenWeather API keys for the corresponding integrations
- Optional: a Gmail account configured for SMTP if you want verification and password-reset email delivery

## Getting started

### 1. Configure the backend

In a terminal:

```bash
cd Back
npm install
```

Create `Back/.env`:

```dotenv
PORT=5000
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster>/<database>
JWT_SECRET=replace-with-a-long-random-secret
EMAIL_USER=your-email@example.com
EMAIL_PASS=your-email-app-password
FRONTEND_URL=http://localhost:5173
VITE_FRONTEND_URL=http://localhost:5173
```

`EMAIL_USER` and `EMAIL_PASS` are only needed for email delivery. Use an app password where required by your email provider. Set `VITE_FRONTEND_URL` to the frontend origin to allow it through the backend's CORS configuration. `FRONTEND_URL` is used when generating email-verification links.

Start the API:

```bash
npm run dev
```

The backend listens on port `5000` by default. Its root health check is available at `http://localhost:5000/`.

### 2. Configure the frontend

In a second terminal:

```bash
cd Front
npm install
```

Create `Front/.env`:

```dotenv
VITE_BACKEND_URL=http://localhost:5000
VITE_GEMINI_API_KEY=your-gemini-api-key
VITE_OPENAI_API_KEY=your-gemini-api-key
VITE_WEATHER_API_KEY=your-openweather-api-key
```

The Gemini and weather integrations need their corresponding keys. The Gemini key is used by frontend code and is therefore visible to users of the built app; restrict it using the provider's available API and usage controls. Never put server credentials, database passwords, or email passwords in `VITE_` variables.

Start the development server:

```bash
npm run dev
```

Vite prints the local frontend URL (typically `http://localhost:5173`) in the terminal.

## Available scripts

Run these from the relevant directory:

| Directory | Command | Description |
| --- | --- | --- |
| `Front` | `npm run dev` | Start the Vite development server |
| `Front` | `npm run build` | Create a production build in `Front/dist` |
| `Front` | `npm run preview` | Preview the production build locally |
| `Front` | `npm run lint` | Run ESLint |
| `Back` | `npm run dev` | Start the API with Nodemon |
| `Back` | `npm start` | Start the API |
| `Back` | `npm test` | Run the Node.js test suite |

## API overview

The backend exposes its API under `/api`:

| Endpoint prefix | Purpose |
| --- | --- |
| `/api/auth` | Registration, login, email verification, password reset, and current-user details |
| `/api/quizzes` | Browse quizzes, generate quizzes, and submit answers |
| `/api/results` | Quiz results and user performance summaries |
| `/api/user` | Profile and avatar management |
| `/api/leaderboard` | Leaderboard data |

Most profile, quiz-submission, and personal-result actions require a valid bearer token.

## Quiz data

Quiz seed data is stored in `Back/data/`. To load the bundled quiz set into MongoDB, run this from `Back`:

```bash
node seeds/quizSeeder.js
```

**Warning:** the seeder deletes the existing quiz documents in the configured database before importing the bundled data. Back up any quiz data you need before running it.

## Security notes

- Keep `.env` files, API keys, passwords, and database connection strings out of Git.
- Use strong, unique values for `JWT_SECRET` and your database credentials.
- Rotate any credentials that have already been committed, shared, or exposed.
- Configure production CORS origins and API-key restrictions for your deployment.

## Contributing

Contributions are welcome. Please open an issue to discuss larger changes, and include relevant test or lint results with pull requests.
