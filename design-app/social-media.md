#social media app

Ask clarifying questions
-
    Is the interviewer looking for a design of the core features, or a high-level overview of the whole service?
    What are the constraints of the system?
    What are your assumptions? (traffic distribution, number of active users and tweets, read vs write-heavy)

Design high-level
-
    Back-of-the-envelope calculations: average KBs per tweet, size of new tweet content per month, read requests and tweets per second, etc.
    High-level components: write, read, and search APIs; types of databases; SQL vs NoSQL; etc

Drill down on your design
-
    Potential bottlenecks: adding a load balancer with multiple web servers, scalability issues, fanout service slowing down tweets and @replies, etc.
    Components that you could dive into: how a user views the home timeline or posts a tweet, the intricacies of the database design, etc.

Bring it all together
-
    Consider: does the final design address the bottlenecks you’ve identified? Does it meet the goals you discussed at the beginning of the interview? Do you have any questions for the interviewer?

Tutorial: https://www.youtube.com/watch?v=KmAyPUv9gOY&t=1s
