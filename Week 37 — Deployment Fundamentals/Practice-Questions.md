# Week 37: Deployment Fundamentals -- Practice Questions

**Total Questions: 20**
- Multiple Choice Questions: 10
- Short Answer Questions: 5
- Practical Exercises: 5

---

## Multiple Choice Questions (MCQs)

### Q1. What is deployment in web development?

- A) Writing code on your local machine
- B) Testing your application in the browser
- C) Making your application available on the internet for users to access
- D) Installing Node.js on your computer

<details>
<summary>View Answer</summary>

**C) Making your application available on the internet for users to access**

Deployment is the process of taking your application from your local development environment and publishing it to a remote server where it can be accessed by anyone on the internet.

</details>

---

### Q2. What does `npm run build` do for a Vite + React application?

- A) Starts the development server with hot reload
- B) Installs all project dependencies
- C) Compiles and minifies the code into an optimized `/dist` folder for production
- D) Deploys the application to Vercel

<details>
<summary>View Answer</summary>

**C) Compiles and minifies the code into an optimized `/dist` folder for production**

The build command transforms your JSX, compiles your CSS, minifies JavaScript, and produces static files ready to be served by a web server or CDN.

</details>

---

### Q3. Why must your Express server use `process.env.PORT` instead of a hardcoded port number?

- A) Hardcoded ports are slower
- B) Hosting platforms like Render assign their own port dynamically
- C) It is a JavaScript syntax requirement
- D) Hardcoded ports do not work with MongoDB

<details>
<summary>View Answer</summary>

**B) Hosting platforms like Render assign their own port dynamically**

Hosting platforms set the PORT environment variable to the port they allocate for your service. If you hardcode a port like `5000`, the platform cannot route traffic to your application.

</details>

---

### Q4. What does DNS stand for, and what does it do?

- A) Data Network Storage -- stores website files
- B) Domain Name System -- translates domain names into IP addresses
- C) Digital Node Service -- connects servers together
- D) Domain Network Security -- protects websites from hackers

<details>
<summary>View Answer</summary>

**B) Domain Name System -- translates domain names into IP addresses**

DNS works like a phone book for the internet. When you type `google.com`, DNS resolves it to an IP address like `142.250.80.46` so your browser knows which server to connect to.

</details>

---

### Q5. Which file must you add to `.gitignore` to prevent leaking secrets?

- A) `package.json`
- B) `server.js`
- C) `.env`
- D) `index.html`

<details>
<summary>View Answer</summary>

**C) `.env`**

The `.env` file contains sensitive information like database passwords, API keys, and JWT secrets. It should never be committed to version control. Always add `.env` to your `.gitignore` file.

</details>

---

### Q6. On Vercel, what prefix must frontend environment variables use in a Vite project?

- A) `REACT_APP_`
- B) `NEXT_PUBLIC_`
- C) `VITE_`
- D) `ENV_`

<details>
<summary>View Answer</summary>

**C) `VITE_`**

Vite only exposes environment variables that start with `VITE_` to your client-side code. For example, `VITE_API_URL` is accessible via `import.meta.env.VITE_API_URL` in your React components.

</details>

---

### Q7. What is the main drawback of Render's free tier for backend hosting?

- A) It does not support Node.js
- B) It does not provide HTTPS
- C) The service spins down after 15 minutes of inactivity, causing cold starts
- D) It cannot connect to MongoDB Atlas

<details>
<summary>View Answer</summary>

**C) The service spins down after 15 minutes of inactivity, causing cold starts**

On the free tier, Render puts your service to sleep when it receives no traffic for 15 minutes. The first request after inactivity can take 30-50 seconds as the service wakes up.

</details>

---

### Q8. What is MongoDB Atlas?

- A) A JavaScript library for querying databases
- B) A locally installed MongoDB database
- C) A cloud-hosted MongoDB database service
- D) A frontend framework for building UIs

<details>
<summary>View Answer</summary>

**C) A cloud-hosted MongoDB database service**

MongoDB Atlas is the official cloud database service from MongoDB. It provides managed MongoDB clusters that are accessible from anywhere, with automatic backups, scaling, and monitoring.

</details>

---

### Q9. What does HTTPS provide that HTTP does not?

