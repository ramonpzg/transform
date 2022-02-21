# Metrics Stores vs Feature Stores

Deriving value from data, whether for internal consumption or for prediction purposes within a (machine learning) system, requires careful engineering, design thinking, and a team of motivated problem solvers with a shared goal. To accomplish this task, deriving value from data, we have the metrics store and the feature store.

## Table of Contents

1. Overview
2. Metrics
3. Metrics Stores
4. Features
5. Features Stores
6. Advantages and Similarities
7. Disadvantages and Differences
8. Why do we need Stores?
9. When should you adopt either?
10. What should I look for in either solution?
11. Recap

TL;DR

> "You should consider Metrics Stores and Feature Stores as part of the building blocks of your data and ML stacks when, regardless of the size of your org, you have different teams building products or deriving insights from the same information in an inconsistent way."

## 1. Overview (Motivating your KPIs and Movies Recommendations)

An almost ubiquitous aspect of modern life is that most of us have and need a job to put food on the table and pay for services such as Netflix, which provide us with entertainment for our lazy Sunday fix. To get through our jobs, and be successful in our chosen careers, some of us need to achieve goals that are usually measured in terms of Key Performance Indicators (KPIs) or metrics. These KPIs might directly or indirectly affect the performance of our team or a key parameter of the success of our company. On the other hand, for Netflix to personalize our experience on those lazy Sundays, and recommend us the next best movie to watch, it needs to know some of the characteristics, which are also called features, that make us who we are inside and outside of the platform (e.g., gender, age, most-watched genre, etc.). You could say that some aggregation of our information and that of others similar to us make up one or more of Netflix's KPIs.

The number of metrics and features tracked at work or used to create bespoke experiences, respectively, can be plenty and their complexity (i.e., the ways in which each is generated) has no creative ceiling. For example, just as purchasing a carton of milk and a t-shirt could be done at their respective dairy and cotton farms, generating metrics and features could be done from a particular database. What we want would just need to be assembled by milking the cows, sewing the cotton, or writing SQL queries. Luckily, to solve all these problems we have convenience, clothing, metrics and feature stores, and in this blog post we'll cover the latter two, so let's start with metrics.


## 2. Metrics

Out of the many similarities companies share, the most notable one is that they all have metrics they need to track to observe the overall progress of their organizations. After all, regardless of the product or service a company provides,

> "if you can not measure it, you cannot improve it" (Lord Kelvin circa 1860).

A more technical definition of metrics tells us that these are *quantifiable measures used to track and assess the status of a specific process at a given point in time*. To put this into perspective, imagine that you are in the business of selling a nicely packaged bundle of spirits mixed with other things (a.k.a. you own a bar and sell, well, cocktails) and that you'd like to know, as precisely as possible, how many and which cocktails or beers give you the most financial return to pay for your establishment's rent, your staff's salary, overall supplies, etc. One way to figure this out would be by calculating the metrics `revenue_per_signature_cocktail` (which contains all of the signature cocktails you have worked so hard to create) and `revenue_per_classic_drink` (which may contain beers or some classic cocktails like an old fashion, a Manhattan, or a cosmopolitan, among others).

![bar](../images/bar-metrics.jpg)

These metrics would help us observe and understand how what we provide to our customers will affect the bottom line of our business. Even though these metrics may not mean much to people outside our bar, they represent a map we should use to help guide us towards one or more goals, e.g. to be the best bar in the world. To illustrate how these metrics get created, assume all of your transactions get placed into a table such as the following one.

| Idx | Item (S=Signature)       |Price|    Date   |Quantity|Signature|
|:---:|:------------------------:|:---:|:---------:|-------:|:-------:|
|  0  | Old Fashion              |  17 | 03-Jan-22 |    2   |    0    |
|  1  | Shiny Palace (S)         |  24 | 03-Jan-22 |    4   |    1    |
|  2  | Multi-vodkaTini (S)      |  23 | 03-Jan-22 |    1   |    1    |
|  3  | Pale Ale                 |   7 | 03-Jan-22 |    3   |    0    |
|  4  | Lager                    |   6 | 04-Jan-22 |    3   |    0    |
|  5  | Crazy Tiki Tower (S)     |  28 | 04-Jan-22 |    2   |    1    |
|  6  | Bananalicious Martini (S)|  25 | 04-Jan-22 |    1   |    1    |
|  7  | Aperol Spritz            |  15 | 04-Jan-22 |    2   |    0    |
|  8  | Caribbean Sugarum (S)    |  26 | 05-Jan-22 |    2   |    1    |
|  9  | Watermelicious (S)       |  28 | 05-Jan-22 |    1   |    1    |
| 10  | Manhattan                |  17 | 05-Jan-22 |    3   |    0    |
| 11  | Brown Ale                |   7 | 05-Jan-22 |    4   |    0    |

