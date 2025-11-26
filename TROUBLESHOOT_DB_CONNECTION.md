# Troubleshooting "Database connection failed" Error

## Step 1: Check Vercel Logs for Exact Error

1. Go to https://vercel.com/dashboard
2. Click your project
3. Click **"Deployments"** tab
4. Click on the latest deployment
5. Click **"Functions"** tab (or "Runtime Logs")
6. Look for error messages - they'll tell us exactly what's wrong

Common errors you might see:
- `Authentication failed`
- `IP not whitelisted`
- `Invalid connection string`
- `ENOTFOUND` or DNS error
- `Connection timeout`

**Copy the exact error message** - this will help us fix it!

---

## Step 2: Verify Connection String Format

Your connection string should look like one of these:

### Format 1 (mongodb+srv):
```
mongodb+srv://admin:201867%40mjmjMJ@cluster0.xxxxx.mongodb.net/Ecommerce-Products?retryWrites=true&w=majority
```

### Format 2 (regular):
```
mongodb://admin:201867%40mjmjMJ@cluster0.xxxxx.mongodb.net:27017/Ecommerce-Products?ssl=true&authSource=admin
```

**Check:**
- ✅ Username is `admin` (not `<username>`)
- ✅ Password has `%40` instead of `@` (because `@` in password is encoded)
- ✅ Database name `/Ecommerce-Products` is added before the `?`
- ✅ No extra spaces before or after

---

## Step 3: Verify MongoDB Atlas Settings

### A. Check IP Whitelist

1. Go to https://cloud.mongodb.com
2. Click **"Security"** → **"Network Access"**
3. Make sure you have `0.0.0.0/0` (or "Allow Access from Anywhere")
4. If not, add it now and wait 1-2 minutes

### B. Check Database User

1. Go to **"Security"** → **"Database Access"**
2. Make sure user `admin` exists and is active
3. Verify the password is correct: `201867@mjmjMJ`

### C. Test Connection from MongoDB Atlas

1. In MongoDB Atlas, click **"Database"**
2. Click **"Connect"** → **"Connect using MongoDB Compass"** (for testing)
3. Copy that connection string and try connecting
4. If it works, the credentials are correct

---

## Step 4: Password Encoding Issue

Your password is: `201867@mjmjMJ`

**The `@` symbol must be encoded in the connection string:**

| Character | Encoding |
|-----------|----------|
| `@` | `%40` |
| `#` | `%23` |
| `%` | `%25` |

So `201867@mjmjMJ` becomes `201867%40mjmjMJ`

**Common mistake:** Forgetting to encode the `@` symbol!

---

## Step 5: Verify Connection String in Vercel

1. Go to Vercel → Your Project → **Settings** → **Environment Variables**
2. Find `MONGO_URI`
3. Check what value is stored
4. Make sure it matches the correct format above

**⚠️ Common Issues:**
- Value has `<username>` or `<password>` not replaced
- Value has `@` in password instead of `%40`
- Database name missing (no `/Ecommerce-Products`)
- Extra spaces or newlines

---

## Step 6: Test Connection String Locally (Optional)

If you want to test before deploying:

1. Create a test file `test-connection.js`:
```javascript
const mongoose = require('mongoose');

const MONGO_URI = 'YOUR_CONNECTION_STRING_HERE';

mongoose.connect(MONGO_URI)
  .then(() => {
    console.log('✅ Connected!');
    process.exit(0);
  })
  .catch(err => {
    console.error('❌ Error:', err.message);
    process.exit(1);
  });
```

2. Run: `node test-connection.js`

This will show you the exact error locally.

---

## Common Fixes

### Fix 1: Password Encoding
If password has `@`, make sure it's encoded:
```
❌ Wrong: admin:201867@mjmjMJ@...
✅ Right: admin:201867%40mjmjMJ@...
```

### Fix 2: IP Whitelist
Make sure MongoDB Atlas has `0.0.0.0/0` in Network Access

### Fix 3: Database Name
Make sure database name is included:
```
❌ Wrong: ...mongodb.net/?retryWrites...
✅ Right: ...mongodb.net/Ecommerce-Products?retryWrites...
```

### Fix 4: Check All Environments
In Vercel, make sure `MONGO_URI` is set for:
- ✅ Production
- ✅ Preview
- ✅ Development

---

## What to Share With Me

Please share:
1. **The exact error message** from Vercel logs (Functions tab)
2. **Your connection string** (with password hidden, like `admin:****@cluster0.xxx...`)
3. **Confirm IP whitelist** has `0.0.0.0/0`

This will help me give you the exact fix!

