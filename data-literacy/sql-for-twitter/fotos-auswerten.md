# Extract Profile Images

## 💡 Profilbilder extrahieren

```sql
create or replace view twitter_profile_images as
select screen_name, profile_image from 
(
  select screen_name
        -- Entfernen des _normal Zusatzes, um größeres Bild zu bekommen
        ,regexp_replace(profile_image_url_https, '_normal', '') as profile_image
        ,rank() over (partition by screen_name order by retrieved_time desc) as `rank`
  from users
  where screen_name in (select distinct follower_of from twitter_followers)
) 
-- Jeweils nur den aktuellsten Datensatz pro Account
where rank = 1
```



