# Quick Setup: Environment Variables in Vercel

## 🎯 Step-by-Step (5 minutes)

### 1. Go to Vercel Dashboard
- Visit: https://vercel.com/dashboard
- Sign in if needed

### 2. Open Your Project
- Click on your project name (probably "ecommerce-backend" or similar)

### 3. Open Settings
- Click **"Settings"** tab at the top

### 4. Click Environment Variables
- In left sidebar, click **"Environment Variables"**

### 5. Add Each Variable
Click **"+ Add New"** for each:

#### Variable 1: MONGO_URI
```
Key: MONGO_URI
Value: [paste your MongoDB connection string]
Environments: ✓ Production ✓ Preview ✓ Development
Click "Save"
```

#### Variable 2: JWT_SECRET
```
Key: JWT_SECRET
Value: [paste your random secret - use https://randomkeygen.com]
Environments: ✓ Production ✓ Preview ✓ Development
Click "Save"
```

#### Variable 3: SKIP_SEED_ON_START
```
Key: SKIP_SEED_ON_START
Value: true
Environments: ✓ Production ✓ Preview ✓ Development
Click "Save"
```

### 6. Redeploy
- After adding variables, Vercel will ask to redeploy
- Click **"Redeploy"** button

### 7. Wait & Test
- Wait 1-2 minutes for deployment
- Test: Visit `https://your-project.vercel.app/api/products`

---

## ❓ Don't Have MongoDB Atlas?

1. Go to https://www.mongodb.com/cloud/atlas/register
2. Create free account
3. Create a free cluster (M0 - Free tier)
4. Create database user (username + password)
5. Add IP whitelist: `0.0.0.0/0` (allows all IPs)
6. Get connection string (Connect → Connect your application)
7. Use it in Vercel as `MONGO_URI`

---

## ❓ Don't Have JWT_SECRET?

Use this online generator:
https://randomkeygen.com/

Copy any "CodeIgniter Encryption Keys" value - it's long enough.

---

## ✅ That's It!

Once you add these 3 variables and redeploy, your app will work!

Optional: Add Pinecone variables later for AI recommendations (not required for basic functionality).

