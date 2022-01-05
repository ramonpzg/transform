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

An almost ubiquitous aspect of modern life is that most of us have and/or need a job in order to put food on the table and pay for services such as Netflix that provide us with entertainment for our lazy Sunday fix. To get through our jobs, and be successful in our chosen careers, some of us need to achieve goals that are usually measured by KPIs or metrics. These KPIs might directly affect the performance of our team, or indirectly affect a key metric for our company. Conversely, in order for Netflix to personalize our experience and give us our next movie recommendation, it needs to know some of the characteristics, or features, that make us who we are in and outside of the platform (e.g., gender, age, most watched genre, ...).

The number of metrics and features needed for each, work and personalization, can be plenty and their complexity -- the ways in which each is generated -- has no creative ceiling. In other words, just as purchasing a carton of milk and a t-shirt could be done at their respective dairy and cotton farms, generating metrics and features could be done from their respective databases. What we need would just need to be assembled by milking the cows, sewing the cotton, and writting SQL queries. Luckily, to solve all these problems we convenience, clothing, metrics and feature stores, and in this blogpose we'll cover the latter two.


## 2. Metrics

