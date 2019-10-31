---
layout: post
title:      "Barely scraping by……"
date:       2019-10-31 15:11:09 +0000
permalink:  barely_scraping_by
---



For our first project,  I decided to use Disney's Vacation Club site as the website to scrape.  Disney is a huge media company that probably spends a lot of resources on their online presence.  Judging by how they cater to the guest experience in their theme parks, hotels and cruises, I naively assumed their website would be perfect.

I looked at their Vacation Club Destinations website and it looked very well structured. Scraping the main page was initially challenging, but through trial and error, the help of online tutorials and mainly the help of our ever supportive and awesome cohort lead, I learned what to look for.

Next, I worked on extracting the address and phone number for each resort.  I inspected the first few resorts on the list and coded my program based on the format they followed.

With great anticipation, I ran my program.  The program showed me a list of resorts, allowed me to choose one to get more details.  I decided to choose the first on the list.  "AH! Victory!", I thought........ until I got a quarter of the way down the list.  This resort page was not structured the same way as the others before it. The previous pages all had specific tags for street, city, state/region. But on this page, the street address, city, state were all in one paragraph. "Ugh!", I thought.
As my program scraped the rest of the pages, I found more than half of the resort pages did not follow the format that I thought I had all figured out.  I inspected each page and found a second loosely structured format that many of the others followed.  I added code to handle the new format (which initially broke the code handling the previous pages) and still found a couple of "rogue" pages that did not follow either format.

I wanted to parse out individual address elements, but unfortunately, the international addresses did not follow the same pattern.  In fact, there were two resorts in France, each listing the city/postal code in a different order. So, I decided to just store all those data elements in one object attribute.

When I decided to extract the description from the resort details pages, I found a couple of anomalies.  I had to change the way I extract the data to ensure that I was not getting extraneous information.

My lessons learned:

1.  It is important to follow industry/company/application standards.  This makes it easier for anyone interacting with or maintaining your code/page.
2.  There is value to storing distinct data elements in their own "container".  I would have liked my program to be able to query the list by city.  But given the lack of standardization, that was difficult to do.
3.  Expect imperfection.  As a developer, we have to protect for the unexpect/non-standard case.



