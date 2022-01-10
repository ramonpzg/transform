# Metrics Stores vs Feature Stores

Deriving value from data, whether for consumption or further value generation within a (machine learning) system, requires care, ingenuity, 

## Table of Contents

1. Overview
2. Metrics
3. Metrics Stores
4. Features
5. Features Stores
6. Advantages
7. Dissadvantages
8. Why do we need Stores?
9. What to look for in either solution
10. When should you adopt either?
11. Recap

TL;DR

> "You should consider Metrics Stores and Feature Stores as part of the building blocks of your data and ML stacks when, regardless of the size of your org, you have different teams building analytical products that benefit from the same information."

## 1. Overview (Motivating your KPIs and Movies Recommendations)

An almost ubiquitous aspect of modern life is that most of us have and need a job in order to put food on the table and pay for services such as Netflix, which provide us with entertainment for our lazy Sunday fix. To get through our jobs, and be successful in our chosen careers, some of us need to achieve goals that are usually measured in terms of Key Performance Indicators (KPIs) or metrics. These KPIs might directly or indirectly affect the performance of our team, or a key metric at our company. Conversely, in order for Netflix to personalize our experience and recommend us the next movie, it needs to know some of the characteristics, or features, that make us who we are in and outside of the platform (e.g., gender, age, most watched genre, ...).

The number of metrics and features needed for each, work and a custom experience, can be plenty and their complexity -- the ways in which each is generated -- has no creative ceiling. In other words, just as purchasing a carton of milk and a t-shirt could be done at their respective dairy and cotton farms, generating metrics and features could be done from their respective databases. What we need would just need to be assembled by milking the cows, sewing the cotton, and writting SQL queries. Luckily, to solve all these problems we have convenience, clothing, metrics and feature stores, and in this blogpose we'll cover the latter two.


## 2. Metrics

Out of the many similarities different companies have, the most notable one is that they all have metrics they need to keep track of. After all, regardles of the product or service they may provide, "if you can not measure it, you cannot improve it."

A more technical definition of metrics tells us that these are quantifiable measures used to track and asses the status of a specific process at a given point in time. To put this into perspective, imagine that you are in the business of selling a nicely packaged boundle of spirits and mixers (a.k.a. a cocktail), and that you'd like to know, as precisely as possible, how many and which of these boundles improves best the financial health of your bar, e.g. pays for you bar's rent, staff's salary, overall supplies, etc. One way to figure it out would be with the metrics `revenue_per_menu_cocktail` (which contains all of the signature cocktails you have worked so hard to create) and `revenue_per_classic_cocktail` (which contains all the classics such as an old fashion, a manhattan, or a cosmopolitan, among many others).

TODO: Add picture of customer ordering a signature, another ordering a classic (old brittish snob ordering old fashion) and the bills and metrics on the side.

These metrics, among many others, help us observe and understand how what we provide to our customers will affect the bottom line of our business. Metrics may not mean much to people outside your organization, but they represent a map we should use to help guide ourselves and our customers.

Metrics vary by industry and company, but there are overlaps across both. For example, different dating apps optimize daily active users (DAU), which is the ratio between users that logged into the app on a given day to use it, over the number of all users registered on the app. While this example is context specific, DAU is a universal metric for companies with a subscription service like Spotify (a music provider), and the NY Times (a news provider).

In contrast, metrics that are specific to a product, especially those with a pattent behind them, we'll be unique, and only valuable for, the company developing or using such product. For example, 

As you can imagine, companies collect different amounts and varieties of data. Moreover, different departments such as finance and marketing might need to create unique metrics or share similar ones across the organization. After all, we'd like to use the finance team's revenue recipe for anything sales related, and the marketing team's ad conversion multitude of recipes for any other downstream application or analysis. With that in mind, it follows that there has to be a better way to collaborate across teams and keep track of what's important to our companies, and the solution to this is what we'll cover next, Metrics Stores.

## 3. Metrics Stores

Think about the 