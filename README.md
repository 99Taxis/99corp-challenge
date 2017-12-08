# 99Pet

99 is the biggest brazilian ride-hailing app. You probably already know that. And it is growing very fast. <br/>
Since we're growing fast, we'd like a new feature in our app, the 99PET.<br/>
And how's that going to work? Well, it is very simple: we want pets to use our service as petssengers. (yes, we really enjoy creating new words)<br/>
According to IBGE (Brazilian Institute of Geography and Statistics), there are 52,2 million dogs and 22 million cats approximately in Brazil. <br/>
Yes, that's right: there are more pets than kids here in Brazil. I mean, we love kids here at 99, but, pets gives us less headaches, that's why we are betting on them. <br/>
So, now you're wondering who will develop this app? Well, I guess we need you to do it. And if you do a good job, we will (probably) want you in our team. ;)<br/>
Do not worry about interfaces nor front-end. We have the best capybara pet-software engineers working on UX, UI and also coding amazing JS (they seem to prefer React Native over Kotlin or Swift). All of them giving their best to create the an amazing experience for our 99PET users.

We expect nothing less from you, and that's why you must create the backend for this app.

So, a few demands:

- You can use any JVM language you want, but, we want you to apply functional concepts while developing this app.<br/> (hint: using Scala is a plus. ;))
- All of the data must be stored in a database of your choice. Expect us to ask why you took this decision.<br/>
- As we said, there are a lot of pets here in Brazil. We expect that one day all of them are going to be using our app. Knowing that, your app must be able to handle a high load of requests per second, so, choose what you will use very wisely.<br/>
- Your application need to be horizontally scalable.<br/>
- We are lazy and want a very detailed README.md explaining how to set the environment up to use your app. Hint: the simpler, the better.<br/>
- The source code should be in any git repository (e.g.: github, bitbucket, gitlab, you choose). If the repository is private, you need to grant access to your interviewers.<br/>
- Well-designed automated tests helps you to build a well-designed application.

I guess that's all you need to know before understanding what you will built.

Your backend app should expose via Restful the following domains:

- Driver<br/>
- Petssenger<br/>
- Ride

The driver won't have any kind of grade, so, you don't need to worry about it. It seems that pets don't know how to rate them very well. They seem to love everyone, so, it'd be pointless to create this feature.<br/>
The driver must have the following attributes: name, e-mail, car type and license plate.

The petseenger is very similar to the driver, I mean, besides being a pet and not a human, but, you already know that. The attributes that they must have are just: name and e-mail. (Yes, e-mail. You can't imagine how smart the pets can get these days...)

The app should allow the clients to create, fetch and update both driver and petseengers.

Also, we want to start rides, update ride status and notify the pet via e-mail when a ride is finished.

Pay attention for the following rules about rides:

- A ride must have a driver and a petseenger.<br/>
- Drivers and petseengers can only be in one ride at once.<br/>
- A ride must have three states: requested, in progress and finished.<br/>
- All the states have a "checkpoint", which is a GPS localization. (latitude/longitude)<br/>
- A ride can be at the "requested" state only once.<br/>
- A ride can be at the "finished" this state only once.<br/>
- The app will receive the checkpoint of a ride at regular intervals. When the first one happens, the ride must be updated to "in progress".<br/>
- The distance is calculated based on the travelled distance between the "start" checkpoint, the "in progress" checkpoints (all of them) and the final checkpoint.<br/>
- The price is calculated based on the distance.<br/>
- After the ride is finished, you app must e-mail the pet about the ride information.

To calculate the distance, the price and to send the e-mail, we will provide the endpoints for you, so, no worries about them.

Watch yourself while designing your Restful endpoints, otherwise the capybara pet-enginners are going to be very pissed. 

Okay, now, explaining how you're going to integrate with our three endpoints:

### How to send a e-mail:

```
POST /email HTTP/1.1
Host: pet.99app.com
Content-Type: application/json

{
  "petssenger_name": "Rufus",
  "petseenger_email": "rufus_big_dog@gmail.com",
  "driver_name": "Zé",
  "driver_email": "zezin@gmail.com",
  "distance": 2.35, //in km
  "price": 9.85
}
```

### How to calculate the distance:

```
POST /distance HTTP/1.1
Host: pet.99app.com
Content-Type: application/json

[
  {
    "checkpoint": "start",
    "lat": -23.550520,
    "lon": -46.633309 
  },
  {
    "checkpoint": "in_progress",
    "lat": -23.563210,
    "lon": -46.654250 
  },
  {
    "checkpoint": "in_progress",
    "lat": -23.574760,
    "lon": -46.648786 
  },
  {
    "checkpoint": "in_progress",
    "lat": -23.567266,
    "lon": -46.638920 
  },
  {
    "checkpoint": "end",
    "lat": -23.571869,
    "lon": -46.630472 
  }
]
```

You can pass only one start and checkpoints, but, several in_progress. 

The return will be:

```
{
  "distance": 5.34 //in km
}
```

### How to calculate the price:

```
GET /price?distance=5.0 HTTP/1.1
Host: pet.99app.com
```

The return will be:

```
{
  "price": 11.7
}
```

Ups, I almost forgot: we don't have these three endpoints yet, so, you should mock all the calls to simulate the behaviour of the three endpoints.

## Plus

If you want to, you can deploy your app somewhere provide the startup scripts in your repository. ;)

That's all you need to know. Well, good luck and if you have any questions, do not hesitate to ask us. 

See you!