- A) Faster loading speed
- B) Encryption of data between browser and server
- C) Better HTML rendering
- D) Access to more CSS features

<details>
<summary>View Answer</summary>

**B) Encryption of data between browser and server**

HTTPS uses SSL/TLS encryption to protect data in transit. This prevents attackers from reading sensitive information like passwords and credit card numbers as they travel between the user's browser and your server.

</details>

---

### Q10. In a deployed MERN stack application, which component is deployed separately from the others?

- A) React frontend and Express backend are deployed together on the same platform
- B) React frontend is deployed on Vercel/Netlify, Express backend on Render, and MongoDB on Atlas -- all separately
- C) Only the database needs separate deployment
- D) Everything runs on a single Vercel deployment

<details>
<summary>View Answer</summary>

**B) React frontend is deployed on Vercel/Netlify, Express backend on Render, and MongoDB on Atlas -- all separately**

In a typical MERN deployment, each layer is hosted independently. The frontend is served as static files from a CDN (Vercel/Netlify), the backend runs as a web service (Render/Railway), and the database is hosted on MongoDB Atlas.

</details>

---

## Short Answer Questions

### Q11. Explain the difference between development and production environments. List at least three differences.

<details>
<summary>View Answer</summary>

**Development** is the local environment where you build and test your application. **Production** is the live environment where real users access your app. Key differences include:

1. **URL**: Development uses `localhost:3000`, production uses a real domain like `myapp.com`.
2. **Error handling**: Development shows detailed stack traces for debugging, while production shows user-friendly error messages.
3. **Performance**: Development serves unoptimized code with source maps, while production serves minified, compressed, and cached files.
4. **Database**: Development often uses a local database, while production uses a cloud database (MongoDB Atlas).
5. **Security**: Development may use HTTP, while production must use HTTPS.

</details>

---

### Q12. What is a CNAME record, and when would you use one for your deployed website?

<details>
<summary>View Answer</summary>

A **CNAME (Canonical Name) record** is a DNS record that maps one domain name to another domain name. Instead of pointing directly to an IP address (like an A record), it points to another domain.

You would use a CNAME record when connecting a custom domain to a platform like Vercel or Netlify. For example:

```
www.myportfolio.com  CNAME  myportfolio.vercel.app
```

This tells DNS that `www.myportfolio.com` should resolve to the same IP address as `myportfolio.vercel.app`. When Vercel changes their server IPs, your domain automatically follows.

</details>

---

### Q13. Why should you never commit your `.env` file to GitHub? What could go wrong?

<details>
<summary>View Answer</summary>

You should never commit `.env` files because they contain sensitive secrets such as:

- **Database passwords** (MongoDB connection strings)
- **JWT secrets** (used to sign authentication tokens)
- **API keys** (for services like Stripe, SendGrid, or AWS)

If these are pushed to a public GitHub repository, attackers can:

1. Access and steal all data from your database
2. Forge authentication tokens to impersonate any user
3. Use your paid API keys, running up large bills
4. Deploy malicious code using your credentials

Even in private repositories, it is bad practice because team members may have different credentials, and secrets should be managed through the hosting platform's environment variable settings.

</details>

---

### Q14. Describe the complete flow of a deployment when you `git push` to a repository connected to Vercel.

<details>
<summary>View Answer</summary>

When you `git push` to a GitHub repository connected to Vercel, the following happens automatically:

1. **Webhook triggered**: GitHub sends a webhook notification to Vercel that new code has been pushed.
2. **Code pulled**: Vercel clones or pulls the latest code from the repository.
3. **Dependencies installed**: Vercel runs `npm install` to install all packages listed in `package.json`.
4. **Build process**: Vercel runs `npm run build` (or the configured build command) to compile and optimize the application.
5. **Deployment**: The built files (from the `dist/` directory) are uploaded to Vercel's global CDN.
6. **URL assigned**: The deployment is assigned a unique URL (e.g., `myapp-abc123.vercel.app`).
7. **Traffic switched**: If this is the production branch, Vercel routes the main domain to this new deployment.

The entire process typically takes 30-90 seconds.

</details>

---

### Q15. What steps are needed to allow your Render-hosted backend to communicate with your Vercel-hosted frontend?

<details>
<summary>View Answer</summary>

