Deployed [Here](https://for-paws-transport.netlify.app)

# What is this project?
This project is to centralize transportation requests by shelters and rescues to transport dogs and cats. It allows a rescue or shelter to post a transportation request, where people can accept the request to transport the animal. It is designed to be both a web and phone app.

### Impact
Rescues and shelters typically have to rely on their personal network or word of mouth to get transportation requests filled. By creating a centralized place for all shelters and rescues to post, it allows them to expand their network and reach more people who will be able to help them complete their transport requests.

<br><br>

# Design Work
## Interview
I interviewed both people who run rescues and people who participate in the transportation process for this project. Everyone I interviews indicated that this work best as a phone app, which helped gear the design of the project to be for mobile.

I asked what the most important information that users need to be in the app.

Volunteers indicated that distance range and availability were the most important features for filtering the requests.

People also indicated that a messaging feature would be useful.

## Sketching
Sketches can be found [here](/sketches/)

<br><br>

# Implimentation
Svelte was used to create the base for this app and was hosted on Netlify.

## Styling
All icons used were taken from [Bootstrap Icons](https://icons.getbootstrap.com/).

Styling for text input boxes, popups, and overlays inspired by [w3schools](https://www.w3schools.com/css/default.asp).

All images from [Canva](https://www.canva.com/templates).

<br/><br/>

# Interface
This is where the user will see all of the open requests that match their profile/preferences.<br>
![alt text](/screenshots/homepage.png)

To see more details about a request, click on the request and a popup will open with more information about the request. If the user wants to accept the request, the will click "Accept Request".<br>
![alt text](/screenshots/more-info.png)

Here the user can see all of their accepted requests that they still have to complete. It will also populate with new requests accepted from the "Open Requests" page.<br>
![alt text](/screenshots/accepted-requests.png)

There is also the ability for the person making the transport request to tag a request with "Caution".<br>
![alt text](/screenshots/caution.png)

You can also communicate with the the person making the request in app.<br>
![alt text](/screenshots/messages.png)

This is the user profile. It allows the user to view and edit their information. The general info section allows the user to input things like their car type (to show how many animals they may be able to transport at one time) or their preferences (to account for allergies). The availability section allows the user to input when they would be able to accept requests, so it can tailor the requests to the user.<br>
![alt text](/screenshots/user.png)
![alt text](/screenshots/availability.png)

The user can click on the pencil icon to edit any of the user info or availability.<br>
![alt text](/screenshots/edit-user-info.png)
![alt text](/screenshots/edit-availability.png)

If the user edits any of their info, it will update in the user info section.<br>
![alt text](/screenshots/updated-user-info.png)

When the user edits their preferences and availability, it changes what transport requests the user is given.<br>
![alt text](/screenshots/more-open-requests.png)

<br><br>

# Future Work
Some features that I would impliment in the future would be to expand the app to allow people who do not have the means or ability to catch strays they see.

Another feature that I would impliment would be to expand it to transport other animals. In my research, I saw a lot of rescues that were also looking to transport farm animals to rescues. For now, the app only supports companian animals, but I would like to expand it to support other domestic animals as well.
