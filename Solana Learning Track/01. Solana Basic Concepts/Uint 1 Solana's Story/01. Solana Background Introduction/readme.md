# Content

Before we start learning to build on Solana, let’s first understand its history.

## **The History of Solana**

In November 2017, ***Anatoly Yakovenko*** published a whitepaper introducing the "***Proof of History***" (which we will delve into in later sections), designed for time synchronization among mutually untrusting computers. With experience in designing distributed systems at Qualcomm, Mesosphere, and Dropbox, Anatoly recognized that reliable clocks could simplify network synchronization, enabling fast network operation constrained only by bandwidth.

Observing that blockchain like Bitcoin and Ethereum, lacking a clock, could achieve only 15 transactions per second, Anatoly envisioned the need for peak transaction speeds of 65,000 transactions per second for a globally decentralized payment system like Visa. Recognizing that resolving the issue of time inconsistency among computers was crucial, Anatoly applied years of distributed systems research to the blockchain domain. His solution not only improved efficiency but also increased speed by orders of magnitude.

Initially, Anatoly implemented the Solana prototype in C language on his Github. Greg Fitzgerald, who had previously collaborated with Anatoly at Qualcomm, encouraged him to rewrite the project in Rust. Within two weeks, Anatoly successfully migrated the project to Rust and named it Loom.

On February 13, 2018, Greg Fitzgerald began creating an open-source prototype for Anatoly's whitepaper. By February 28, Greg released the first version capable of verifying and processing over 10,000 signed transactions in half a second. Shortly after, Stephen Akridge, another former colleague from Qualcomm, demonstrated how to enhance processing speed by using graphics processors for signature verification. Anatoly invited Greg, Stephen, and three others to co-found a company named Loom.

Around the same time, another Ethereum-based project called Loom Network emerged, causing occasional confusion between the two projects. The Loom team decided to give their project a new name. Eventually, they chose to name it Solana in homage to their three years of work and surfing in Solana Beach, Northern San Diego. On March 28, 2018, the team created Solana's GitHub and officially named Greg Fitzgerald's prototype Solana.