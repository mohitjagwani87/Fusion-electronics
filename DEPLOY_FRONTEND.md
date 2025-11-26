# Frontend Deploy Kaise Karein - Step by Step

## Current Situation

- ✅ Backend API deployed hai: `ecommerce-online-store-backend-xxx.vercel.app`
- ❌ Frontend deployed nahi hai

## Frontend Deploy Karne Ke Steps:

### Step 1: Vercel Mein Naya Project Banao (Frontend ke liye)

1. Go to https://vercel.com/dashboard
2. Click **"+ Add New"** → **"Project"**
3. **Import Git Repository:**
   - Select your GitHub repo: `mohitjagwani87/Ecommerce-Online-Store`
   - Click **"Import"**

### Step 2: Project Settings Configure Karo

1. **Project Name:** 
   - Kuch bhi naam de do jaise: `ecommerce-frontend` ya `fusion-electronics-website`

2. **Root Directory:**
   - **Important:** Leave it EMPTY (root directory hi use karega)
   - Ya manually set karo if needed

3. **Framework Preset:**
   - Vercel auto-detect karega **"Create React App"**
   - Agar nahi, manually select: **"Create React App"**

4. **Build Command:**
   - Set: `npm run build`
   - (Default ho sakta hai, check kar lo)

5. **Output Directory:**
   - Set: `build`
   - (Default ho sakta hai, check kar lo)

6. **Install Command:**
   - Set: `npm install`
   - (Default ho sakta hai)

### Step 3: Environment Variables (Agar Chahiye)

Frontend ko backend URL chahiye. Check karo `setupProxy.js` ya `apiClient.js` mein kaunsa URL use ho raha hai.

Agar frontend mein environment variable chahiye:
- `REACT_APP_API_URL` = Backend ka URL
  - Example: `https://ecommerce-online-store-backend-xxx.vercel.app`

### Step 4: Deploy!

1. Click **"Deploy"** button
2. Wait 2-3 minutes
3. Deployment complete hone ke baad, aapko mil jayega:
   - Frontend URL: `https://your-frontend-name.vercel.app`

### Step 5: Frontend Ko Backend Se Connect Karo

Frontend code check karo - agar hardcoded localhost URL hai, toh environment variable use karo:

1. Vercel Dashboard → Frontend Project → **Settings** → **Environment Variables**
2. Add:
   - **Key:** `REACT_APP_API_URL`
   - **Value:** `https://your-backend-url.vercel.app`
   - Environments: ☑ Production ☑ Preview ☑ Development
3. **Redeploy** karo

---

## Quick Alternative: Ek Hi Project Mein Dono Deploy Karo

Agar aap chahte ho ki ek hi Vercel project mein dono frontend aur backend ho:

1. Root level pe `vercel.json` banao (agar nahi hai)
2. Configure karo ki:
   - `/api/*` routes → backend
   - Everything else → frontend build

**But yeh complex hai.** Better hai separate projects mein deploy karo.

---

## Test Karo

Deployment ke baad:

1. Visit frontend URL: `https://your-frontend.vercel.app`
2. Home page load hona chahiye
3. Products dikhne chahiye (agar backend connected hai)
4. Navigation kaam karna chahiye

---

## Summary

**Simple Steps:**
1. Vercel → New Project
2. GitHub repo import karo
3. Build command: `npm run build`
4. Output: `build`
5. Deploy!
6. Environment variable add karo (backend URL)
7. Redeploy

**Time:** 5-10 minutes

---

**Need help?** Batao agar koi step mein issue ho!

