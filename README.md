# Worker Pool
The worker pool distributes work across the workers to the least loaded worker.

## Demo
The pool was tested by a load generator that produces tasks at a inconsistent interval, faster than the time it takes to complete the tasks itself. 
The tasks also take an inconsistent amount of time to finish.
In this example the tasks were just sleeps.

The gif below shows values for:
- `Workers`: Pending requests for worker
- `Avg Load`: Average pending requests for worker pool
- `Std Dev`: Standard deviation of pending requests

![gif](.github/lb.gif)

## Design
![diagram](.github/lb.png)

*The design was based off the talk [concurrency is not parallelism](https://www.youtube.com/watch?v=cN_DpYBzKso) by Rob Pike, the diagram is also from there*

1. Requests are made by a requester
1. The Balancer dispatch's requests to a select worker in the worker pool
1. The Worker will execute the task specified by the request 
