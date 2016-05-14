# appsignal-metrics

Collection of potentially interesting examples of [AppSignal](/appsignal/appsignal)
[custom metrics](http://docs.appsignal.com/getting-started/custom-metrics.html).

## Examples

An example represents an interesting metric from a typical web application.
For each example there's a:

- brief description of the metric and motivation,
- code snippet of the measurement within your application (ruby),
- code snippet of the visualization via dashboard graph (yml),
- screenshot(s) of the visualization.

Ideally.

### session_creation_count

Count whenever a new session is created (i.e. a user logs in).

#### measurement

```ruby
Appsignal.increment_counter('session_creation_count', 1)
```

#### visualization

```yml
-
  title: "Newly created sessions"
  kind: "count"
  format: "throughput"
  fields:
    - session_creation_count
```

### backend_api_call

Record the execution time of each back-end API call.

#### measurement

```ruby
time = Benchmark.ms { MyAPI.call(params) }
Appsignal.add_distribution_value('back_end_api_call', time)
```

#### visualization

- [Screenshot (Time)](screenshots/backend_api_call_time.png)
- [Screenshot (Throughput)](screenshots/backend_api_call_throughput.png)

```yml
-
  title: 'API call time'
  kind: measurement
  format: duration
  fields:
    - back_end_api_call
-
  title: 'API call throughput'
  kind: measurement
  format: throughput
  fields:
    - back_end_api_call_count
```

### backend_api_error

Count API errors by type (i.e. HTTP response code).

#### measurement

```ruby
unless response.success?
  Appsignal.increment_counter("backend_api_error_#{response.code}", 1)
end
```

#### visualization

- [Screenshot (Time)](screenshots/backend_api_error.png)

``` yml
-
  title: 'API errors'
  kind: count
  filter: 'backend_api_error_[0-9]+'
  format: number
```

## Contribute

- fork this repo,
- add your example in one single commit,
- open a pull request
- thanks!

## LICENSE

[MIT](LICENSE)
