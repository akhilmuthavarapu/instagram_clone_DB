# instagram_clone_DB
Here is the finalized `README.md` content in proper Markdown format for your **Instagram Clone Database** project:

---

````markdown
# 📸 Instagram Clone Database

This project simulates a simplified backend database of an Instagram-like application. It includes essential tables such as `USERS`, `PHOTOS`, `LIKES`, `TAGS`, and `PHOTO_TAGS`, along with a collection of meaningful SQL queries used to derive insights about users, engagement, and trends.

---

## 🧱 Database Schema

### 🧑 USERS
Stores user information like username and account creation date.

### 🖼️ PHOTOS
Stores uploaded photo URLs with a reference to the user.

### ❤️ LIKES
Tracks which user liked which photo.

### 🏷️ TAGS
Contains all hashtags used.

### 🔗 PHOTO_TAGS
Links photos to their associated hashtags (many-to-many relationship).

---

## 📊 Key SQL Queries & Insights

### 1. 📈 Average User Posts  
**Q:** How many times does the average user post?

```sql
SELECT 
  ROUND(
    (SELECT COUNT(*) FROM PHOTOS) / 
    (SELECT COUNT(*) FROM USERS)
  ) AS AVG_USER_POST;
````

---

### 2. 👴 Top 5 Oldest Users

**Q:** Who are the 5 earliest registered users?

```sql
SELECT * FROM USERS
ORDER BY CREATED_AT
LIMIT 5;
```

---

### 3. 📅 Best Day to Schedule Ad Campaign

**Q:** Which day of the week sees the most user registrations?

```sql
SELECT 
  DAYNAME(CREATED_AT) AS DAYNAME,
  COUNT(*) AS COUNT
FROM USERS
GROUP BY DAYNAME
ORDER BY COUNT DESC
LIMIT 1;
```

---

### 4. 💤 Inactive Users

**Q:** Which users have never uploaded a photo?

```sql
SELECT USERS.USERNAME
FROM USERS
LEFT JOIN PHOTOS ON USERS.ID = PHOTOS.USER_ID
WHERE PHOTOS.IMAGE_URL IS NULL;
```

---

### 5. 🏆 Most Liked Photo Contest

**Q:** Who received the most likes on a single photo?

```sql
SELECT USERS.USERNAME, PHOTOS.IMAGE_URL, COUNT(*) AS LIKE_COUNT
FROM PHOTOS
JOIN LIKES ON PHOTOS.ID = LIKES.PHOTO_ID
JOIN USERS ON USERS.ID = PHOTOS.USER_ID
GROUP BY PHOTOS.ID
ORDER BY LIKE_COUNT DESC
LIMIT 1;
```

---

### 6. 🔥 Top 5 Most Used Hashtags

**Q:** What are the top 5 most frequently used hashtags?

```sql
SELECT TAG_ID, TAG_NAME, COUNT(*) AS USAGE_COUNT 
FROM PHOTO_TAGS 
JOIN TAGS ON TAGS.ID = TAG_ID 
GROUP BY TAG_ID 
ORDER BY USAGE_COUNT DESC 
LIMIT 5;
```

---

### 7. 🤖 Bot Detection

**Q:** How many users have liked every photo in the system?

```sql
-- Count of total photos
SELECT COUNT(*) FROM PHOTOS;

-- Users who liked every photo
SELECT USER_ID
FROM LIKES
GROUP BY USER_ID
HAVING COUNT(*) = (SELECT COUNT(*) FROM PHOTOS);
```

---


---

## 🚀 Getting Started

1. Clone or download the SQL file.
2. Import into your preferred SQL environment (e.g., MySQL Workbench, PostgreSQL, etc.).
3. Run the queries to gain insights and extend the database as needed.

---

## 📜 License

This project is built for learning and demonstration purposes. Feel free to fork and extend it as needed.

```

---

You can save this content directly in a `README.md` file in your project repository. Let me know if you want a sample ER diagram or SQL dump structure added!
```
