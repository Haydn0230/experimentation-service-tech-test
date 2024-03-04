# Experimentation Service Tech Test
Welcome to the experimentation service tech test! 

We've been asked to develop an app thats going to allow us to split customers into equal shares and then serve 
different versions of the website to them to see which one they prefer. We need to keep track of who's seen what so 
we can accurately monitor the success of different version of the site. The format of this test is split into 3 different tasks, 
with each building on the previous.

### Tech
There are no specific requirements around tech, so please choose whatever language will best showcase your abilities! We're more interested 
in understanding your ability to problem solve and explain why you've tackled the problem in the way you have. We have provided a 
dockerfile to make things easier but feel free to ignore this if you'd prefer to use something else. 


## Task 1
Situation: Our front ends want to be able to split customers between experiments, but they want us to do the assigning of the experiments for each user.
Lets write a service that takes an id and returns an experiment. To do this we are going to need an app that allows us to:
 - create an experiment
 - assign an experiment
 - delete an experiment 

<details>
<summary>Example Request</summary>

```
  localhost:8080/experiment/{customer-id}
```
</details>

<details>
<summary>Example Response</summary>

```json
{
    "experiment": [
        {
            "id": "2bd1e4d7-09fd-4b24-9359-52f42b46e090",
            "created": "2024-03-04T10:44:22.531+00:00",
            "name": "colour",
            "type": "yellow"
        }
    ],
    "userId": "d7cf75e1-90dd-4bda-ad63-06fcdcce7194"
}

```
</details>

---
## Task 2 
Situation: The front ends really like our service, but they want the ability to track which customer is on which experiment over time, so lets store the experiment that the customer has been assigned to for future use
<details>
<summary>Hint</summary>
We can store the values in a map to satisfy the requirement of persisting experiments between requests
</details>

---
## Task 3
Situation: The website has become so popular because of all our experiments! 
But this has meant that the single app we have deployed is struggling to cope, when it goes down we don't have anything to tell us which customer is on which experiment, disaster!
So we need to increase the fault tolerance of the system. How can we do this?

<details>
<summary>Hint</summary>
We need to horizontally scale, so we need to remove the state out of the app and into a caching service like redis (look at the dockerfile) 
To spin up Redis do the following:

 - Run the following at the root of the repository```docker-compose up -d```
 - Check its running with ```docker ps```

We can interact with redis via the redis-commander image, if we go to ```localhost:8081``` we can view our data via a GUI. 

</details>

---