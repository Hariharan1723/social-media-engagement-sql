# 📊 Social Media User Engagement Analytics (SQL Project)

> A normalized MySQL database project that models an Instagram-like platform — analyzing user behavior, content performance, engagement trends, and network relationships using structured SQL queries.

---

## 🧠 Project Overview

This project simulates a social media platform where users upload photos, give likes, post comments, follow each other, and tag content with hashtags.

The goal was to:
- Design a **normalized relational database** (3NF)
- Perform **ETL** by importing CSV datasets into MySQL
- Write **25+ analytical SQL queries** to extract real business insights
- Identify **bot accounts**, **inactive users**, and **top performers**

---

## ⚙️ Tools & Technologies

| Category | Details |
|---|---|
| **Database** | MySQL 8.x |
| **Environment** | MySQL Workbench |
| **Data Source** | CSV Files |
| **ETL Method** | `LOAD DATA LOCAL INFILE` |
| **Query Types** | DDL, DML, DQL, JOINs, Aggregations, Subqueries, CTEs, Views |

---

## 🗂️ Project Structure

```
social-media-engagement-sql/
│
├── database_setup.sql          # Schema creation + CSV data import
├── analytics_queries.sql       # All analytical SQL queries
├── README.md                   # Project documentation
├── database_schema_diagram.png # ER Diagram
│
└── data/
    ├── users.csv
    ├── photos.csv
    ├── likes.csv
    ├── follows.csv
    ├── comments.csv
    ├── tags.csv
    └── photo_tags.csv
```

---

## 🗃️ Database Schema

The database `db_silver` contains **7 normalized tables**:

```
users ──< photos ──< likes
  │          │
  │       photo_tags >── tags
  │
  ├──< comments
  └──< follows
```

| Table | Description |
|---|---|
| `users` | User accounts with username and registration timestamp |
| `photos` | Photos uploaded by users |
| `likes` | Which users liked which photos (composite PK) |
| `comments` | Text comments on photos |
| `follows` | Follow relationships between users (composite PK) |
| `tags` | Unique hashtags |
| `photo_tags` | Many-to-many: photos ↔ tags |

---

## 💡 Key Analytical Insights

### 👥 User Insights
- **5 oldest registered users** — for loyalty rewards
- **Most popular registration day** — to schedule ad campaigns
- **Month-wise registration trends** — to track growth

### 📸 Activity & Posting Behavior
- Users who **never posted a photo** (inactive — email campaign targets)
- **Average posts per user** across the platform
- **User ranking** by total number of posts

### ❤️ Engagement Analysis
- Photo that received the **most likes** (contest winner)
- **Top 5 most-used hashtags** (for brand partnerships)
- **Bot detection** — users who liked *every single photo*
- **Celebrity detection** — users who never commented
- **Bot/celebrity percentage** across the platform

### 🌐 Follower Network
- **Top 3 most-followed users**
- Users who **follow more than follow them back**
- Detection of **self-follows** (data quality cleanup)

### 📊 Content Metrics
- Percentage of photos **with at least one like**
- Photos with **zero likes and zero comments**
- Users who **liked their own photos**
- **Comment-to-like ratio** per photo

### ⏱️ Temporal Analysis
- **Total likes per month** in 2017
- **Weekday vs. weekend** posting patterns

### 🏆 Engagement Summary
- Combined metric: posts + likes + comments per user
- **Active user view** (≥10 posts AND ≥50 likes received)
- Average likes each user's photos receive

---

## 🚀 How to Run the Project

### 1. Clone the Repository
```bash
git clone https://github.com/<your-username>/social-media-engagement-sql.git
cd social-media-engagement-sql
```

### 2. Open MySQL Workbench and connect to your local server


### 3. Enable local file import (run once as admin)

Find all `LOAD DATA LOCAL INFILE` lines and replace the path with your local path:
```
-- SET GLOBAL local_infile = 1;

```

### 4. Update file paths in database_setup.sql
```sql
LOAD DATA LOCAL INFILE 'C:/Users/YourName/Downloads/social-media-engagement-sql/Data/users.csv'
```

### 5. Run the setup script
```sql
SOURCE database_setup.sql;
```

### 6. Run analytical queries
```sql
SOURCE analytics_queries.sql;
```

---

## 📋 Sample Query Results

### Most Liked Photo
```sql
SELECT u.username, p.id AS photo_id, COUNT(*) AS total_likes
FROM likes l
JOIN photos p ON p.id = l.photo_id
JOIN users u ON u.id = p.user_id
GROUP BY p.id
ORDER BY total_likes DESC
LIMIT 1;
```

### Top 5 Hashtags
```sql
SELECT tag_name, COUNT(tag_name) AS total
FROM tags
JOIN photo_tags ON tags.id = photo_tags.tag_id
GROUP BY tags.id
ORDER BY total DESC
LIMIT 5;
```

### Bot Detection (users who liked every photo)
```sql
SELECT u.username, COUNT(u.id) AS total_likes
FROM users u
JOIN likes l ON u.id = l.user_id
GROUP BY u.id
HAVING total_likes = (SELECT COUNT(*) FROM photos);
```

---

## 📈 Key Outcomes

- Designed a realistic, **normalized relational database** for engagement tracking
- Performed **ETL and data validation** entirely within MySQL
- Detected **bot and inactive accounts** using behavioral logic
- Derived **actionable business insights** from raw engagement data
- Demonstrated proficiency in **JOINs, subqueries, aggregations, views, and CTEs**

---

## 🧰 Skills Demonstrated

`MySQL` · `Data Modeling` · `ETL` · `DDL / DML / DQL` · `Normalization` · `Joins` · `Subqueries` · `Aggregation` · `Window Functions` · `Views` · `Data Validation`

---

## 👨‍💻 Author

**Hariharan B**
- GitHub: (https://github.com/hariharan1723)
- LinkedIn:(https://www.linkedin.com/in/hariharanbalamurugan)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
