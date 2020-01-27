https://levelup.gitconnected.com/ultimate-guide-to-blazing-fast-performance-in-rails-1-77e281a1df52

## ActiveRecord

```ruby
# Enable slow query logs in Rails
ActiveRecord::Base.logger = Logger.new(STDOUT)
```

```ruby
# Get rails to show you the sql that will run
User.where(id: 1).to_sql
=> "SELECT \"users\".* FROM \"users\" WHERE \"users\".\"id\" = 1"
```

```ruby
# Get rails to explain the sql query for more detail
User.where(id: 1).explain
```

```ruby
# The explain will tell you which index is being used, and what work happens in the back.
=> EXPLAIN for: SELECT "users".* FROM "users" WHERE "users"."id" = $1 [["id", 1]]
                                QUERY PLAN
--------------------------------------------------------------------------
 Index Scan using users_pkey on users  (cost=0.14..8.16 rows=1 width=962)
   Index Cond: (id = '1'::bigint)
(2 rows)
```

## Cache

```ruby
# Lets say you have some categories you offer in your project.
Rails.cache.fetch("categories", expires_in: 5.minutes) do 
   Categories.all.map(&:name)
end
```

## Gems

[Fast JSON API by Netflix](https://github.com/Netflix/fast_jsonapi) - Serializer
