# n8n Lead Generation & Deduplication System

## 🚀 Overview
This project is a production-ready lead generation automation built with n8n. It scrapes business data, cleans it, and stores only unique leads in Google Sheets.

---

## 🧠 Problem
Most scraping workflows create duplicate entries when re-run, leading to messy datasets and inefficient outreach.

---

## ⚙️ Solution
This system:
- Fetches existing records
- Normalizes lead names
- Uses Set-based deduplication
- Appends only new leads

---

## 🏗️ Architecture
Google Places API  
→ Data Cleaning (Code Node)  
→ Fetch Existing Sheet Data  
→ Deduplication (Set Logic)  
→ Append New Leads  
→ Google Sheets  

---

## 🔑 Key Logic (Deduplication)

```js
const existing = new Set(
  existingRows.map(r => r.name.trim().toLowerCase())
);

return newItems.filter(item => {
  const name = item.json.name.trim().toLowerCase();
  if (existing.has(name)) return false;
  existing.add(name);
  return true;
});
