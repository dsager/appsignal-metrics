# session_creation_count

Count whenever a new session is created (i.e. a user logs in).

## record

```ruby
Appsignal.increment_counter('session_creation_count', 1)
```

## visualize

```yml
-
  title: "Newly created sessions"
  kind: "count"
  format: "throughput"
  fields:
    - session_creation_count
```