When we think of metrics we think of aggregated results by different dimensions. In this instance, a dimension in the table above is represented by any column that is not a continuous one (e.g. Price) and a measure to aggregate a dimension by usually involves time or any other category. For example, tracking the average revenue made, the emails sent out for ad campaigns, the churn experienced, and others, only (or mostly) make sense from a time perspective (i.e. average revenue per month, emails sent out in a week, or daily churn). This means that we want to see the sums, averages, and the like by the minute, hour, day, week, or any other value to reason about their change from X point in the past to today or whichever date we are interested in. That said, the aforementioned metrics of interest for the bar would look like the following ones after being calculated.

| day_of_year | revenue_per_classic_drink | revenue_per_signature_cocktail |
|:-----------:|:---:|:--------:|
|  Day 3    | 55 | 119 |
|  Day 4    | 48 | 81 |
|  Day 5    | 78 | 80 |

In addition to those in bars and restaurants, metrics vary by industry and company, but there are overlaps across both. For instance, different dating apps optimize daily active users (DAU), which is the ratio between users that log into an app on a given day over the number of all users registered on the app at that same point in time. While this example may seem very context-specific, DAU is a universal metric for companies with a subscription service, for example, Spotify (a music provider) and the NY Times (a news provider). In contrast, metrics that are specific to a product, especially those with a patent behind them, will be unique and valuable for the company developing with or using such a product. The gaming industry is notorious for its patent applications and, as such, some of their metrics range from complex in-game marketplaces using real currency to new video rendering systems that increase the quality of a game.

As you can imagine, all these metrics require data and companies collect a wide variety of data, at distinct velocity, veracity, and validity. Moreover, different departments such as the finance and marketing ones might need to create unique metrics or share similar ones across an organization in any industry. After all, if we wanted to create a report based on the metrics from these two departments, we'd like to use the finance's team revenue recipe, and the marketing's team ad conversion recipes rather than one curated by anyone else in the company. Beyond acquiring such metrics, we would use downstream applications for analysis to enable better decision-making processes. With this in mind, it follows that there has to be a good way to collaborate across teams and keep track of what's important to our companies, and that solution is what we'll cover next, the Metrics Stores.

## 3. Metrics Stores

Think about the last time you went to your local supermarket, chances are, you knew the items you needed, the aisle where they were located, and the ballpark price of your bill -- unless we go back to the height of COVID-19, where we would take what we could get. With that in mind, having a metrics store at your organization is like having a supermarket right next to where you live, it's a convenient place to get the essentials and more. So you can think of a metrics store like a supermarket of information, whereas soon as you walk in you can see a catalog of your metrics, callable by a convenient API and with an intuitive interface to create new ones, update old ones, and delete non-useful ones.

**TODO: Add drawing of stick person staring in awe at an empty shell on the isle where toilet papers used to go during COVID, and another staring at an aisle full of metrics to pick and choose from. Don't forget the mask.**

At its core, a metrics store (should) contains three important components to provide a robust analytics workflow: A metrics framework, a metrics API, and a metrics catalog. These get combined into a solution that becomes,
1. a metrics layer in between your data and the downstream applications used by your team where,
2. anyone can define global and local metrics once, usually through the combination of SQL and YAML files, and these files are given to the metrics layer for consumption. After your company's metrics are stored,
3. downstream applications like Power BI, Hex, Tableau, or Jupyter Notebooks, can access all the metrics in the store via a Metrics Query Language API.

Having the core files written in YAML allows you and your team to use software engineering best practices to version control each metric, or group of metrics, while making the process of modifying one or more that which follows the (1) edit, (2) submit a pull requests, (3) review it, (4) approve it, and (5) repeat process.

