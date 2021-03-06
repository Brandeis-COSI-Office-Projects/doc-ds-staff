---
weight: 1
bookFlatSection: true
title: "The Project"
---

# An Overview of the Project

## Blueprint

The project is about collecting and analyzing past alumni employment data. We have collected over a thousand lines of data which contains the following information:

    First Name
    Last Name
    Gender
    Class Year
    Majors
    All Past Job Titles
    Years of Service for All Jobs

An example would be:

    First Name: Chuyue
    Last Name: Xiao
    Gender: Female
    Class Year: 2020
    Majors: Computer Science
    All Past Job Titles: [Business Consulting Intern, Software Engineering and Data Analytics Intern ...]
    Years of Service for All Jobs: [2 months, 4 months ...]

After collecting the raw data, we did all sorts of data cleaning to make it easier to read, analyze, and visualize. Steps include: 

- Merging job titles with lower occurrences to similar titles with higher occurrences. E.g., merging "Senior Software Engineer" to "Software Engineer"
- Unifying "years of service" format. Before they are like "1 year 3 months", "3 mo", "2 yrs 1 mo"... and we unified all the time formats to be "xyxm", like "4y7m".
- Sorting job titles based on occurrences. E.g., we have 1347 occurrences of Software Engineer and 296 occurrences of Software Engineering Intern.

We are currently at the visualizing stage where we are finding the best tool to do data visualization. Possible choices are Tableau, Power BI, etc.

## Statistics

    1430
        We have 1430 lines of alumni that we are trying to find

    1045
        We are able to find 1045 alumni on LinkedIn

    73.08%
        73.08% of 1430 alumni have LinkedIn employment information

    2613
        We have 2613 unique job titles

    36
        After processing and merging, we now have 36 job titles to proceed. 

    1403
        The highest occurrences of job title is Software Engineer, 1403 times.
        
    360
        The second highest occurrences of job title is Intern, 360 times.