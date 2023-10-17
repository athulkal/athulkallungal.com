+++
title = 'Uk Companies with sponsorship license Analysis'
date = 2023-10-16T02:01:06+01:00
draft = false
categories = ["Python"]
showReadingTime = true
ShowShareButtons = true
+++

### The idea for the project

The idea came into being while I was chekcing out the UK companies which would sponsor an employees by giving them a skilled worker visa. I found the list of companies you can check it out [here](https://www.gov.uk/government/publications/register-of-licensed-sponsors-workers).The one problem I found with this data set was that it had no information on which sector these companies were from. So, if I want to check for a company in a specific industry and if they were hiring it was literally not possible.

### The motive: I needed to find Tech companies that were sponsoring visas

So, I started by searching for ways to get this information. So, I went to this [page](https://find-and-update.company-information.service.gov.uk/) and search the first company and I was able to find something interesting.

![CompanyDetails](/img/companydetails.png)

I found there was a section called Nature of Business which defined what type of business they where doing great exactly what I was looking for. So, now I can write a script using some automation library.

### Selenium, the webscraper

I had used selenium before for funny things like filling out Mcdonald's survey so I could get a free Big mac yeah I know but that was just for fun. But to be honest I don't know of other popular automation libraries. So, I set up selenium to go the website and type each company in the list and then grab the nature of business and use pandas library to add a column and put that info there.

you can check the **CODE** [here](https://github.com/athulkal/pybotUKSPONSORS)

### Limitations/How I overcome that

1. The first limitation was that I ran sample check and found out that some company names were messed up in a way the search returned no results. So, I first cleaned the file in Excel.
2. The second problem was that some of them didn't have the section called Nature of Business so I programmed my bot to send a generic Not Found which I would later clean up in Excel.
3. The third and the most challenging one was rate limiting which was implemented on the website. I had to do a few trial runs as how many requests I can make it seemed like 50 to 100 requests would get my IP address blocked. So I set a timer of 5 secs between each request.This meant that it would take three days to actually get all of the data on there. So I had to cut short to 500 companies just for demonstration purposes.

### Final results

I used to pandas to update the dataset and save it as a new csv file. I did some clean up work in Excel and the data was ready to be visualised. I used Tableau to do this beacause it is a easy to use software. You can check out the detailed visualisation over [here](https://public.tableau.com/app/profile/athul.kallungal/viz/TechcompaniesUKsponsor/TechSponsorChart?publish=yes)

![DataVisualised](/img/Visualisation.png)
