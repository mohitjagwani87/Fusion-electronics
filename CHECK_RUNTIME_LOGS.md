# How to Check Runtime Logs for Database Errors

## Build vs Runtime

- **Build logs** (what you just checked): ✅ Shows if code compiled successfully
- **Runtime logs** (what you need now): Shows if MongoDB connection works when function runs

---

## Step 1: Check Runtime/Function Logs

1. Go to Vercel Dashboard → Your Project
2. Click **"Deployments"** tab
3. Click on the **latest deployment** (the one that just completed)
4. Look for tabs: **"Functions"** or **"Runtime Logs"** or **"Logs"**
5. Click on that tab
6. Look for errors - they'll show MongoDB connection errors

**OR**

1. Go to your deployed URL: `https://your-project.vercel.app/api/products`
2. Go back to Vercel → Deployments → Latest → Functions/Runtime Logs
3. You should see the error from when the request tried to connect

---

## Step 2: Verify Connection String is Updated

1. Go to Vercel → Your Project → **Settings** → **Environment Variables**
2. Find `MONGO_URI`
3. Click to view/edit it
4. Verify it looks exactly like this:
   ```
   mongodb+srv://admin:201867mjmjMJ@cluster0.8rbr3rw.mongodb.net/Ecommerce-Products?retryWrites=true&w=majority
   ```

**Check:**
- ✅ No `<` or `>` brackets
- ✅ Password is `201867mjmjMJ` (no brackets)
- ✅ Has `/Ecommerce-Products` before the `?`
- ✅ Has `?retryWrites=true&w=majority` at the end

---

## Step 3: Common Runtime Errors

### Error 1: "Authentication failed"
**Cause:** Wrong username or password  
**Fix:** Verify username is `admin` and password is exactly `201867mjmjMJ`

### Error 2: "IP not whitelisted" or "ENOTFOUND"
**Cause:** MongoDB Atlas Network Access not configured  
**Fix:** Go to MongoDB Atlas → Security → Network Access → Add `0.0.0.0/0`

### Error 3: "Database not found" or "Collection not found"
**Cause:** Database doesn't exist (this is okay, MongoDB creates it automatically)  
**Fix:** This is normal - database will be created on first use

### Error 4: "Connection timeout"
**Cause:** Network issue or IP whitelist  
**Fix:** Check MongoDB Atlas Network Access has `0.0.0.0/0`

---

## Step 4: Test the API

After checking logs:

1. Visit: `https://your-project.vercel.app/api/products`
2. You should see either:
   - ✅ JSON response: `[]` (empty array - means connected but no products)
   - ✅ JSON response with products (if database has data)
   - ❌ Error message (check the exact error)

---

## Quick Checklist

- [ ] Build completed successfully (✅ you already did this)
- [ ] Connection string updated in Vercel (check Settings → Environment Variables)
- [ ] Connection string has correct format (no brackets, has database name)
- [ ] MongoDB Atlas Network Access has `0.0.0.0/0`
- [ ] Checked Runtime/Function logs for exact error message
- [ ] Tested API endpoint: `https://your-project.vercel.app/api/products`

---

**Next:** Check the Runtime/Function logs and share the exact error message you see!

