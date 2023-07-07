### 2018 - My first Commercial App

There was **need** to test a Radar Station.
For this, was used a Quadcopter which writes flight logs. 
These logs are written as binary files, so not possible directly open and read.

My **task** was to make desktop app which parses log files and creates human-readable text.
It was not hard in terms of programming, but **challenge** is binary files. 
To parse them, you should know how data is written.
There was no such algorithm for encoding along with the Quadcopter.
Moreover, there was no guarantee that the algorithm exists in the public access. 

What I **did** is I spent more than 1 week looking for the algorithm in the Internet and finally found.
Then, I started actual development. Even though I had no experience with desktop,
I quickly figured it out, and it took me 1 month to implement app from scratch.

As a **result**, research team was able to test Radar Stations using this app as a custom(trusted) solution.