A metrics store such as, for example, [Transform](https://blog.transform.co/the-first-metrics-store/) not only allows you to track different metrics definitions, but it also enables you to retrieve any of your metrics in an iterative fashion for analysis from your analytical tool of choice and begin your insights quest. 

Before metrics stores existed, data professionals had to write the metrics logic for their desired aggregations, load the data into their downstream application of choice (e.g. Tableau or Power BI), and only then proceed to do their analysis. This metric logic was (and still is to some degree) an operation to return a table-like object called an OLAP cube (Online Analytical Processing). You can think of these cubes as the culmination of a `groupby` query in SQL or a `pivot_table` operation using Python's beloved pandas library. In the tables returned by the latter function, the values represent your measures of interest (e.g. sales) and the columns and rows the dimensions (e.g., the year and the type of customer) you aggregated the values by. Usually, these dimensions are categories and/or a time value.

These OLAP cubes can be quite large and, most likely, will only represent a portion of your data as aggregations and, by that same aggregated nature, they will take away your ability to interrogate the data on a row-by-row, person-by-person, or transaction-by-transaction basis. This process of creating OLAP cubes can be quite repetitive and error-prone as it used to be a necessary step prior to extracting data from one (or many) potentially large tables. So you can probably begin to pair the solution provided by a **metrics framework** with the problem of having to continuously create OLAP cubes before any analysis takes place, or the benefits of having a convenient **metrics catalogue** ready for retrieval via a convenient **API**. These three core features offered by a metrics store are solutions one should look at once our organizations are ready to take metrics seriously and at scale.

There are several à la carte metrics store options that exist today, and those include [Transform](https://transform.co/), [Supergrain](https://www.supergrain.com/), and [GoodData](https://www.gooddata.com/). Other DIY approaches are tackled by open-source frameworks such [MetriQL](https://metriql.com/), which sits on top of dbt-core, and [Cube](https://cube.dev/). If you know of the modern data stack you might be tempted to think of the functionality of dbt as that of a metrics store and, in effect, there are some similarities between the two but dbt is not (at least not right now) a complete replacement for a metrics store but rather a complementary tool for them.

## 4. Features

Features are numerical representations of raw data, and they are used to train machine learning models as well as to create business metrics. Notice that the word **numerical** here is very important as features without the appropriate representation (e.g. raining and not raining versus 1 and 0, respectively), will not be of use to a machine learning model. You can think of features as columns in a tabular dataset holding information that we can add together, subtract, or do other mathematical operations with. Let's examine the machine learning workflow in the following image to see where and how features are used.

**TODO: Drawing of the machine learning cycle (see image below for an example).**

![data-science-workflow](../images/ds-workflow.png)

In the image above you can see that a machine learning project starts with a problem that can be solved with data which contains information in the form of feature (predictive values) and labels (what we want to predict). The data might come from different sources and it will most likely require some preparation, such as that in the images below before we get to use it to train a model.
![feats1](../images/features-1.png)

![feats2](../images/features-2.png)

Once we have a trained model, we would go through an experimentation stage to evaluate it and fine-tune it to maximize our ML gains. After we are done training our model, we deploy it and monitor the predictions it makes. This cycle of producing an ML model is enabled by the features we use as well as the ones we engineer ourselves via a process called, feature engineering.

**TODO: Drawing of a carpenter or architect putting together the features of a building, house, office or anything.**

Feature engineering "*is the process of formulating the most appropriate features given the data, the model, and the task*."<sup>1</sup> Formulating new features help us extract information from rich pieces of data such as dates (e.g. 12-Jan-2022 14:20:17) and locations (e.g. 123 Startup St, San Francisco, CA 02022, USA), among many others. Conversely, feature engineering also helps us compress multiple variables with similar information into fewer variables, which in turn helps get rid of redundancy and noise in the data.

Careful selection of features to use directly in a model or to be engineered with others can drastically affect the performance of a machine learning model. Hence, getting this step of the process right might be considered by many companies that use ML, the most important one in their pipelines. That said, to get the process of selecting the right historical and real-time data right, the feature store was born.

## 5. Features Stores

Just as metric stores make the lives of data professionals easier when they need to look for the data they need, when they need it, and how they need it, the ML world has a similar product for its own data needs, the feature store.

While the definition of a feature store will be a slightly different one depending on who you ask, one definition that seems to wrap up its goals well enough is that found in a blog post by Tecton's CEO, Mike Del Baso, and its Tech Lead, Willem Pienaar, titled, *"[What is a Feature Store?](https://www.tecton.ai/blog/what-is-a-feature-store/)".* It says, feature stores are "an ML-specific data system that runs data pipelines that transform raw data into feature values, stores and manages the feature data itself, and serves data consistently for training and inference purposes." Essentially, while different companies may have different needs for a feature store, these stores allow users to define features (yes, similar to how metrics stores allow users to define their metrics), transform, serve, share them and, in some cases, monitor them to detect distribution and, potentially, concept drift.

Feature stores were created to address the aforementioned tasks in both batch and online environments. A batch environment consists of historical data, generally sitting in a data warehouse like snowflake, used to train machine learning models and make predictions for groups of customers and to use these as needed. In addition, these predictions need not be made once the model is trained and, instead, the model would be the artifact of interest that gets saved to make predictions for active customers at different time intervals. Conversely, an online environment mostly refers to real-time or on-demand inference (i.e. predictions) using data coming from the interaction of users and customers with our applications and services. Moreover, it can also refer to online training and learning. The former aims to learn from each incoming data point, and the latter uses micro batches (e.g. every 10 to 20-minutes) to retrain a model (or multiple).

The key challenge to making online inference work seamlessly is that models will often require both static and dynamic features, meaning, stored information about a user as well new information coming into our platform from the real-time usage of it. Combining these two can be tricky and approaches such as real-time transformation pipelines for incoming data -- those connected to different data sources via [Apache Flink](https://flink.apache.org/) and other tools rather than, or alongside, the warehouse -- can take too long and may increase the wait-time between the request for a prediction and providing one to a user.

Both approaches, offline and online, are very important, and depending on the nature of a company, online inference may add more value than any offline ML operation. This increases the appeal for feature stores even though it is certainly not the only value it adds to an ML team. Let's walk through some of the core components of a feature store in detail, as shown in the image below.

![feature_store](../images/fs_process.jpg)

1. **Data Access and Storage** - Data access refers to data coming from different places and at different time intervals. The two most important sources of data arrive (1) on-demand from our applications -- where data can be split into logs, usage, and 3rd party APIs, among others -- and from (2) the historical information we have already collected about our customers and their behavior in our platform, i.e. the data sitting in a warehouse. It is important to note that feature stores do not duplicate data but rather enable accessing data in the warehouse for training as needed. For the inference side, they allow us to create materialized versions (usually with [Redis](https://redis.io/)) of the data we need with low latency for online inference. Technically speaking, this means that the offline data storage needs of a feature store are met by extending the data warehouse or lake to hold the features we need when we need them.
2. **Data Transformations** within a feature store can be the same transformations applied to data sitting in a warehouse before or after its arrival (via an ETL or ELT job, respectively). This means that this is not the feature engineering process that might be part of your machine learning model package served as a REST API but rather the initial step before your model applies its own transformations to the data, i.e. the way in which you ingested the data you needed from the warehouse to train your model.
3. **Serving** refers to providing models with the latest features they need to make a prediction in real-time. For example, a user searches for a product in your marketplace and your model provides a recommendation, or another user orders a meal from your three-way marketplace and, within seconds, you provide that user with an estimated time of arrival for their meal. In both instances, the users are already members of your platforms and while you already have their static features, the dynamic ones will come in as they type a query for a video, a restaurant, a meal, etc.
4. **The feature registry** allows you to keep feature definitions in one place, making it easier to track, share and reuse features across teams with minimal effort.
5. **Feature Monitoring** aims to detect when the distribution of a feature has changed drastically between the historical and online data These changes could cause [data or concept drift](https://www.linkedin.com/feed/update/urn:li:activity:6897870268199440386/).
8. **The architects of "intelligence"** are your data scientists, machine learning or MLOps engineers creating and maintaining models in production to add value to your company. The pull data from the offline store inside the feature store, generate a model to serve predictions while keeping an eye on it. 

Lastly, it is important to note that a feature store solution does not require all of the components described above to be considered one. Instead, the most common component in a feature store is data access for online inference. Instead of highlighting all use cases here, you should check out the talks at [featurestore.org](https://www.featurestore.org/) and [applyconf.com](https://www.applyconf.com/session-video-archive/) which include excellent overviews of the solutions different companies have created in-house and/or open-sourced to the community.

## 6. Advantages and Similarities

Today, metrics stores solve many problems in and outside the modern data stack, which is an ever-evolving set of tools used to tackle modern data problems within the data life-cycle. These problems range from merging disparate data sources to transforming complex datasets for analytical consumption. Within the modern data stack, metrics stores sit between end users and the data warehouses of their organizations while providing access to metrics of all shapes and sizes in a consistent fashion. Outside of this modern data stack, metric stores give access to any tool or platform via a convenient API that does not care about the level of coolness of the tool, e.g. Excel, SPSS, and Tableau can make use of data coming from a metrics store.

Some advantages of metrics stores are closely tied to the problems that they solve, and here are some of the common ones.
1. Provide consistent definitions for metrics and build trust among end-users.
2. Enable software engineering best practices.
3. No more wasted time writing queries/code instead of deriving insights from data.
5. No more (or more like less) inaccurate values at the time of reporting.
6.  No more duplicate data or increased costs with the use of cloud resources for computing metrics.

Some of the advantages above also overlap with those of a feature store. For example, imagine two data science teams building models for different purposes but with the same data, which might end up creating the feature DAU but with different logic. One might defined this feature as `active_users` / `all_users` while another team might define it as (`active_users` + `daily_subscribers`) / `all_users`. You might think, what's the big deal with the two, and the answer is distribution drift. While it is not preposterous to think that a new subscriber might not be using the app immediately after they signed up, this is not always the case.

**TODO: drawing of a woman, a man, and other genders downloading a dating app, showcase this in a matrix. One logs into an app, finishes the setup and starts swiping, one dreads the thought of not having their religion/gender identity as an option (i.e.), another can't pick the right pictures, and another cannot think of any clever prompts to put down. The last drawing, all walking away and one stays swiping.**

Imagine you just downloaded a dating app and that, as you go through the set-up, you encounter that your pronouns and gender identity are not available, that you can't think of something clever to put down as a prompt for your profile, or that you struggle to pick the right pictures. All these problems make you put off **logging in** to the app to start swiping until later but meanwhile, you have already signed up to the app and that extra data point for the latter DAU example is just, well, noise.

That said, another great advantage of feature stores is that they create materialized versions of your features on the fly so that your model can make predictions in an **online environment**. They abstract away the complexity of having multiple data pipelines and enable sharing features across teams. Which in turn reduces development time and increases collaboration. Not every data scientist thinks the same way and/or will have the foresight or experience to create the same features. Making the collaboration part a key advantage of a feature store.

An interesting yet not-surprising similarity between the two stores is that they both work almost exclusively with tabular data. Furthermore, they can both be complementary to each other when you take out the online aspect of feature stores. In fact, the similarities go up to the implementation details as you write code and track features and metrics that will be used for downstream purpose, an ML model or dashboard creation.

## 7. Disadvantages and Differences

Both stores require some technical expertise on the set-up side. Metrics stores can be set up by the data, analytics, or DevOps engineering team and be consumed via its UI by different end-users. Here, your typical click-and-drop functionalities can coexist with code for version control and more complex use cases. In contrast, feature stores can be set up by their end-users, machine learning and DevOps engineers, data engineers, and more software development savvy data scientists.

Another disadvantage shared by both is that these are tools that will be easier to adopt by larger companies rather than smaller ones. Building a solution with a feature store requires engineering skills, thorough testing, and maintenance, and while these can be done by the end-user, the same is not true for a metrics store where the end-user need not be software-savvy data professionals. The process of creating one from scratch with some of the open-source tools available (e.g. MetriQL, cube, etc.) would require, at the very least, a dedicated person, if not a team and some decisions might be driven by efficiency and habit rather than the end-user itself as this person might not be involved in the creation of the store.

**TODO: cartoon showing excel spreadsheet projection with a whiteboard and more cells and columns in the background.**

Another important point about either store is that handling large datasets in either direction, too many rows or too many columns can be a challenge. If you think about the process of creating measures that matter for the company, a calculation based on too many data points might slow down the aggregation process. Conversely, hand-crafting 10 to 30 complex features to be tracked by the feature store might be a piece of cake, but the same process with thousands could prove to be unproductive for both small and large teams.

A couple of important differences that may open up the discussion for the interoperability of the two include the following. (1) Metrics can be fed to an ML model but features might be meaningless as metrics. (2) Feature stores are optimized for online (i.e. as close as, if not completely at, real-time) usage while metrics stores work (mostly, although not solely) with batch data. (3) Metrics tend to have a longer shelf-life than features, meaning, features can come and go as the products and services of a company mature, but a company metric tied to its success need not be touched nor changed by anyone. (4) Metrics stores should support simple-to-complex metrics while feature stores should make the simple ones easy to implement for fast and effective iteration.

### Metrics vs Features Examples

![](../images/metrics_churn.png)

One way to differentiate between metrics and features is by thinking through the problem of churn. On the metrics side (see image above) you have a ratio represented by the number of customers that have left your company, divided by the number of customers you still have, and across some time dimension (e.g. day, week, month, quarter, etc.). In contrast, in machine learning the feature of churn is represented as a 1 or a 0, churned or current customer (as shown in the image below), and your job is to use some or all of the features at your disposal to train an algorithm that will learn to predict this 0 or 1.

![](../images/features_churn.png)

In essence, in one instance you are looking at an aggregation of customers by a time component while in the other you are looking at each individual observation and their characteristics. Another way of thinking of this is that the former is more human friendly while the latter is more machine friendly. The word friendly in the context of the metric means that the max number of observations you might see will be 365 (if looking at daily churn in a year), while for a machine learning problem you could be staring at an endless list of customers for days, weeks, etc., to train only one model.

**TODO: Add a cartoon starting at a graph going up or down with churn, and another of a person with glasses staring at an endless spreadsheet with data.**

## 8. Why do we need Stores?

Some of the reasons we need stores for metrics and features overlap with why we need supermarkets and clothing stores. While we can go and hunt for food every day, or weave away the clothing pieces we want to wear, it is much better to have the creation and distribution of commonly used products (just like metrics and features) in one place and create some separation of concerns between core activities for daily functioning and value-added from other businesses.

Having your metrics logic separate from a downstream application will allow data consumers to spend more time deriving insights in the same way not having to hunt would allow a chef to spend more time in the kitchen worrying about the flavour and taste of food. In contrast, handing over the feature creation and serving process to a feature store would allow a team of data scientists to focus on creating and productionising ML at their organizations.

Defining metrics as code and making it so that changes to a metric definition have to follow software engineering best practices will help put in place a systematic process that is both battle-tested and scalable. In addition, it could have the added effect of improving an organisation's analytics team in software engineering direction.

Features based on human behaviour will always be at a distribution shift risk as we change our minds all the time or our preferences tend to evolve due to changes in our environment. For example, our preferences in food, videos, news articles, and tweets might change on a day-to-day basis while our preferences for cars, flights, and houses might change at a much slower pace. Hence, being able to detect changes between in what I liked yesterday versus what I am interested in today, is a feature that feature stores can enable in a well-put-together machine learning system.

## 9. When should you adopt either?

If you want to empower more data producers and consumers at your organization to take advantage of the data at their disposal, all while keeping the consistency, reusability, and governance of metrics' definitions in check, then a metrics store might be a good solution for you.

If ML is not a "nice-to-have" at your organization, and online inference is part of your core offering, the feature stores might be a good solution for your ML team. If all of your data scientists and ML Engineers have to build their custom data pipelines for each model, then sharing and reusing the commonly generated features would be made more straightforward via a feature store. If you need a way to monitor the distribution shifts between historical and incoming data, you know the drill now.

## 10. What should I look for in either solution?

On the metrics store side, the most important characteristics to look for include (1) a **metrics framework** where you could define and manage your metrics once. (2) A **metrics catalogue** that provides an interface for your metrics knowledge. And (3) a **metrics API** to allow your store to meet consumers where they are at.

On the feature stores side it is not a matter **what will I get** but rather **what will I be able to solve** with one. In particular, if a feature store will solve the following questions for you, you can safely answer the main question for this section.
1. Can I help reduce the amount of feature pipelines developed for model training and serving?
2. Can I avoid unnecessary data pre-processing before training and serving?
3. Can I monitor my features to keep data quality high, i.e. can I monitor incoming data for distribution and concept drift?
4. Can I quickly access static features (e.g. age, occupation, income, etc.) and combine them with dynamic ones (e.g. location, destination, query, etc.) to provide predictions to users with minimal latency?
5. Can I create reproducible training datasets?

## 11. Recap

Metrics allow us to track what matters for our organizations while features are the fuel for the machine learning models that help us personalize experiences and provide recommendations, among others. Metrics stores give us a platform to write, govern, and serve metrics in a common language, and feature stores abstract away the searching and reshaping of features while providing scalability in both, online and offline environments.

Lastly, if you need consistency, scalability, reusability, and any other x-ability to boost the performance of your data-driven decision process as well as your ML operations, then you might want to think about adopting one or both of these stores.

![maestro](../images/maestro_orchestra.png)

## References

[1] - _Feature Engineering for Machine Learning_ by Alice Zheng and Amanda Casari