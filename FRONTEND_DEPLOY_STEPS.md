# Frontend Deploy Karne Ka Complete Guide

## Step-by-Step Instructions

### Step 1: Vercel Dashboard Open Karo

1. Go to: https://vercel.com/dashboard
2. Login karo (agar nahi kiya)

### Step 2: New Project Banao

1. Top right corner pe **"+ Add New"** button click karo
2. **"Project"** select karo

### Step 3: GitHub Repo Import Karo

1. **"Import Git Repository"** section mein
2. Aapka repo dikhna chahiye: `mohitjagwani87/Ecommerce-Online-Store`
3. **"Import"** button click karo

### Step 4: Project Configuration

Agar Vercel automatically detect nahi kare, manually set karo:

1. **Project Name:**
   - Kuch bhi naam: `ecommerce-frontend` ya `fusion-website` ya `ecommerce-app`
   - (Jo bhi aapko pasand ho)

2. **Framework Preset:**
   - Auto-detect: **"Create React App"** 
   - Agar nahi, manually select: **"Create React App"**

3. **Root Directory:**
   - **Leave EMPTY** (root directory use karega)
   - Ya manually type: `.` (dot)

4. **Build Command:**
   - Set: `npm run build`
   - (Default ho sakta hai)

5. **Output Directory:**
   - Set: `build`
   - (Default ho sakta hai)

6. **Install Command:**
   - Set: `npm install`
   - (Default ho sakta hai)

### Step 5: Environment Variables (IMPORTANT!)

**Yeh step zaruri hai backend se connect karne ke liye:**

1. **"Environment Variables"** section expand karo
2. Click **"Add"** ya **"+ Add"**
3. Enter:
   - **Key:** `REACT_APP_API_BASE_URL`
   - **Value:** `https://ecommerce-online-store-backend-1wg9sg0mu.vercel.app`
     - (Yeh aapka backend URL hai - check karo agar different hai)
   - **Environments:** ☑ Production ☑ Preview ☑ Development
     - (Saare checkboxes tick karo)
4. **Save** karo

### Step 6: Deploy!

1. Scroll down karo
2. **"Deploy"** button click karo
3. Wait 2-3 minutes
4. Deployment complete hone ke baad aapko URL milega:
   - Example: `https://ecommerce-frontend.vercel.app`

### Step 7: Test Karo

1. Frontend URL open karo
2. Home page load hona chahiye
3. Products dikhne chahiye (agar backend connected hai aur MongoDB working hai)

---

## Common Issues & Fixes

### Issue 1: Build Fail
**Fix:** Check build logs, agar error aaye toh batao

### Issue 2: Products Nahi Dikhte
**Fix:** 
- Environment variable check karo (`REACT_APP_API_BASE_URL`)
- Backend URL correct hai ya nahi
- Backend MongoDB connection check karo

### Issue 3: CORS Error
**Fix:** Backend mein CORS already enabled hai, toh issue nahi aana chahiye

---

## Quick Checklist

Before deploying:
- [ ] GitHub repo ready hai
- [ ] Backend URL mil gaya (`ecommerce-online-store-backend-xxx.vercel.app`)

During deployment:
- [ ] Framework: Create React App
- [ ] Build Command: `npm run build`
- [ ] Output: `build`
- [ ] Environment Variable: `REACT_APP_API_BASE_URL` with backend URL

After deployment:
- [ ] Frontend URL open karo
- [ ] Home page load hua
- [ ] Navigation kaam kar raha hai

---

**Ready? Chalo deploy karte hain!** 🚀

