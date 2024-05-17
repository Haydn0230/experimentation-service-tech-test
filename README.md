# Experimentation Service Tech Test
Welcome to the experimentation service pair programming exercise! 

We've been asked to develop an app thats going to allow us to split customers into equal shares and then serve 
different versions of the website to them to see which one they prefer. We need to keep track of who's seen what so 
we can accurately monitor the success of different version of the site. The format of this test is split into 3 different tasks, 
with each building on the previous. It's a pair programming exercise where you'll be in the driving seat and will be accompanied by an engineer.

The exercise is only an hour and there's no right and wrong answer. We're interested in how you approach the problem and to see how you work. It's not an exam, so use whatever resources you might normally use to help you solve the problem. Everyone uses Google + Stack Overflow right? And the engineer accompanying you will be there to talk through the problem and help you out if you need.

### Tech
There are no specific requirements around tech, so please choose whatever language will best showcase your abilities! We're more interested 
in understanding your ability to problem solve and explain why you've tackled the problem in the way you have.


## Task 1 - Create a management endpoint for experiments
Situation: Our front ends want to be able to split customers between experiments this involves us managing and assigning the experiments for each user.
Lets write a service that allows us to manage experiments. To do this we are going to need an app that allows us to meet the following requirements:

Requirements: 
- Be able to create an experiment
- Be able to retrieve the full list of experiments

<details>
<summary>Create experiment example</summary>

Verb: **POST**

Endpoint:
```
localhost:8080/experiment
```

Request:
```json
{
    "name": "colour",
    "type": "red"
}
```

Response
```json
{
  "experimentId": "4fabbf99-20fa-4957-8c3c-8d46eeadea87"
}
```
</details>

<details>
<summary>List experiment example</summary>

Verb: **GET**

Endpoint:
```
localhost:8080/experiment
```

Response
```json
[
    {
        "id": "8fda77e3-f909-41e3-a6fc-63c25334de09",
        "date": "2024-02-27T16:16:43.801+00:00",
        "name": "colour",
        "type": "brown"
    },
    {
        "id": "f298c447-3917-446d-acdd-c8f7a123c27a",
        "date": "2024-02-27T16:16:43.801+00:00",
        "name": "colour",
        "type": "yellow"
    },
    {
        "id": "4fabbf99-20fa-4957-8c3c-8d46eeadea87",
        "date": "2024-02-27T16:16:44.502+00:00",
        "name": "colour",
        "type": "red"
    }
]
```
</details>


## Task 2 - Assign an experiment to a user
Situation: Now that we have a service that allows us to create and list experiments lets create an endpoint to assign a customer to each experiment. To do this the front ends will
send us an id and we can return the customers id with the experiment they are assigned to.  

Requirements:
- When given a customer id we assign them to an experiment, store that link and return both the experiment and customer id 
- A customer can be assigned to only 1 experiment at a time. 
- On repeated calls with the same customer id we should retrieve the same experiment


<details>
<summary>Assign a customer example</summary>

Verb: **GET**

Endpoint:
```
localhost:8080/experiment/user/{id}
```

Response
```json
{
    "date": "2024-02-27T16:21:28.533+00:00",
    "output": [
        {
            "id": "32a82a81-5dba-434b-8ce2-7bda3343702d",
            "date": "2024-02-27T16:16:43.801+00:00",
            "name": "colour",
            "type": "brown"
        }
    ],
    "userId": "123"
}
```
</details>

## Task 3 - Delete an experiment
Situation: Now that we have the ability to create experiments and assign those to users we now want the ability to stop experiments. To do this we will need to the ability to delete an experiment. 

Requirements: 
- Be able to delete an experiment
- Remove the deleted experiment from users that currently have that experiment assigned

<details>
<summary>Delete an experiment example</summary>

Verb: **DELETE**

Endpoint:
```
localhost:8080/experiment/{id}
```

Response
```json
{
    "deleted": true,
    "removedFrom": 1,
    "id": "8fda77e3-f909-41e3-a6fc-63c25334de09"
}
```

</details>

