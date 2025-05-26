## 1. What is PostgreSQL?

PostgreSQL হলো একটা ওপেন সোর্স রিলেশনাল ডাটাবেইজ ম্যানেজমেন্ট সিস্টেম (RDBMS)। একে অনেকেই "Postgres" নামেও চেনে। এটা দিয়ে আমরা অনেক সুন্দরভাবে টেবিল বানাতে পারি, ডেটা রাখতে পারি, আবার সেই ডেটা থেকে প্রয়োজন অনুযায়ী query চালিয়ে ডেটা খুঁজেও বের করতে পারি। ছোট থেকে বড় সব প্রজেক্টেই এটা ব্যবহার করা হয় — কারণ এটা ফ্রি, দ্রুত কাজ করে, আর খুবই শক্তিশালী!

---

## 2. Explain the Primary Key and Foreign Key concepts in PostgreSQL.

**Primary Key** হলো টেবিলের একটা কলাম (বা একাধিক কলাম) যেটা প্রতিটা row কে unique ভাবে চিনিয়ে দেয়। যেমনঃ `ranger_id` – এইটা যদি প্রাইমারি কী হয়, তাহলে কেউ একই আইডি দিয়ে দুইবার এন্ট্রি দিতে পারবে না। এটাতে NULL ও রাখা যাবে না।

**Foreign Key** হলো এমন একটা কলাম যেটা অন্য টেবিলের প্রাইমারি কি কে নির্দেশ করে। এটা দুটি টেবিলের মাঝে সম্পর্ক (relation) তৈরি করে। যেমন `sightings` টেবিলে `ranger_id` থাকবে, যেটা `rangers` টেবিলের `ranger_id` কে নির্দেশ করে। এইভাবে আমরা বুঝতে পারি কোন সাইটিংটা কোন রেঞ্জার করেছে।

---

## 3. What is the difference between the VARCHAR and CHAR data types?

এই দুইটাই টেক্সট রাখার জন্য ব্যবহার করা হয়, কিন্তু -

- `VARCHAR(n)` মানে, যত খুশি লেখা যাবে এর মধ্যে, কিন্তু ম্যাক্সিমাম `n` ক্যারেক্টার পর্যন্ত।
- `CHAR(n)` মানে, যত ছোটই লেখা হোক না কেনো, জায়গা `n` ক্যারেক্টারের মতোই নেবে। বাকি জায়গা ফাঁকা থাকবে।

`VARCHAR` বেশ flexible, আর `CHAR` এর রয়েছে fixed length।

---

## 4. Explain the purpose of the WHERE clause in a SELECT statement.

`WHERE` clause ব্যবহার করা হয় ফিল্টার করার জন্য। মানে আমি শুধু ওই ডাটাগুলাই দেখতে চাই যেগুলা আমার শর্ত (condition) পূরণ করে।

যেমনঃ

```sql
SELECT * FROM sightings WHERE location = 'Snowfall Pass';
```

এইখানে আমরা শুধু ওইসব সাইটিংস দেখবো যেগুলার লোকেশন 'Snowfall Pass'।

---

## 5. What is the significance of the JOIN operation, and how does it work in PostgreSQL?

JOIN ব্যবহার করে আমরা একাধিক টেবিল থেকে ডাটা একসাথে নিতে পারি। যেমনঃ একটি টেবিলে রেঞ্জারের নাম আছে, আরেকটায় সাইটিংস — এখন যদি কেউ জানতে চায় কে কোন প্রাণী কোথায় দেখেছে, তখন দুইটা টেবিল JOIN করতে হবে।

PostgreSQL এ সবচেয়ে কমন INNER JOIN যেখানে শুধু সেইসব রো আসবে যেগুলার দুইটা টেবিলেই ম্যাচিং ডাটা আছে।

উদাহরণঃ

```sql
SELECT r.name, s.location
FROM rangers r
JOIN sightings s ON r.ranger_id = s.ranger_id;
```

এই query-র আউটপুটে rangers টেবিলের নাম আর sightings টেবিলের লোকেশন একসাথে দেখা যাবে।