To allow cross-origin communication between your frontend (Vercel) and backend (Render), you need to:

1. **Configure CORS on the backend**: Install and configure the `cors` middleware in your Express app to allow requests from your Vercel frontend URL:

```javascript
const cors = require('cors');
app.use(cors({
  origin: 'https://myapp.vercel.app',
  credentials: true
}));
```

2. **Set the API URL on the frontend**: Add the Render backend URL as an environment variable in Vercel:

```
VITE_API_URL = https://my-api.onrender.com/api
```

3. **Use the environment variable in frontend API calls**:

```javascript
const API_URL = import.meta.env.VITE_API_URL;
const response = await fetch(`${API_URL}/posts`);
```

4. **Ensure HTTPS on both sides**: Both Vercel and Render provide automatic HTTPS, which is required for secure cross-origin requests.

</details>

---

## Practical Exercises

### Exercise 1: Deploy a React App to Vercel

**Objective:** Deploy a Vite + React application to Vercel and access it via a live URL.

**Steps:**

1. Create a new Vite + React project (or use an existing one):

```bash
npm create vite@latest my-deploy-test -- --template react
cd my-deploy-test
npm install
```

2. Modify `src/App.jsx` to display your name and a message:

```jsx
function App() {
  return (
    <div style={{ textAlign: 'center', marginTop: '100px' }}>
      <h1>Hello, World!</h1>
      <p>This is my first deployed React application.</p>
      <p>Deployed on: {new Date().toLocaleDateString()}</p>
    </div>
  );
}

export default App;
```

