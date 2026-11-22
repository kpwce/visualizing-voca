---
title: 'Alysa''s Metapoetry'
description: 'Alysa attempted to write a poem.'
---

## Poetry's Uncomputability
Written by Alysa Meng[^1]

I scraped the Voca collection one evening.  
An audiovisual allure brimming with tantalizing findings.  
*Jackpot!* I thought that night.  
*What a perfect dataset to glean insight!*

Promised metadata paradises to decrypt,  
Using a ten-minute programming script,[^2]  
thousands of college poetry readings,  
Machine-readable text for statistical processing.

But then a typo—"san fransisco."[^3]  
A link clicked—missing captions and audio.[^4]  
Cambodia's krama, intangible cultural heritage of a nation,  
becomes Mexico's crema, due to transcription automation.[^5]

Classifications and visualizations  
reimagine search and computation.  
Should we lower cognitive load  
by transforming metaphors into binary code?[^6]

When static labels reduce a dynamic space,  
What identities do we erase?  
Whose voices remain unheard?  
Who really interprets these precious words?[^7]

It's not a question of time complexity.  
The archive resists computability  
After all, computers cannot quantify our humanity.

## Notes
[^1]: This poem reflects on Alysa's experience working on this project. Note that Alysa has a degree in computer science, not in poetry.
[^2]: The web scraping script to download the metadata for our site takes around 7 minutes to run on Google Colab.
[^3]: There are tags for both "San Fransisco" and "San Francisco". The latter is the correct spelling. Maryelizabeth spent some time clustering these in OpenRefine.
[^4]: This refers to the 30 minutes I spent trying to figure out where the .mov file was for Eavan Boland's reading. See "Adventures in Web Scraping" for more details.
[^5]: In Monika Sok's 2020 reading of "Tuol Sleng," "[krama](https://ich.unesco.org/en/RL/cultural-practices-and-expressions-linked-to-krama-a-traditional-woven-textile-in-cambodia-02115)" is transcribed as "[crema](https://en.wikipedia.org/wiki/Crema_(dairy_product))" in the captions. Transcription in Voca is done by a 3rd-party vendor and then reviewed by the Poetry Center. It is a difficult task for automated speech recognition due to the many multilingual readings in Voca and the fact that poetry often breaks standard writing conventions.
[^6]: Poetic search systems are difficult to design because of the subjective interpretation of poems that can change over time.
[^7]: This primarily refers to complexity of the tags. A poet may intend for a reading to mean one thing. The Poetry Center staff interprets it a slightly different way in the tagging process. We applied a k-means clustering algorithm to develop a typology for the 3,000+ reading tags, which potentially influences how we classified the tags and how our audience views them! This note also applies to our word cloud on the main page, which attempts to classify tracks. Karen Brennan, in her 2005 Voca reading of "The Garden in Which I Walk", sums up this dilemma: "I guess I should say that this book is called fictions by the publisher, Fiction Collective, but, actually, these little pieces are all hybrids of some sort or another... I actually argued with some people about whether this was a prose poem or not. I actually think of it as fiction. But this whole book has things that are kind of uncategorizable, I guess. I guess that's a good thing, but, you know, some may think not."