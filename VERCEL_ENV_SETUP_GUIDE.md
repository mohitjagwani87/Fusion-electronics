# Step-by-Step Guide: Setting Environment Variables in Vercel

## Why Environment Variables Matter

Without environment variables, your app **will not work**. The backend needs:
- Database connection (MongoDB)
- Secret keys for authentication
- API keys for features (optional)

---

## 📋 Step-by-Step Instructions

### Step 1: Go to Your Vercel Project

1. Go to https://vercel.com/dashboard
2. Click on your project (likely called something like "fusion-electronics-api" or "ecommerce-backend")

### Step 2: Open Environment Variables Settings

1. Click on **"Settings"** tab (at the top of the project page)
2. Click on **"Environment Variables"** (in the left sidebar)

You'll see a page that looks like this:
```
┌─────────────────────────────────────────┐
│ Environment Variables                   │
├─────────────────────────────────────────┤
│ [Key]          [Value]    [Environment] │
│                                          │
│ [+ Add New]                              │
└─────────────────────────────────────────┘
```

### Step 3: Add Required Variables

Click **"+ Add New"** for each variable below:

---

## 🔴 REQUIRED Variables (Add These First!)

### 1. MONGO_URI (MongoDB Connection String)

**Key:** `MONGO_URI`  
**Value:** Your MongoDB connection string

**How to get it:**
- If you have MongoDB Atlas:
  1. Go to https://cloud.mongodb.com
  2. Click on your cluster
  3. Click "Connect" → "Connect your application"
  4. Copy the connection string
  5. Replace `<password>` with your actual password
  6. Example: `mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/Ecommerce-Products?retryWrites=true&w=majority`

- If you're using local MongoDB (not recommended for Vercel):
  - You'll need to use MongoDB Atlas instead (Vercel can't connect to localhost)

**Environment:** Select **ALL THREE**:
- ✅ Production
- ✅ Preview  
- ✅ Development

---

### 2. JWT_SECRET (Authentication Secret)

**Key:** `JWT_SECRET`  
**Value:** A random secret string (at least 32 characters)

**How to generate:**
- Option 1: Use online generator: https://randomkeygen.com/ (use "CodeIgniter Encryption Keys")
- Option 2: Run in terminal: `openssl rand -base64 32`
- Option 3: Just type any long random string like: `mySuperSecretKeyForJWT1234567890abcdefghijklmnop`

**Example:** `K7gNU3sdo+OL0wNhqoVWhr3g6s1xYv72ol/pe/Unols=`

**Environment:** Select **ALL THREE**:
- ✅ Production
- ✅ Preview
- ✅ Development

---

### 3. SKIP_SEED_ON_START (Critical for Serverless!)

**Key:** `SKIP_SEED_ON_START`  
**Value:** `true`

**Why this is important:**
- Prevents database seeding during serverless function startup
- **Without this, your function will timeout!**

**Environment:** Select **ALL THREE**:
- ✅ Production
- ✅ Preview
- ✅ Development

---

## 🟡 OPTIONAL Variables (For AI Recommendations)

These are only needed if you want AI-powered product recommendations:

### 4. PINECONE_API_KEY
- Get from: https://app.pinecone.io/
- Create account → API Keys section
- Copy your API key

### 5. PINECONE_HOST
- Get from: https://app.pinecone.io/
- In your index dashboard, copy the "Host" URL
- Example: `https://your-index-xxxxx.svc.us-east-1-aws.pinecone.io`

### 6. GOOGLE_AI_API_KEY
- Get from: https://makersuite.google.com/app/apikey
- Create a new API key
- Copy the key

### 7. PINECONE_INDEX (Optional)
- **Key:** `PINECONE_INDEX`
- **Value:** `ecommerce-products` (or your index name)

---

## 📝 Quick Reference: What to Add

### Minimum Setup (App will work, but no AI recommendations):
```
✅ MONGO_URI
✅ JWT_SECRET  
✅ SKIP_SEED_ON_START=true
```

### Full Setup (With AI recommendations):
```
✅ MONGO_URI
✅ JWT_SECRET
✅ SKIP_SEED_ON_START=true
✅ PINECONE_API_KEY
✅ PINECONE_HOST
✅ GOOGLE_AI_API_KEY
✅ PINECONE_INDEX (optional)
```

---

## ⚠️ Important Tips

1. **Case-Sensitive**: Variable names are case-sensitive. Use exact names:
   - ✅ `MONGO_URI` 
   - ❌ `mongo_uri` or `MONGO_URI_` (wrong!)

2. **Select All Environments**: For each variable, select all three checkboxes:
   - Production
   - Preview
   - Development

3. **No Spaces**: Don't add spaces before or after the value

4. **After Adding Variables**: Vercel will ask if you want to redeploy. Click **"Redeploy"** to apply changes.

---

## 🎯 After Adding Variables

1. **Redeploy** your project:
   - Vercel will show a popup asking to redeploy after adding variables
   - Or go to "Deployments" tab → Click "Redeploy" on latest deployment

2. **Test your API**:
   - Visit: `https://your-project.vercel.app/api/products`
   - Should return products (or empty array if no products yet)

3. **Check Logs** if it doesn't work:
   - Go to "Deployments" → Latest → "Functions" tab
   - Look for error messages

---

## 🆘 Troubleshooting

### "MongoDB connection error"
- Check your `MONGO_URI` is correct
- Make sure you replaced `<password>` in the connection string
- In MongoDB Atlas, make sure IP whitelist includes `0.0.0.0/0` (all IPs)

### "FUNCTION_INVOCATION_FAILED" still happening
- Make sure `SKIP_SEED_ON_START=true` is set
- Redeploy after adding the variable

### "JWT_SECRET must be set"
- Add `JWT_SECRET` variable with any long random string

### "Pinecone error" (if using recommendations)
- Check `PINECONE_API_KEY` and `PINECONE_HOST` are correct
- App will still work, just recommendations will use fallback method

---

## 📸 Visual Guide

```
Vercel Dashboard
  └── Your Project
       └── Settings (tab at top)
            └── Environment Variables (left sidebar)
                 └── [+ Add New] button
                      └── Enter Key and Value
                           └── Select Environments (✓ all three)
                                └── Save
                                     └── Redeploy when prompted
```

---

## ✅ Checklist

After you're done, verify:
- [ ] Added `MONGO_URI` (for all 3 environments)
- [ ] Added `JWT_SECRET` (for all 3 environments)  
- [ ] Added `SKIP_SEED_ON_START=true` (for all 3 environments)
- [ ] (Optional) Added Pinecone variables if using recommendations
- [ ] Redeployed the project
- [ ] Tested the API endpoint

---

**You can always add or change these variables later - just go back to Settings → Environment Variables!**

