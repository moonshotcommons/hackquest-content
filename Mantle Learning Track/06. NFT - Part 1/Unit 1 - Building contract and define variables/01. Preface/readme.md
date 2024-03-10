# Content/Intro

In this unit, we will do the first two things we need to do for every contract:

1. define the *contract* 
2. define some *variables*

As we mentioned in About This Course, on the course landing page, everything in the digital world is about data, and for any case where we have data, we need to have *variables* in different data *structures* to store these data. 

In our NFT *contract*, we will define three necessary data structures before we do anything:

1. Token - This is a struct we defined to represent the NFT.
2. tokens - this is a mapping we use to manage all the NFTs
3. nextTokenId - a counter to track total NFTs issued, and check the next available TokenId. 

We will explain in each step why we chose this data structure for this piece of information. 