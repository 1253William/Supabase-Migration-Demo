# Supabase-Migration-Demo
MongoDB Data API → Supabase Migration Demo  
This is a lightweight demo repo showing how to migrate from MongoDB's Data API (sunsetting Sept 30, 2025) to Supabase with REST API.

## Prerequisites
- MongoDB Atlas
- Supabase account
- Node.js installed

## Steps

1. Export MongoDB data
```bash
mongoexport --uri="<uri>" --collection=users --jsonArray --out=users.json
```

2. Create mongo_users_raw table on Supabase:

```sql
create table mongo_users_raw (
  id uuid primary key default gen_random_uuid(),
  data jsonb not null
);
```

3. Load data with:

```bash
node loadToSupabase.js
```

4. Normalize:
```
insert into users (name, email)
select data->>'name', data->>'email' from mongo_users_raw;
```


