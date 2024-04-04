# Instagram-user-analytics
Data analytics project done using SQL workbench

## Project Introduction

In this project data analysis involves analyzing user interactions and engagement with the Instagram app to provide valuable insights that can help the business grow.

This include how users engage with a digital product, such as a software application or a mobile app.

It is basically divided into two parts: 
- Marketing Analysis
- Investor Metrics

## Business Task

To analyze data of Instagram in various aspects and help different teams plan their upcoming events and strategies accordingly to grow overall business.

## Approach

Our approach to this project will be mainly divided into two main parts:

- Marketing Analysis
	- Loyal user reward
	- Inactive user engagement
	- Contest winner declaration
	- Hashtag research
	- Ad campaign launch

- Investor Metrics
	- User engagement
	- Bots and fake accounts

## Marketing analysis


### Loyal user reward

Task : Identify the five oldest users on Instagram from the provided database 

```SQL
select * from users order by created_at limit 5;
```
### Inactive user engagement

Task: Identify users who have never posted a single photo on Instagram
 
```SQL
select distinct username from users
left join photos on users.id = photos.user_id
where photos.id is null;
```

### Contest Winner Declaration

Task: Determine the winner of the contest, where the user with the most likes on a single photo wins.

```SQL
select users.id, users.username, count(likes.photo_id) as no_of_likes
from  likes inner join photos on likes.photo_id = photos.id inner join users on photos.user_id = users.id
group by likes.photo_id
order by no_of_likes desc;
```

### Hashtag Research

Task: Identify and suggest the top five most commonly used hashtags on the platform

```SQL
select tag_name, count(tag_name) as no_of_tags
from tags inner join photo_tags on tags.id = photo_tags.tag_id
group by tags.tag_name
order by no_of_tags desc
limit 5;
```

### Ad Campaign Launch

Task: Determine the day of the week when most users register on Instagram

```SQL
select count(*) as total_users, DAYNAME(created_at) as day_name
from users
group by day_name
order by total_users desc;
```

## Investor Metrics

### User Engagement

Task: Calculate the average number of posts per user on Instagram. Also, provide the total number of photos on Instagram divided by the total number of users

```SQL
select
(select
	count(id)
from
photos) / (select count(DISTINCT user_id)
from
photos) as average_posts,
(select count(id)
from 
photos) / (select count(id)
from 
users) AS ration_of_photo_by_users;
```

### Bots & Fake Accounts

Task:  Identify users (potential bots) who have liked every single photo on the site

```SQL
with potential_bots as (
select users.username, count(likes.photo_id) as photo_likes from likes inner join
users on user.id = likes.user_id group by users.username)

select username, photo_likes from potential_bots where photo_likes = (select count(*) from photos) order by username;
```

## Insights

- We have identified 5 oldest users, marketing team can plan strategy for them for being loyal users which can motivate other users to stay with platform.

- We have found 26 users which are inactive, we can plan activity or push notifications to encourage those user to use the platform.

- We have found winner of our contest, we should encourage such contests and engage users to take participations to improve overall user engagement.

- We have found top 5 used hashtags of the application. Team should work on recommending these hashtags to users while creating a new post as it will help us improve user experience.

- We have identified days when mostly a new user gets registered, our team can plan ad-campaign strategy to make sure we are sending notifications or promotions on or prior to such days so that we can have maximum users registered on our platform.

- We have found average number of posts and ratio of customer with number of post, we can use this data to share with stake holders to show potential of our application so that they can trust and invest in our growth.

- We have also identified potential bots, this data will help  team to remove such potential bots to avoid fraud that might happen and encourage people to have real accounts and information to share which will result in positive user experience. 
 
``**Please refer to Attached PPT for detailed steps and SQL output for all queries**``

### Thank you! Please share your valuable feedback! 
