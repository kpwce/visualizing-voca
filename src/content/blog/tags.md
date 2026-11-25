---
title: 'Tags essay draft'
description: 'Draft'
---
# Tumultuous Tags

The readings in Voca are each associated with one or more tags. Some of the readings have tags associated with individual poems, while others only have tags associated with the reading as a whole. This disparity is a result of inconsistent grant funding for the Poetry Center’s digitization projects.

The tags themselves consist of thousands of unique words and phrases which are associated with the recordings. We scraped these from the site and put them into Google Sheets to enable our data exploration. Looking at the thousands of words in our spreadsheet, we felt both overwhelmed in anticipation of trying to coax meaning from so much data and excited by the actual language in the list. Voca is an archive of poetry, and many of the tags reflect that subject matter with terms like ‘[inside/outside worlds](https://voca.arizona.edu/items-with-tag/5965/5965),’ ‘[ultratranslation](https://voca.arizona.edu/items-with-tag/4835/4835),’ ‘[non-existence](https://voca.arizona.edu/items-with-tag/6409/6409)’ and many others that seem to reflect a taggers’ response to the reading more than any sort of search optimization.

## Why explore digital tags?

The data from institutional digital archives such as Voca may surprise users with its evidence of human creation. Despite a clean, alphabetized digital interface, the tags contain language that resists standardization and that reflects individual experiences with the recordings. For example, the tags ‘surreal’ and ‘surrealism’ both appear. An automated tagger would likely have collapsed these into one term. The existence of both serves as evidence of the multiple taggers who made slightly different associations with similar content.

This lack of standardization is an issue that is frequently present in digital collections and digital archives today. As early as 2009, in their foundational textbook, Arlene G. Taylor and Daniel N. Joudrey were discussing in which digital environments it is most appropriate to use a controlled vocabulary, noting that "people do not think of the same terms to express the same aboutness concepts." (333) Taylor and Joudrey discuss the benefits and drawbacks of using controlled vocabularies compared to social tagging practices. A controlled vocabulary is more likely to result in a concise, manageable list of subject terms, while social tagging practices are more likely to capture nuances and inter-community understandings that controlled vocabularies might miss.

Voca's archive, however, is an excellent example of a digital archive which has been processed and tagged solely by library staff members and still contains broad variation in tags. Both the variations of actual words used and the type of data that seems to have been prioritized in the tags varies between readings. The poetry center has been building Voca for x years; this sort of variation reflects the changes in staff, workflows, and understandings of digital data over time.

This kind of messy data is common in digital archives today, but it may soon be seen as a product of its time. As AI tools become more routinely used in library work, the future of digital tagging practices like Vocas's grow even more uncertain.

Standardized digital tagging systems offer many benefits to digital archives. They create data that is more user-friendly, more search-engine friendly, and likely in smaller amounts. The purpose of this essay is not to argue for the creation and use of purposefully messy data. Instead, we are curious to discover the narratives contained in this kind of jointly created metadata.

## Sorting tags manually and automatically --> Parts of Speech --> move to metapoetry

Our first engagement with the tags was an attempt to sort them into more manageable categories. This initial approach was a manual one; we came up with a list of ten semantic categories and attempted to align each tag with its category. This process quickly became almost impossible. *examples*.

Next, we used several python scripts to organize the tags into categories. One script created 84 word clusters, another 48. Ultimately, we used the script-generated categories and manually merged them together and sorted any unassigned tags. The more we worked with the tags using this approach, the more the various tensions between human categorization, machine learning processes, messy data, and the messiness of the English language, emerged. We are working with a language that contains many words with multiple meanings, archival material that relies heavily on context and interpretation, and data that has been created by multiple people across several decades. We are interested in categorizing the tags in order to better investigate the narratives contained in the dataset, but we do not believe our tags should be considered in any way authoritative.

## Sorting by Parts of Speech 

We also experimented with an automated process to organized the tags by parts of speech. The automated tagger broke phrases into several words so that terms like "sixth grade" were tagged 'noun' *and* 'adjective.'

Nouns are the most common part of speech in the dataset by far, with 2,405 words and phrases tagged. The automated tagger also looked for interjections, auxiliary verbs, adpositional phrases, determiners, subordinating conjunctions, coordinating conjunctions, X (voiceless velar fricative??), pronouns, and proper nouns. It was largely excellent at identifying nouns and proper nouns but struggled with adverbs and some of the less common parts of speech such as interjections. For example, the adverb list included very few actual adverbs and included things like 'woolly bear caterpillar,' 'lichen,' and 'cacti.'

The automatically-created tags list was useful to help us understand the data, and was interesting to create poetry with. As we sorted the tags into semantic categories, it was frequently necessary to refer back to the poems the tags were associated with, to make sure we understood the meaning. For example, should 'eve' refer to time of day or the religious figure?

*Discuss which parts of speech were most prevalent, what is interesting about the results.*

- phrases are often tagged noun AND adj
    - e.g. 'ancient greece' 'sixth grade'
- ADV tagger found very few actual adverbs. Interesting to look at what it came back with. Tension between automated processes and messy data/descriptive language.
- every letter of l = a = n = g = u = a = g = e identified as a noun

- adj count: 401 + 24 + 14 + 4 + 1 = 444
- adv count: 13 + 2 + 2 + 1 = 18
- noun count: 1577 + 625 + 146 + 37 + 8 + 2 + 3 + 1 + 1 + 1 + 1 + 1 + 1 + 1 = 2405


## Locations
Many of the poems in the archive reference specific locations which were important to the taggers to note. *Discuss which locations were most/least prevalent, what is interesting about the results. Discuss how location-descriptive words that aren’t included in the locations list relate to the locations.*

## Proper Nouns

The metadata contains a range of specific references, from mythologies to popular culture to literary and historical figures. *Discuss if any one reference or type of reference shows up most often. Should we organize by year? Maybe a chart?*

## Conclusion

*Discuss findings of visualizations, re-engage with the importance of the data.*