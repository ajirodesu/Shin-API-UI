# Shin API UI

Shin API UI is a lightweight, dark-themed API documentation and testing dashboard built with **Node.js**, **Express**, **Tailwind CSS**, and vanilla **JavaScript**.  
It lets you list, explore and test REST-style endpoints from a single, responsive interface.

> Note: The project files (index, settings and API modules) are included in this repo. See the **Live Demo** and **Usage** below.

---

## 🚀 Features

- Interactive API testing panel — send requests and inspect responses in-app.  
- Dark, responsive UI and mobile-first layout.  
- Autodiscovery of API modules placed in the repository's `api/` directory.  
- Live response viewer with pretty-printed JSON and copy-to-clipboard.  
- Statistics summary (counts and method breakdown).  
- Configurable via `settings.js` in the repository root.  
- Deploy-ready (includes `vercel.json` for Vercel deployments).

---

## 🔗 Live Demo

A demo is available here:

> Comming Soon. :contentReference[oaicite:0]{index=0}

---

## 🛠️ Quickstart

### Prerequisites

- Node.js (v14 or later)  
- npm or yarn

### Install & run

```bash
# Clone this repository
git clone https://github.com/ajirodesu/Shin-API-UI.git

# Enter the project
cd Shin-API-UI

# Install dependencies
npm install
# or
yarn install

# Start the server
npm start
# or
yarn start
````

By default the dashboard/server runs on `http://localhost:4000` (the project expects port 4000 unless overridden). ([GitHub][1])

---

## ⚙️ Configuration

Edit `settings.js` in the project root to customize the UI and initial notifications. Example shape (this repository includes a `settings.js` you can reuse):

```js
module.exports = {
  name: 'Iwato Rest API',       // display name shown in the header
  version: '1.0.0',             // interface version string
  description: 'Modern API explorer and tester.',
  icon: '/docs/images/icon.png',     // header icon path (relative to public/doc assets)
  author: 'ShinDesu'     ,     // display author (or 'auto' to fetch from GitHub)
  telegram: 'https://t.me/+AQO22J2q6KBlNWM1'
};
```

`settings.js` lives in the repo root. ([GitHub][2])

---

## 📁 Where to place endpoints

This project auto-discovers API modules from the repository's `api/` directory (not `/endpoints`). Each API module should export a `meta` object and an `onStart` function (see example below). Check the repo `api/` folder for examples. ([GitHub][3])

### Example: Hello endpoint

```js
// /api/hello.js
const meta = {
  name: 'hello',            // unique name used by the UI
  desc: 'Returns a greeting message',
  method: 'get',            // HTTP method (get, post, put, delete, etc.)
  category: 'examples',     // used to group endpoints in the sidebar
  guide:['add a name'],
  params: ['name']          // parameter names expected by the endpoint
};

async function onStart({ req, res }) {
  const { name } = req.query;
  const greeting = name ? `Hello, ${name}!` : 'Hello, World!';
  return res.json({
    message: greeting,
    timestamp: new Date().toISOString()
  });
}

module.exports = { meta, onStart };
```

Place the file under `api/` and restart the server. The UI will list it under the `Examples` (or the category you specify).

---

## 🧭 Dashboard overview

* **Home Page** — categorized endpoints.
* **Endpoint panel** — description, parameter input form and **Execute** button.
* **Response viewer** — pretty-printed JSON with copy functionality.
* **Statistics** — cards summarizing endpoints and HTTP method usage.

---

## 🔁 Deploying

The repository includes `vercel.json` for quick deployment to Vercel. The demo above is deployed at the URL listed earlier. ([GitHub][1])

---

## 📜 License

This project is licensed under the **MIT License**. See `LICENSE` in the repo. ([GitHub][1])

---

## ❤️ Credits & authors

* **Rynn** — original creator/author (upstream).
* **Lenwy** — concept inspiration.
* **AjiroDesu** — UI/UX redesign and previous enhancements and repository owner / current maintainer.

---

## 🔧 Troubleshooting

* Server fails to start: ensure Node version ≥ 14 and run `npm install` again.
* New API not visible: confirm the file is inside `api/`, exports `meta` and `onStart`, and restart the server.
* Port conflict: change environment `PORT` or edit the start script as needed.

---