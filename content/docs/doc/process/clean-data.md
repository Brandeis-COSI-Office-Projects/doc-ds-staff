---
title: Clean Data
weight: 2
---

# Clean Data for Faster and Easier Readability and Visualization

## Raw Data

The raw data is pretty messy. We have lots of columns that are not useful for this particular project, like `Preferred Email`, `Address`, `Current Company` etc, so we extract only those columns that are essential for later visualization. Useful columns including:

    First Name
    Last Name
    Gender
    Class Year
    Majors
    All Past Job Titles
    Years of Service for All Jobs

Since the original data is in a Google Sheet, we need to download it as `.csv` format. CSV files are separated by delimiter comma`,`. So the raw data looks like:

    firstName,lastName,gender,classYear,majors,job1,job1yearsofservice,job2,job2yearsofservice...

For faster processing, we convert the `csv` format to `json` format. This format is commonly used in programming. It's basically a `key-value` pair. Processed data looks like this:

```json
{
    "firstName": "Chuyue",
    "lastName": "Xiao",
    "gender": "F",
    "classYear": 2020,
    "major": [
        "COSI"
    ],
    "job": [
        [
            "Business Consulting Intern",
            "2m"
        ],
        [
            "Software Engineering and Data Analytics Intern",
            "4m"
        ]
    ]
}
```

## Merging Job Titles

Because we have over two thousands unique job titles, it would be very hard to visualize and read without any merging. We apply a merging algorithm which replaces job titles with lower occurrences with similar job titles with higher occurrences.

E.g.,

{{< columns >}}
**Before merging**:

    RPA Developer
    Associate Programmer
    DevSecOps Engineer II
    Principal Software Engineer, Application
    Software Engineer
    Consultant
    Data Science Consultant
    Advisor
    Network Consultant
    Intellectual Property Attorney
    Patent Attorney
    Chief Intellectual Property Attorney

<--->
**After merging**:

    Software Engineer
    Software Engineer
    Software Engineer
    Software Engineer
    Software Engineer
    Consultant
    Consultant
    Consultant
    Consultant
    Attorney
    Attorney
    Attorney
{{< /columns >}}

Using the merging algorithm, we have reduced the job titles from **2613** to **36**.

### Algorithms

Here is a shorter version of how I merge the titles:

```python
dict_tags = {
    'Software Engineer' : [
        'Software Engineer',
        'Senior Software Engineer',
        'Software Developer',
        'Principal Software Engineer',
        'Software Development Engineer',
        'Software Architect',
        # ......
    ],
    'Software Engineer Intern' : [
        'Software Engineer Intern',
        'Software Engineering Intern',
        'Software Development Intern',
        'Software Intern',
        'Software Engineer Internship',
        # ......
    ],
    'Consultant/Advisor' : [
        'Consultant',
        'Senior Consultant',
        'Principal Consultant',
        'IT Consultant',
        'Advisor',
        'Senior Consultant - Financial Services',
        'Technical Consultant',
        # ......
    ],
    'Founder/Owner' : [
        'Co-Founder',
        'Founder',
        'Owner',
        'Founder and CEO',
        'Co-Founder and Operational CFO',
        'Co-Founder and CTO',
        'Co-Founder and CEO',
        # ......
    ],
# ......
    'Analyst' : [
        'Analyst',
        'Senior Analyst',
        'Application Analyst',
        'Programmer Analyst',
        'IT Development Analyst',
        # ......
    ],
    'Marketing' : [
        'Freelance Marketing',
        'Director of Global Marketing',
        'Product Marketing Manager',
        'Senior Director of Fieling Marketing',
        'Marketing Manager',
        # ......
    ]
}
```
Basically, job titles inside the square bracket `[` and `]` will be replaced by job titles inside the quotation marks `'` and `'`. E.g., `Senior Analyst` will be replaced by `Analyst`.

{{< hint danger >}}
**Be aware! The following webpage's code size is pretty large!**
{{< /hint >}}

[A complete version of the algorithm can be found here.](../../utilities/algorithm)

## Unifying Time Format

Before, the **"years of service"** section is formatted as `"xyxm"`. E.g., `"1y3m"`, `"3y"`, `"8y1m"`. In order to ensure a faster data visualization process, I have unified the time to "years" unit. E.g., `1y3m` will be `1.25` years; `3y` will be `3` years; `8y1m` will be `8.08` years.

## Results of Cleaning

After the cleaning process, the data is ready to go as a `json` file. It's very easy to just visualize it using the `json` format or first convert it to `.csv` or `.xlsx` format and then visualize it.