# Your MongoDB Connection String Setup

## ⚠️ Important: You Need the Right Connection String

The connection string you provided:
```
mongodb://atlas-sql-6907a3469d27891c52d2004e-okf37q.a.query.mongodb.net/sample_mflix?ssl=true&authSource=admin
```

This is for **MongoDB SQL API**, but we need the **MongoDB Driver connection string** for Node.js/Express.

---

## ✅ Step 1: Get the Correct Connection String

1. Go to https://cloud.mongodb.com
2. Click on your cluster (in Database view)
3. Click **"Connect"** button
4. Choose **"Connect your application"** (NOT "Connect using MongoDB Shell" or "Connect using MongoDB Compass")
5. You'll see a connection string that looks like:
   ```
   mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/?retryWrites=true&w=majority
   ```
   OR
   ```
   mongodb://username:password@cluster0.xxxxx.mongodb.net:27017/?ssl=true&authSource=admin
   ```

6. **Copy that connection string**

---

## ✅ Step 2: Format It With Your Credentials

You provided:
- **Username:** `admin`
- **Password:** `201867@mjmjMJ`

**IMPORTANT:** Your password has special characters (`@`). In MongoDB connection strings, `@` needs to be URL-encoded as `%40`.

### Here's your formatted connection string:

**Replace the `<username>` and `<password>` in your connection string:**

```
mongodb+srv://admin:201867%40mjmjMJ@cluster0.xxxxx.mongodb.net/Ecommerce-Products?retryWrites=true&w=majority
```

**OR if it's the regular format (not mongodb+srv):**

```
mongodb://admin:201867%40mjmjMJ@cluster0.xxxxx.mongodb.net:27017/Ecommerce-Products?ssl=true&authSource=admin
```

**Notice:**
- Username: `admin`
- Password: `201867@mjmjMJ` → encoded as `201867%40mjmjMJ` (the `@` becomes `%40`)
- Database name: `/Ecommerce-Products` (before the `?`)

---

## ✅ Step 3: Complete Connection String

Since I don't have your exact cluster hostname, here's what you need to do:

1. Get the connection string from "Connect your application" (Step 1 above)
2. Replace `<username>` with: `admin`
3. Replace `<password>` with: `201867%40mjmjMJ` (note the `%40` instead of `@`)
4. Add database name: After `.net` or `.mongodb.net`, add `/Ecommerce-Products`
5. Keep the rest (`?retryWrites=true&w=majority` or `?ssl=true&authSource=admin`)

### Example Final Format:

```
mongodb+srv://admin:201867%40mjmjMJ@cluster0.xxxxx.mongodb.net/Ecommerce-Products?retryWrites=true&w=majority
```

**OR**

```
mongodb://admin:201867%40mjmjMJ@cluster0.xxxxx.mongodb.net:27017/Ecommerce-Products?ssl=true&authSource=admin
```

---

## ✅ Step 4: Add to Vercel

1. Go to https://vercel.com/dashboard
2. Click your project
3. **Settings** → **Environment Variables**
4. Click **"+ Add New"**
5. Enter:
   - **Key:** `MONGO_URI`
   - **Value:** Your formatted connection string (from Step 3)
6. Check all 3 environments: ☑ Production ☑ Preview ☑ Development
7. Click **"Save"**
8. Click **"Redeploy"** when prompted

---

## 🔍 How to Find Your Cluster Hostname

If you're not sure what your connection string should be:

1. In MongoDB Atlas dashboard
2. Click **"Database"** (left sidebar)
3. Click **"Connect"** on your cluster
4. Click **"Connect your application"**
5. Look at the connection string - it will have your cluster hostname like:
   - `cluster0.abc123.mongodb.net`
   - Or something similar
6. Copy the entire connection string format shown

---

## 📝 Quick Reference

**Your credentials:**
- Username: `admin`
- Password: `201867@mjmjMJ`
- Encoded password: `201867%40mjmjMJ`
- Database: `Ecommerce-Products`

**Connection string template:**
```
mongodb+srv://admin:201867%40mjmjMJ@YOUR_CLUSTER_HOST/Ecommerce-Products?retryWrites=true&w=majority
```

Replace `YOUR_CLUSTER_HOST` with your actual cluster hostname from MongoDB Atlas.

---

## ⚠️ Special Note About Password Encoding

Your password `201867@mjmjMJ` contains an `@` symbol.

In connection strings:
- `@` is a special character (separates credentials from hostname)
- So `@` in password must be encoded as `%40`
- `201867@mjmjMJ` → `201867%40mjmjMJ`

**Other special characters that might need encoding:**
- `@` → `%40`
- `#` → `%23`
- `%` → `%25`
- `:` → `%3A` (usually not needed in password)
- `/` → `%2F`

---

## ✅ Checklist

- [ ] Got connection string from "Connect your application" (not SQL API)
- [ ] Replaced `<username>` with `admin`
- [ ] Replaced `<password>` with `201867%40mjmjMJ` (encoded `@`)
- [ ] Added `/Ecommerce-Products` before the `?`
- [ ] Added connection string to Vercel as `MONGO_URI`
- [ ] Selected all 3 environments
- [ ] Redeployed Vercel project
- [ ] Tested API endpoint

---

**Need help?** Just share the connection string you see in "Connect your application" and I'll format it for you!

