### General

1. **what challenges did you face and how did you overcome?**

   2 calendar (front-end). most complex component in our project. no body wants to accept this task (include me).

   4 days until deadline to complete this task before demo last month, an almost impossible task.

   finally, my tutor Kris encourage me to challenge my self (because I designed this calendar, and its back-end system). I accept it in consideration of project demonstration performance.

   1. Discuss if it is necessary to complete or delivery this task.

   2. Discuss the feasibility of my idea of development. I had an idea about this calendar, and have a prototype calendar in simple tech stack, like native HTML.

   3. determine the priority of functions. sort them.

   4. code the most important function, test, and do it again and again according to the priority list.

   5. Until the deadline, which is 1 month age, 80% of these 2 calendars are complete.

      

2. **how is your idea/solution different from existing one?**

   We searched some current booking website like **open table**. Although they are popular to customers, their booking system is not flexible enough. We can't see their business setting system, but we can still find something in customer booking page.

   We found that user can only select from several fixed start time, with a fifteen 15 or thirty 30 minutes interval. For example, 10:00 AM, 10: 30AM, 11:00 AM and so on. But we think they miss some features.

   1. The first is their start time is not flexible. In most case, store can provide service in their any business time, like 10: 05 AM, 10: 10 AM. But their current system doesn't support it. Our system solved this problem.
   2. The second is their customer cannot choose end time. For example, their service start at 10: 00 AM, but when should this service finish? There is not a clearly expectation for customer. Our system solved this problem too. 

   In our system, we have 3 different types of service duration to meet all requirements. They are fixed, unlimited, and flexible.

   1. In fixed duration, the service are fixed, like 1 hour / 1 and a half hour / 2 hours, and so one. However, customer can choose start time at minimum of 5 minutes, like 10: 05, 10: 10.
   2. In unlimited duration, it is similar to open table's system.
   3. In changeable duration, business owner can choose a minimum and maximum service time, like 1 hour to 2 hours. Customers can choose service duration themselves within this range, like 1.5 hour.

   These are the reasons why our system is so different and unique.

   

### Tech

**Back-end**

1. **Mongoose Aggregate Framework**:

   Searching system. query cross multiply table. It has a pipeline, unique operator syntax. 

   Example: we use it in filtering store's max Person Per Section. In store table, their is no such a field. This filed exists in store's related service info. So, we choose Mongoose Aggregate pipeline, and filter's stores in their related service info table.

   

2. **Core Algorithm**. 3 tables. If business owner wants to add time interval like [9:00 - 11:00], data will be stored as [900, 905... 1055] (number). 

   Sync. 

   how and when booking record instance is created? When customer want to book a service, first of all, system will use the service info id and customer intend week to search database. If the booking record in this service and in this week exist, we will add booking information in this existing booking record. But if we don't find such a booking record, we will user service calendar template and week timestamp to create one.

3. **Sync update mechanism**. 

   This mechanism is for service info & booking record. You knew the booking record is created by service calendar and a week timestamp, and when customer wants to book a service, it will find if the booking record for selected service and selected time exists. When booking record created, it will uses the latest service info calendar template.

   But what if the service info calendar template changed? After change,  new booking record will use the latest template, but old booking record still use the old template. Sync update mechanism is designed to solve this problem.

   In this mechanism, if business owner add a time interval, system will find its service-related booking records, and add this time interval to these booking records if they are not expired. On the other hand, if business owner want to delete a time interval, we still find its service-related booking records. However, in this case, for each booking records we found, we have to determine if this time interval in each booking records has been booked by customer. For each booking records, If this time interval is not booked, we can delete it. But if this time interval is booked, we will not delete it. It can protect reservation information.

   That's all about sync update mechanism.

   

4. **Interlock system. store business time & service info.**

   This is a data protection mechanism. If the business owner wants to delete a certain business hours of the store, there must be no service during the business hours; if the business owner wants to add a service hours, the service hours must be within the business hours of the store.

   

5. **ordering system**. cooperate with Jet PPT 4 steps (pre-verification for present to customer, only show available time and service.), (customer select time and service), (verification, booking record table OR service info table, explain when and why), (decision making).

   After 4 steps, we do 2 things:

   1. Add booking information to booking record, update service reservation qty & availability statues. 
   2. Create order.

6. Joi

   

**Front-end**

1. **2 calendar. How to develop? **

   No third-party library is used. We searched current calendar library, we found that they cannot match our system. They are mostly daily based, but our system is weekly based. As a result, we decide to create a highly customized calendar system, and it can 100% suitable to our back-end and database design.

   If business owner wants to add time interval like [9:00 - 11:00], data will be stored as [900, 905... 1055] (number). These data will be send to back-end, and after verification via Joi, save to database.

   We have a repeat inspection mechanism. For example, if there is [900, 905 ...] in database, when you insert [8:00, 10:00] to database, only [8:00 - 9:00] can be insert, and [9:00 - 10:00] will be discard because they are repeated.

   When you open this calendar or update this calendar, front-end will receive latest data that I mentioned before. These data will be restructured as a new Array. Each element of this new Array is an Object, it includes attributes like day, start time, end time, and some other information for calculation. Each element represent a time tag in our calendar. After that, I use these information to calculate the position and area of this time tag in calendar.

   Once you click this time tag, you can modify OR delete it. The principle of modification and delete is similar to addition. 

   

2. **Sync button**

   In our system, each store has a business hour, and each store has several services, they do have their service hours. But you know, in most case, service business hour is similar OR completely same to store's business hour. This is why Sync button exist. It can simplify business owner's operation.

   It is more like a mechanism of initialization. In our predicted scenario, when business owner create a new service, it can use Sync button to copy store's business hour, and then modify it.

   We still have some protection mechanism there. If this service calendar is not empty, business owner cannot sync. This design is to avoid data overwriting.

   

3. **Image update system**

   1. First, we update image to Github repo, but we failed.
   2. Our tutor Kris told me to use PICGO, it is a picture bed. It can save pictures and return URL. However, all these operations are manually. It means that we can't upload picture through front-end.

   3.  Finally, we decide to use AWS S3,  Cognito & IAM. When we upload image, it will be send to AWS S3 storage bucket, and return a URL. Then we send this URL to back-end and database, this URL will be saved as a String in database document. When we use this picture, database will return this URL, and front-end can render picture directly by using this URL. 

4. 