3. Push to a GitHub repository
4. Go to [vercel.com](https://vercel.com) and import the repository
5. Verify build settings and click **Deploy**
6. Open the live URL and confirm the app works

**Expected Result:** A live URL like `https://my-deploy-test.vercel.app` showing your React application.

<details>
<summary>Verification Checklist</summary>

- [ ] Project builds locally with `npm run build` without errors
- [ ] Code is pushed to GitHub
- [ ] Vercel project is created and linked to the GitHub repo
- [ ] Build settings are correct (Build: `npm run build`, Output: `dist`)
- [ ] Deployment completed successfully
- [ ] Live URL is accessible and shows the correct content
- [ ] Page loads over HTTPS (padlock icon in browser)

</details>

---

### Exercise 2: Deploy an Express API to Render

**Objective:** Deploy an Express.js backend API to Render and test it with a browser or Postman.

**Steps:**

1. Create a simple Express API:

```javascript
// server.js
const express = require('express');
const cors = require('cors');

const app = express();
app.use(cors());
app.use(express.json());

const posts = [
  { id: 1, title: 'First Post', content: 'Hello from my deployed API!' },
  { id: 2, title: 'Second Post', content: 'Deployment is working!' }
];

app.get('/', (req, res) => {
  res.json({ status: 'API is running', timestamp: new Date() });
});

app.get('/api/posts', (req, res) => {
  res.json(posts);
});

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => console.log(`Server on port ${PORT}`));
```

2. Create a `package.json` with a proper `start` script
3. Push to GitHub
4. On Render, create a **New Web Service** linked to the repo
5. Set Build Command to `npm install` and Start Command to `node server.js`
6. Deploy and test the endpoints

**Expected Result:** Visiting `https://your-api.onrender.com/api/posts` returns JSON data.

<details>
<summary>Verification Checklist</summary>

- [ ] `package.json` has `"start": "node server.js"` script
- [ ] Server uses `process.env.PORT` (not hardcoded)
- [ ] Code is pushed to GitHub
- [ ] Render web service is created and linked
- [ ] Build and start commands are configured correctly
- [ ] Deployment log shows no errors
- [ ] Root endpoint (`/`) returns a success response
- [ ] `/api/posts` endpoint returns the posts array as JSON
- [ ] Response includes proper `Content-Type: application/json` header

</details>

---

### Exercise 3: Configure Environment Variables

**Objective:** Set up environment variables for both frontend and backend in a deployed MERN application.

**Steps:**

1. In your Express backend, use environment variables for configuration:

```javascript
// server.js
const mongoose = require('mongoose');

const MONGODB_URI = process.env.MONGODB_URI;
const JWT_SECRET = process.env.JWT_SECRET;

if (!MONGODB_URI) {
  console.error('MONGODB_URI is not defined in environment variables');
  process.exit(1);
}

mongoose.connect(MONGODB_URI)
  .then(() => console.log('Connected to MongoDB'))
  .catch(err => console.error('Connection failed:', err));
```

2. Create a local `.env` file (DO NOT commit this):

```env
MONGODB_URI=mongodb://localhost:27017/mydb
JWT_SECRET=local_dev_secret
PORT=5000
```

3. Verify `.env` is in `.gitignore`
4. On Render, add the production environment variables through the dashboard
5. On Vercel, add `VITE_API_URL` pointing to your Render backend URL
6. Verify that both frontend and backend read from environment variables correctly

<details>
<summary>Verification Checklist</summary>

- [ ] `.env` file exists locally with all required variables
- [ ] `.env` is listed in `.gitignore`
- [ ] Code uses `process.env.VARIABLE_NAME` (not hardcoded values)
- [ ] Backend validates that required env vars exist on startup
- [ ] Environment variables are set in Render dashboard
- [ ] `VITE_API_URL` is set in Vercel dashboard
- [ ] Frontend correctly uses `import.meta.env.VITE_API_URL`
- [ ] Both apps work correctly with their respective environment variables

</details>

---

### Exercise 4: Set Up MongoDB Atlas for Production

**Objective:** Create a free MongoDB Atlas cluster and connect it to your deployed Express backend.

**Steps:**

1. Sign up at [mongodb.com/atlas](https://www.mongodb.com/atlas)
2. Create a free M0 cluster
3. Create a database user with a strong password (no special characters)
4. Configure Network Access to allow all IPs (`0.0.0.0/0`)
5. Get the connection string and update it with your password and database name
6. Add the connection string as `MONGODB_URI` in Render's environment variables
7. Deploy and verify the connection by checking Render's logs

```
Expected connection string format:
mongodb+srv://myuser:mypassword@cluster0.abc123.mongodb.net/myPortfolioDB?retryWrites=true&w=majority
```

8. Test by creating data through your API and verifying it appears in Atlas

<details>
<summary>Verification Checklist</summary>

- [ ] Atlas account created
- [ ] Free M0 cluster provisioned and running
- [ ] Database user created with Read/Write permissions
- [ ] Network Access allows `0.0.0.0/0` (or your server's IP)
- [ ] Connection string copied and password replaced
- [ ] `MONGODB_URI` set in Render environment variables
- [ ] Backend deployment logs show "Connected to MongoDB Atlas"
- [ ] Data created via API appears in Atlas dashboard (Collections tab)
- [ ] No connection errors in the deployment logs

</details>

---

### Exercise 5: Connect a Custom Domain

**Objective:** Connect a custom domain (or subdomain) to your Vercel-deployed frontend.

**Steps:**

1. Purchase a domain from any registrar (Namecheap, Cloudflare, etc.) or use a free subdomain service for practice
2. In your Vercel project, go to **Settings** > **Domains**
3. Add your custom domain (e.g., `myportfolio.com`)
4. Vercel will provide DNS records to configure:

```
Type: A
Name: @
Value: 76.76.21.21

Type: CNAME
Name: www
Value: cname.vercel-dns.com
```

5. Go to your domain registrar's DNS settings
6. Add the A record and CNAME record provided by Vercel
7. Wait for DNS propagation (check with `nslookup myportfolio.com` or [dnschecker.org](https://dnschecker.org))
8. Verify HTTPS is automatically configured by Vercel

<details>
<summary>Verification Checklist</summary>

- [ ] Domain purchased or subdomain obtained
- [ ] Domain added in Vercel project settings
- [ ] DNS records (A and/or CNAME) added at the registrar
- [ ] DNS propagation completed (verified with DNS checker)
- [ ] Website loads at the custom domain
- [ ] HTTPS works automatically (padlock icon visible)
- [ ] Both `myportfolio.com` and `www.myportfolio.com` work
- [ ] Old `.vercel.app` URL still works as well

</details>

---

## Summary

| Category | Count |
|---|---|
| Multiple Choice Questions | 10 |
| Short Answer Questions | 5 |
| Practical Exercises | 5 |
| **Total** | **20** |
