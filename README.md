# Data analysis on in-vehicle coupon recommendations


## Data
This data comes from the [UCI Machine Learning repository](https://archive.ics.uci.edu/ml/datasets/in-vehicle+coupon+recommendation) and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios, including the destination, current time, weather, passenger, etc., and then asks people whether they will accept the coupon if they are the driver. Answers given that the users will drive there “right away” or “later before the coupon expires” are labeled as “Y = 1”, and answers “no, I do not want the coupon” are labeled as “Y = 0”. There are five different types of coupons—less expensive restaurants (under $20), coffee houses, carry out and take away, bars, and more expensive restaurants ($20–$50).


## Deliverables
This is a a brief report that highlights the differences between customers who did and did not accept the coupons. The exploratory data analysis uses plotting, statistical summaries, and visualization using Python.


## Data Description
The attributes of this data set include:

1. User attributes
   - Gender: male, female
   - Age: below 21, 21 to 25, 26 to 30, etc.
   - Marital Status: unmarried partner, single, married partner, divorced, or widowed
   - Has children: 0 or 1
   - Education: some college - no degree, bachelors degree, associates degree, high school graduate, graduate degree (Masters or Doctorate), or some high school
   - Occupation: architecture & engineering, business & financial, etc.
   - Annual income: less than $12500, \$12500 - $24999, \$25000 - $37499, etc.
   - Car: type of car
   - Number of times that he/she goes to a bar every month: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
   - Number of times that he/she buys takeaway food every month: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
   - Number of times that he/she goes to a coffee house every month: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
   - Number of times that he/she eats at a restaurant with average expense less than $20 per person every month: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
   - Number of times that he/she goes to a restaurant with average expense $20–$50 per person every month: 0, less than 1, 1 to 3, 4 to 8 or greater than 8

2. Contextual attributes
   - Driving destination: home, work, or no urgent destination
   - Location of user, coupon and destination: we provide a map to show the geographical location of the user, destination, and the venue, and we mark the distance between each two places with time of driving. The user can see whether the venue is in the same direction as the destination and the driving distance (in minutes) to the venue.
   - Weather: sunny, rainy, or snowy
   - Temperature: 30F, 55F, or 80F
   - Time: 7AM, 10AM, 2PM, 6PM, or 10PM
   - Passenger: alone, partner, kid(s), or friend(s)

3. Coupon attributes
   - time before it expires: 2 hours or one day
   
   
## Summary of Findings
### 1. We have simplified and cleaned the data:
- The column `toCoupon_GEQ5min` is `1` for all drivers. That means, all the restaurants/bars/coffee houses/etc. are at least five minutes away from the driver. We dropped this column as it has no contribution to the problem.
- The column `direction_opp` is the opposite of the column `direction_same`. Hence, we dropped it.
- The columns `toCoupon_GEQ15min` and `toCoupon_GEQ25min` have both the unique values `0` and `1`. We combined the two columns into one column called `driving_distance`.
- Since the column `car` has more than 99% missing values, we dropped it.
- The five columns `CoffeeHouse`, `Restaurant20To50`, `CarryAway`, `RestaurantLessThan20`, and `Bar` have less than 2% missing values each. We imputed these missing values by replacing them with the most common class.

### 2. General coupon analysis results:
- 56.8% of all drivers chose to accept the coupon.
- The coupon `Coffee House` has the highest occurance (31.5%), whereas the coupon `Restaurant(20-50)` has the lowest occurance (11.8%).
- The coupon `Carry out & Take away` has the highest acceptance rate (73.5%), closely followed by the coupon `Restaurant(<20)` (70.7%).
- The coupon `Bar` has the highest decline rate (41.4%), closely followed by the coupon `Restaurant(20-50)` (44.1%).
- The `temperature` `80F` has the highest occurance (~51%), followed by `55F` (~31%), and then by `30F` (~18%).

### 3. Investigating the `Bar` coupons:
- 41% of the bar coupons were accepted.
- Drivers who accepted the bar coupons do very likely go to a bar more than 3 times a month.
- Drivers who accepted the bar coupons do likely go to a bar more than once a month. Among this group, drivers who are not with a kid in the car are more likely to accept bar coupons.

### 4. Investigating the `Coffee House` coupons:
- 49.9% of coffee house coupons were accepted.
- Drivers who accepted the coffee house coupons do likely go to a coffee house more than once a month. Among this group, drivers below the age of 21 OR drivers for whom the coffee house of the coupon is in the same direction as their current destination are more likely to accept coffee house coupons.
- Drivers who accepted the coffee house coupons do likely go to a coffee house and are not with a kid in the car. Students driving at 10AM or 2PM are very likely to accept the coffee house coupons, and so are drivers who head to work under snowy weather.


## Link to Notebook

[in-vehicle_coupon_recommendation.ipynb](https://github.com/jessi88/in-vehicle_coupon_recommendation/blob/main/in-vehicle_coupon_recommendation.ipynb)
