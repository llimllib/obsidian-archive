---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/hollance/neural-engine

> When I was still providing ML consulting services for iOS, I would often get email from people who are confused why their model doesn't appear to be running on the Neural Engine, or **why it is so slow** when the ANE is supposed to be way faster than the GPU...

> It turns out that **not every Core ML model can make full use of the ANE**. The reason why can be complicated, hence this document tries to answer the most common questions.

> The ANE is great for making ML models run really fast on iPhones and iPads. A model that is optimized for the ANE will seriously outperform the CPU and GPU. But the ANE also has limitations. Unfortunately **Apple isn't giving third-party developers any guidance** on how to optimize their models to take advantage of the ANE. It's mostly a process of trial-and-error to figure out what works and what doesn't.