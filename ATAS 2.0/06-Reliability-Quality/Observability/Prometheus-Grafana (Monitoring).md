![[Pasted image 20260125173453.png]]
### 1. Top Graph: P95 Latency (User Experience)
- The Math : histogram_quantile(0.95, ...)
- What it means : This tells you the maximum wait time for 95% of your users .
- In your graph :
  - The line is around 0.01 . This means 95% of your requests are finished in 0.01 seconds (10ms) . That is extremely fast!
  - At the start (around 16:55), it was higher (near 0.1s). This might have been when the app was starting up or handling its first heavy requests.
- Why use P95? : If you use "Average," one very slow request is hidden. P95 ensures that even your "unlucky" users are still getting a fast experience.
### 2. Bottom Graph: Throughput (Traffic Volume)
- The Math : sum(rate(...[1m]))
- What it means : This is the number of requests per second hitting your server.
- In your graph :
  - The value is around 3 . This means your traffic script is hitting the API 3 times every second .
  - The Big Drop : You see the line go to 0 between 17:07 and 17:23. This is exactly when you were editing the code and the server was restarting, or when the traffic script was stopped.
  - The Spike : At 17:25, it jumps back up to 3 because we started the script again.