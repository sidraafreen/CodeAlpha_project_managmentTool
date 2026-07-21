# Flowdeck

A full-stack, real-time project management tool (Trello/Asana style) with a
dark, modern UI. Built with Node.js/Express on the backend and vanilla
HTML/CSS/JS on the frontend — no build step required.

## Features

- **Auth system** — register/login with hashed passwords (bcrypt) and JWT sessions
- **Projects** — create group projects, invite teammates by email, remove members
- **Kanban board** — drag-and-drop task cards across To do / In progress / Done
- **Tasks** — title, description, priority, due date, assignee
- **Comments** — threaded discussion on every task
- **Notifications** — in-app notification bell for assignments, comments, invites
- **Real-time updates** — powered by Socket.IO: boards update live for every
  member the instant a task moves, a comment is posted, or a member is added
- **Responsive, dark-themed UI** — works on desktop, tablet and mobile, with a
  custom logo and icon set (all inline SVG, no external icon fonts)

## Requirements

- [Node.js](https://nodejs.org) v16 or newer (includes npm)

## Setup

1. Unzip this project and open a terminal in the `flowdeck` folder.
2. Install dependencies:

   ```bash
   npm install
   ```

3. Start the server:

   ```bash
   npm start
   ```

4. Open your browser at **http://localhost:4000**

That's it — no database server, Docker, or extra configuration needed. Data is
stored in a local file at `server/data/db.json`, which is created
automatically the first time you run the app.

### Changing the port

```bash
PORT=5000 npm start
```

### Trying it with a teammate

Open the app in two different browsers (or a normal + incognito window),
register two different accounts, create a project in one, invite the other
account's email as a member from the **Members** button on the board, then
watch tasks/comments sync live between both windows.

## Project structure

```
flowdeck/
├── server/
│   ├── server.js          # Express app + Socket.IO wiring
│   ├── auth.js             # JWT helpers & middleware
│   ├── db.js                # simple file-backed JSON data store
│   ├── notify.js            # notification helper
│   ├── routes/
│   │   ├── auth.js           # register / login / me / user search
│   │   ├── projects.js       # project CRUD + members
│   │   ├── tasks.js          # task CRUD + drag-and-drop move
│   │   └── comments.js       # comments on tasks
│   └── data/db.json        # auto-created local data file
└── public/
    ├── index.html          # login / register
    ├── dashboard.html      # project overview
    ├── board.html          # kanban board
    ├── css/style.css       # dark theme, responsive layout
    └── js/
        ├── api.js            # fetch wrapper + helpers
        ├── icons.js           # inline SVG icon set
        ├── notifications.js   # shared sidebar/topbar/notifications/socket
        ├── dashboard.js       # dashboard page logic
        └── board.js           # kanban board logic
```

## Notes

- This project stores data in a JSON file rather than a full database server,
  so it runs anywhere Node.js runs with zero extra setup. For production use
  at scale, swap `server/db.js` for a real database (Postgres, MongoDB, etc.)
  behind the same function signatures.
- Set a real `JWT_SECRET` environment variable before deploying anywhere
  public:

  ```bash
  JWT_SECRET=your-long-random-secret npm start
  ```
