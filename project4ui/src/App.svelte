<script>
  import logo from "./assets/logo.png";
  import Footer from "./lib/Footer.svelte";
  import Header from "./lib/Header.svelte";

  let user = $state({
    car: "Crossover",
    availability: {
      Monday: { start: "17:00", end: "20:00" },
      Tuesday: { start: "17:00", end: "20:00" },
      Wednesday: { start: "12:00", end: "21:00" },
      Thursday: { start: "09:00", end: "12:00" },
      Friday: { start: "09:00", end: "17:00" },
      Saturday: { start: "", end: "" },
      Sunday: { start: "", end: "" },
    },
    catCarrier: 1,
    dogCarrier: 0,
    comp: "false",
    maxDistance: 150,
    preference: "None",
  });

  let requests = $state({
    requests: [
      {
        id: 1,
        comp: "true",
        pickupDay: "Wednesday",
        pickupTime: "17:00",
        danger: "false",
        description:
          "Two adult cats being transported from Columbus shelter to rescue in Cincinnati. Must be picked up before end of day Wednesday.",
        pickupCity: "Hillard, Ohio",
        distance: 116,
        pickupLocation: "Columbus Humane",
        dropoffCity: "Cincinnati, Ohio",
        dropoffLocation: "Furry Friends Rescue",
        numberOfCats: 2,
        numberOfDogs: 0,
        carriersProvided: "true",
        accepted: "false",
      },
      {
        id: 2,
        comp: "true",
        pickupDay: "Tuesday",
        pickupTime: "20:00",
        danger: "false",
        description:
          "One dog being transported from a shelter in Georgia to Lexington needs to transport from Lexington up to Florence",
        pickupCity: "Lexington, Kentucky",
        distance: 82,
        pickupLocation: "TBD",
        dropoffCity: "Florence, Kentucky",
        dropoffLocation: "Second Chance Rescue",
        numberOfCats: 0,
        numberOfDogs: 1,
        carriersProvided: "true",
        accepted: "false",
      },
      {
        id: 3,
        comp: "true",
        pickupDay: "Friday",
        pickupTime: "13:00",
        danger: "true",
        description:
          "Five puppies need transport house from Peebles, Ohio to Cincinnati, Ohio. Caution is advised",
        pickupCity: "Peebles, Ohio",
        distance: 68,
        pickupLocation: "TBD",
        dropoffCity: "Florence, Kentucky",
        dropoffLocation: "Second Chance Rescue",
        numberOfCats: 0,
        numberOfDogs: 5,
        carriersProvided: "true",
        accepted: "true",
      },
      {
        id: 4,
        comp: "true",
        pickupDay: "Monday",
        pickupTime: "14:00",
        danger: "false",
        description:
          "Senior dog heading from Indianapolis to Cincinnati for foster placement.",
        pickupCity: "Indianapolis, Indiana",
        distance: 113,
        pickupLocation: "IndyHumane",
        dropoffCity: "Cincinnati, Ohio",
        dropoffLocation: "Furry Friends Rescue",
        numberOfCats: 0,
        numberOfDogs: 1,
        carriersProvided: "false",
        accepted: "false",
      },
      {
  id: 5,
  comp: "true",
  pickupDay: "Wednesday",
  pickupTime: "09:00",
  danger: "false",
  description: "Four kittens being moved from Florence to Louisville for foster home placement.",
  pickupCity: "Covington, Kentucky",
  distance: 100,
  pickupLocation: "Kenton County Animal Services",
  dropoffCity: "Louisville, Kentucky",
  dropoffLocation: "Save Haven Rescue",
  numberOfCats: 4,
  numberOfDogs: 0,
  carriersProvided: "true",
  accepted: "false"
},
{
  id: 6,
  comp: "true",
  pickupDay: "Friday",
  pickupTime: "17:00",
  danger: "false",
  description: "A bonded pair of dogs relocating from Cincinnati to Indianapolis",
  pickupCity: "Cincinnati, Ohio",
  distance: 150,
  pickupLocation: "Cincinnati Animal CARE",
  dropoffCity: "Indianapolis, Indiana",
  dropoffLocation: "",
  numberOfCats: 0,
  numberOfDogs: 2,
  carriersProvided: "false",
  accepted: "false"
},
{
  id: 7,
  comp: "true",
  pickupDay: "Thursday",
  pickupTime: "17:00",
  danger: "false",
  description: "A mother cat and her five kittens being transported from Dayton shelter to Cincinnati.",
  pickupCity: "Dayton, Ohio",
  distance: 109,
  pickupLocation: "Humane Society Of Greater Dayton Adoption Center",
  dropoffCity: "Cincinnati, Ohio",
  dropoffLocation: "The Scratching Post",
  numberOfCats: 6,
  numberOfDogs: 0,
  carriersProvided: "false",
  accepted: "false"
},
{
  id: 8,
  comp: "true",
  pickupDay: "Monday",
  pickupTime: "08:00",
  danger: "false",
  description: "One small dog being transported from Cincinnati to Dayton.",
  pickupCity: "Cincinnati, Ohio",
  distance: 54,
  pickupLocation: "Cincinnati Animal CARE",
  dropoffCity: "Dayton, Ohio",
  dropoffLocation: "Wonder Dogs Rescue",
  numberOfCats: 0,
  numberOfDogs: 1,
  carriersProvided: "true",
  accepted: "false"
}
    ],
  });
  let sortedRequests = $state([{
    id: -1,
    comp: "",
    pickupDay: "",
    pickupTime: "",
    danger: "",
    description: "",
    pickupCity: "",
    distance: 0,
    pickupLocation: "",
    dropoffCity: "",
    dropoffLocation: "",
    numberOfCats: 0,
    numberOfDogs: 0,
    carriersProvided: "",
    accepted: "",
  }])

  let currPage = $state("main");
  let isHidden = $state(true);
  let isOverlayHidden = $state(true);
  let isHiddenMain = $state(true);
  let editOption = $state("");
  let moreInfoRequest = $state({
    id: -1,
    comp: "",
    pickupDay: "",
    pickupTime: "",
    danger: "",
    description: "",
    pickupCity: "",
    distance: 0,
    pickupLocation: "",
    dropoffCity: "",
    dropoffLocation: "",
    numberOfCats: 0,
    numberOfDogs: 0,
    carriersProvided: "",
    accepted: "",
  });
  let completedRequests = $state(32)

  let tempCar = $state(user.car);
  let tempCatCarrier = $state(user.catCarrier);
  let tempDogCarrier = $state(user.dogCarrier);
  let tempEditDay = $state("");
  let tempAvailability = $state({
    Monday: {
      start: user.availability.Monday.start,
      end: user.availability.Monday.end,
    },
    Tuesday: {
      start: user.availability.Tuesday.start,
      end: user.availability.Tuesday.end,
    },
    Wednesday: {
      start: user.availability.Wednesday.start,
      end: user.availability.Wednesday.end,
    },
    Thursday: {
      start: user.availability.Thursday.start,
      end: user.availability.Thursday.end,
    },
    Friday: {
      start: user.availability.Friday.start,
      end: user.availability.Friday.end,
    },
    Saturday: {
      start: user.availability.Saturday.start,
      end: user.availability.Saturday.end,
    },
    Sunday: {
      start: user.availability.Sunday.start,
      end: user.availability.Sunday.end,
    },
  });
  let tempComp = $state(user.comp);
  let tempDistance = $state(user.maxDistance);
  let tempPreference = $state(user.preference);

  const carTypes = [
    "2-Door Sedan",
    "4-Door Sedan",
    "Crossover",
    "SUV",
    "Minivan",
    "Truck",
    "Van",
    "Other",
  ];

  let days = $state([
    "Monday",
    "Tuesday",
    "Wednesday",
    "Thursday",
    "Friday",
    "Saturday",
    "Sunday",
  ]);

  let dayOrder = {
  'Sunday': 0,
  'Monday': 1,
  'Tuesday': 2,
  'Wednesday': 3,
  'Thursday': 4,
  'Friday': 5,
  'Saturday': 6
};

  function updateUser() {
    switch (editOption) {
      case "editCar":
        user.car = tempCar;
        break;

      case "editCatCarrier":
        user.catCarrier = tempCatCarrier;
        break;

      case "editDogCarrier":
        user.dogCarrier = tempDogCarrier;
        break;

      case "editAvailability":
        user = {
          ...user,
          availability: {
            ...user.availability,
            [tempEditDay]: {
              start: tempAvailability[tempEditDay].start,
              end: tempAvailability[tempEditDay].end,
            },
          },
        };
        days = days;
        tempEditDay = "";
        break;

      case "editComp":
        user.comp = tempComp;
        break;

      case "editDistance":
        user.maxDistance = tempDistance;
        break;

      case "editPreference":
        user.preference = tempPreference;
        break;

      default:
        break;
    }

    user = user;
    editOption = "";
    isHidden = true;
    isOverlayHidden = true;
  }

  function closePopup() {
    tempCar = user.car;
    tempCatCarrier = user.catCarrier;
    tempDogCarrier = user.dogCarrier;
    if (tempEditDay) {
      tempAvailability[tempEditDay].start =
        user.availability[tempEditDay].start;
      tempAvailability[tempEditDay].end = user.availability[tempEditDay].end;
    }
    tempComp = user.comp;
    tempDistance = user.maxDistance;
    tempPreference = user.preference;

    isHidden = true;
    isOverlayHidden = true;
  }

  function requestsForUser() {
    let r = [{
      id: -1,
    comp: "",
    pickupDay: "",
    pickupTime: "",
    danger: "",
    description: "",
    pickupCity: "",
    distance: 0,
    pickupLocation: "",
    dropoffCity: "",
    dropoffLocation: "",
    numberOfCats: 0,
    numberOfDogs: 0,
    carriersProvided: "",
    accepted: "",
  }];
    for (let i = 0; i < requests.requests.length; i++) {

      //handling user comp preference
      if (user.comp == "true" && requests.requests[i].comp == "false") {
        console.log("test1")
        continue;
      }

      //handling user distance
      if(user.maxDistance < requests.requests[i].distance){
        console.log("test2")
        continue;
      }

      //handling user availability
      if((user.availability[requests.requests[i].pickupDay].start > requests.requests[i].pickupTime) || (user.availability[requests.requests[i].pickupDay].end < requests.requests[i].pickupTime)) {
        console.log("test3")
        continue;
      }

      //handling user species preference
      if (user.preference != "None") {
        if (
          requests.requests[i].numberOfCats != 0 &&
          user.preference === "Dogs"
        ) {
          console.log("test4")
          continue;
        }
        if (
          requests.requests[i].numberOfDogs != 0 &&
          user.preference === "Cats"
        ) {
          console.log("test5")
          continue;
        }
      }

      if(r[0].id === -1){
        r[0] = requests.requests[i]
      } else {
        r.push(requests.requests[i])
      }
    }
    sortedRequests = r
    sortedRequests.sort((a, b) => dayOrder[a.pickupDay] - dayOrder[b.pickupDay])
  }
  requestsForUser()

  function userAcceptRequest(){
          for(let i = 0; i < requests.requests.length; i++){
            if(requests.requests[i].id === moreInfoRequest.id){
              requests.requests[i].accepted = "true"
            }
          }
          requestsForUser()
          isHiddenMain = true
          isOverlayHidden = true
  }

  function userCompletedRequest(){
              for(let i = 0; i < requests.requests.length; i++){
            if(requests.requests[i].id === moreInfoRequest.id){
              requests.requests[i].accepted = "completed"
            }
          }
          completedRequests++
          requests = requests
          sortRequestsByDay()
          isHiddenMain = true
          isOverlayHidden = true
  }

  function sortRequestsByDay(){
    requests.requests.sort((a, b) => dayOrder[a.pickupDay] - dayOrder[b.pickupDay])
    console.log(requests)
  }
  sortRequestsByDay()

  function convertTo12Hr(x){
    const timeString12hr = new Date('1970-01-01T' + x + 'Z')
  .toLocaleTimeString('en-US',
    {timeZone:'UTC',hour12:true,hour:'numeric',minute:'numeric'}
  );
  return timeString12hr
  }

  console.log("12:00" >= "12:00")
</script>

<main>
  <Header />

  <div class="overlay" hidden={isOverlayHidden}></div>
  <div hidden={isHiddenMain} class="popup" style="max-width: 450px; padding-left: 20px; padding-right: 20px">
    <div style="position: relative">
      <div style="position: absolute; top: 20px; right: 0px;">
        <button
          onclick={() => {
            isOverlayHidden = true;
            isHiddenMain = true;
          }}
          class="transparent-btn"
        >
          <i style="font-size: 20px" class="bi bi-x-lg"></i>
        </button>
      </div>

      <div
        style="padding-top: 60px; padding-bottom: 40px; padding-left: 10px; padding-right: 10px"
      >
        <h4>{moreInfoRequest.description}</h4>
        <br />
        {#if moreInfoRequest.danger === "true"}
          <div
            style="border: 2px solid darkred; color: darkred; background-color: lightpink; padding-top: 5px; padding-bottom: 5px; padding-left: 10px; padding-right: 10px; border-radius: 20px; width: fit-content"
          >
            <p><b>Caution</b></p>
          </div>
        {/if}
        <br />
        <h4>Pickup Information:</h4>
        <div style="margin-left: 10px; margin-right: 10px">
          <div>
            <p>
              Time: {moreInfoRequest.pickupDay} at {convertTo12Hr(moreInfoRequest.pickupTime)}
            </p>
          </div>
          <div>
            <p>
              Location: {moreInfoRequest.pickupLocation} in {moreInfoRequest.pickupCity}
            </p>
          </div>
        </div>
        <br />

        <h4>Dropoff Information:</h4>
        <div>
          <div style="margin-left: 10px; margin-right: 10px">
            <div>
              <p>
                Location: {moreInfoRequest.dropoffLocation} in {moreInfoRequest.dropoffCity}
              </p>
            </div>
          </div>
        </div>
        <br />

        {#if moreInfoRequest.comp === "true"}
          <p><b>Gas Money Provided?:&nbsp;</b>Yes</p>
        {:else}
          <p><b>Gas Money Provided?:&nbsp;</b>No</p>
        {/if}

        <div style="text-align: center">
        {#if currPage === "main"}
        <button class="accept-complete-btn" onclick={() => {
          userAcceptRequest()
        }}>Accept Transport Request</button>
        {:else}
        <button  class="accept-complete-btn" onclick={() => {
          userCompletedRequest()
        }}>Complete Request</button>
        {/if}
</div>

      </div>
    </div>
  </div>

  <div
    style="position:absolute; top:75px; bottom:74px; left:0px; right:0px; overflow:auto; background-color: #C0D6DF"
  >
    {#if currPage === "main"}
      <div style="display: flex; flex-direction: column; align-items: center;">
        <div>
          <h1>Open Requests</h1>
        </div>
        {#each sortedRequests as request}
        {#if request.accepted === "false"}
          <button
            class="transparent-btn"
            style="text-align: left"
            onclick={() => {
              moreInfoRequest = request;
              isOverlayHidden = false;
              isHiddenMain = false;
            }}
          >
            <div
              style="background-color: white; width: calc(100vw - 40px); max-width: 500px;; margin-top: 20px; padding: 20px"
            >
              <div style="padding-bottom: 10px">
                {#if request.numberOfDogs}
                  <h1>Dogs: {request.numberOfDogs}</h1>
                {/if}
                {#if request.numberOfCats}
                  <h1>Cats: {request.numberOfCats}</h1>
                {/if}
              </div>

              <div>
                {#if request.pickupTime >= "12:00"}
                <p style="font-size: 20px; padding-bottom: 10px">{request.pickupDay} at {convertTo12Hr(request.pickupTime)}</p>
                {:else}
                <p style="font-size: 20px">{request.pickupDay} at {request.pickupTime}&nbsp;AM</p>
                {/if}
              </div>
              <div style="display: flex; flex-wrap: wrap;">
                <div style="width: 50%">
                <p style="font-size: 16px">From:</p>
                  <p style="font-size: 16px">&nbsp;&nbsp;{request.pickupCity}</p>
                </div>
                <div style="width: 50%">
                <p style="font-size: 16px">To:</p>
                  <p style="font-size: 16px">&nbsp;&nbsp;{request.dropoffCity}</p>
                </div>
              </div>
            </div>
          </button>
          {/if}
        {/each}
        <img src={logo} style="width: 300px" />
      </div>
    {:else if currPage === "user"}
      <div class="overlay" hidden={isOverlayHidden}></div>
      <div hidden={isHidden} class="popup">
        <div style="position: relative">
          <div style="position: absolute; top: 20px; right: 20px;">
            <button onclick={closePopup} class="transparent-btn">
              <i style="font-size: 20px" class="bi bi-x-lg"></i>
            </button>
          </div>

          <div
            style="display: flex; flex-direction: column; align-items: center; padding-top: 50px;
          padding-bottom: 40px"
          >
            {#if editOption === "editCar"}
              <h3>Edit Car Type:</h3>
              <select
                name="car"
                id="car"
                bind:value={tempCar}
                style="font-size: 20px; margin-top: 20px; width: 300px; padding-top: 10px; padding-bottom: 10px"
              >
                {#each carTypes as cars}
                  <option value={cars}>{cars}</option>
                {/each}
              </select>
            {:else if editOption === "editCatCarrier"}
              <h3>Edit Number of Cat Carriers:</h3>
              <input
                type="number"
                bind:value={tempCatCarrier}
                style="font-size: 20px; margin-top: 20px; width: 300px; padding-top: 10px; padding-bottom: 10px"
              />
            {:else if editOption === "editDogCarrier"}
              <h3>Edit Number of Dog Carriers:</h3>
              <input
                type="number"
                bind:value={tempDogCarrier}
                style="font-size: 20px; margin-top: 20px; width: 300px; padding-top: 10px; padding-bottom: 10px"
              />
            {:else if editOption === "editAvailability"}
              <h3>Edit {tempEditDay}'s Availability:</h3>
              <div
                style="display: flex; justify-content: space-between; align-items: center; padding-top: 10px;"
              >
                <input
                  bind:value={tempAvailability[tempEditDay].start}
                  type="time"
                  name="{tempEditDay}Start"
                />&nbsp;to&nbsp;
                <input
                  bind:value={tempAvailability[tempEditDay].end}
                  type="time"
                  name="{tempEditDay}End"
                />
              </div>
            {:else if editOption === "editComp"}
              <h3>Do you require gas money?:</h3>
              <select
                name="comp"
                id="comp"
                bind:value={tempComp}
                style="font-size: 20px; margin-top: 20px; width: 300px; padding-top: 10px; padding-bottom: 10px"
              >
                <option value="true">Yes</option>
                <option value="false">No</option>
              </select>
            {:else if editOption === "editDistance"}
              <h3>Edit Max Distance (miles):</h3>
              <input
                type="number"
                bind:value={tempDistance}
                style="font-size: 20px; margin-top: 20px; width: 300px; padding-top: 10px; padding-bottom: 10px"
              />
            {:else if editOption === "editPreference"}
              <h3>Do you have a species preference?:</h3>
              <select
                name="pref"
                id="pref"
                bind:value={tempPreference}
                style="font-size: 20px; margin-top: 20px; width: 300px; padding-top: 10px; padding-bottom: 10px"
              >
                <option value="Cats">Cats</option>
                <option value="Dogs">Dogs</option>
                <option value="None">No Preference</option>
              </select>
            {/if}

            <button
              style="padding: 10px; width: 150px; margin-top: 20px; border-radius: 20px; border: none; font-weight: bold; color: white; background-color: #4A6FA5"
              onclick={updateUser}>Update</button
            >
          </div>
        </div>
      </div>

      <div>
        <div
          style="display: flex; flex-direction: column; align-items: center;"
        >
          <div style="text-align:center; padding-top: 75px">
            <i style="font-size: 75px" class="bi bi-person-circle"></i>
            <h1>User</h1>
            <h3>Completed Transport Requests:&nbsp;{completedRequests}</h3>
          </div>
          <br /><br />

          <!-- edit car -->
           <div style="background-color: white;  width: calc(100vw - 40px); max-width: 500px; margin-bottom: 30px; padding-bottom: 10px">
            <h2 class="user-titles">General Info</h2>
          <div
            style="display: grid; grid-template-columns: 5fr 1fr"
          >
            <div>
              <p
                class="user-gen-info"
              >
                <b>Car Type:&nbsp;</b>{user.car}
              </p>
            </div>

            <div
              style="display: flex; justify-content: center; align-items: center"
            >
              <button
                class="transparent-btn"
                onclick={() => {
                  isHidden = false;
                  isOverlayHidden = false;
                  editOption = "editCar";
                }}
              >
                <i style="font-size: 20px" class="bi bi-pencil-square"></i>
              </button>
            </div>

            <!-- edit cat carrier -->
            <div>
              <p
                class="user-gen-info"
              >
                <b>Number of Cat Carriers:&nbsp;</b>{user.catCarrier}
              </p>
            </div>

            <div
              style="display: flex; justify-content: center; align-items: center"
            >
              <button
                class="transparent-btn"
                onclick={() => {
                  isHidden = false;
                  isOverlayHidden = false;
                  editOption = "editCatCarrier";
                }}
              >
                <i style="font-size: 20px" class="bi bi-pencil-square"></i>
              </button>

              <!-- edit dog carrier -->
            </div>
            <div>
              <p
                class="user-gen-info"
              >
                <b>Number of Dog Carriers:&nbsp</b>{user.dogCarrier}
              </p>
            </div>

            <div
              style="display: flex; justify-content: center; align-items: center"
            >
              <button
                class="transparent-btn"
                onclick={() => {
                  isHidden = false;
                  isOverlayHidden = false;
                  editOption = "editDogCarrier";
                }}
              >
                <i style="font-size: 20px" class="bi bi-pencil-square"></i>
              </button>
            </div>

            <!-- edit preference -->
            <div>
              <p
                class="user-gen-info"
              >
                <b>Species Preference:&nbsp</b>{user.preference}
              </p>
            </div>

            <div
              style="display: flex; justify-content: center; align-items: center"
            >
              <button
                class="transparent-btn"
                onclick={() => {
                  isHidden = false;
                  isOverlayHidden = false;
                  editOption = "editPreference";
                }}
              >
                <i style="font-size: 20px" class="bi bi-pencil-square"></i>
              </button>
            </div>

            <!-- edit distance -->
            <div>
              <p
                class="user-gen-info"
              >
                <b>Max Distance:&nbsp</b>{user.maxDistance} miles
              </p>
            </div>

            <div
              style="display: flex; justify-content: center; align-items: center"
            >
              <button
                class="transparent-btn"
                onclick={() => {
                  isHidden = false;
                  isOverlayHidden = false;
                  editOption = "editDistance";
                }}
              >
                <i style="font-size: 20px" class="bi bi-pencil-square"></i>
              </button>
            </div>

            <!-- edit comp -->
            <div>
              <p
                class="user-gen-info"
              >
                <b>Do you need gas money?:&nbsp;</b>{#if user.comp === "true"}
                  Yes
                {:else}
                  No
                {/if}
              </p>
            </div>

            <div
              style="display: flex; justify-content: center; align-items: center"
            >
              <button
                class="transparent-btn"
                onclick={() => {
                  isHidden = false;
                  isOverlayHidden = false;
                  editOption = "editComp";
                }}
              >
                <i style="font-size: 20px" class="bi bi-pencil-square"></i>
              </button>
            </div>
          </div>
</div>

          <!-- edit availability -->
           <div style="background-color: white;  width: calc(100vw - 40px); max-width: 500px; margin-bottom: 40px; padding-bottom: 10px">
            <h2 class="user-titles">Availability</h2>
          <div
            style="display: grid; grid-template-columns: 5fr 1fr"
          >
            {#each days as day}
              <div>
                <p
                  style="padding-top: 10px; padding-bottom: 10px; padding-left: 30px; font-size: 20px"
                >
                  {#if user.availability[day].start && user.availability[day].end}
                    {day}: {convertTo12Hr(user.availability[day].start)} - {convertTo12Hr(user.availability[day].end)}
                  {:else}
                    {day}: Unavailable
                  {/if}
                </p>
              </div>
              <div
                style="display: flex; justify-content: center; align-items: center"
              >
                <button
                  class="transparent-btn"
                  onclick={() => {
                    isHidden = false;
                    isOverlayHidden = false;
                    editOption = "editAvailability";
                    tempEditDay = day;
                  }}
                >
                  <i style="font-size: 20px" class="bi bi-pencil-square"></i>
                </button>
              </div>
            {/each}
          </div>
</div>

        </div>
      </div>
    {:else if currPage === "requests"}
            <div style="display: flex; flex-direction: column; align-items: center;">
              <div>
                <h1>Accepted Requests</h1>
              </div>
        {#each sortedRequests as request}
        {#if request.accepted === "true"}
          <button
            class="transparent-btn"
            style="text-align: left"
            onclick={() => {
              moreInfoRequest = request;
              isOverlayHidden = false;
              isHiddenMain = false;
            }}
          >
            <div
              style="background-color: white; width: calc(100vw - 40px); max-width: 500px;; margin-top: 20px; padding: 20px"
            >
              <div style="padding-bottom: 10px">
                {#if request.numberOfDogs}
                  <h1>Dogs: {request.numberOfDogs}</h1>
                {/if}
                {#if request.numberOfCats}
                  <h1>Cats: {request.numberOfCats}</h1>
                {/if}
              </div>
              <div style="padding-bottom: 10px">
                {#if request.pickupTime > "12:59"}
                <p style="font-size: 20px;">{request.pickupDay} at {convertTo12Hr(request.pickupTime)}</p>
                {:else}
                <p style="font-size: 20px">{request.pickupDay} at {request.pickupTime}&nbsp;AM</p>
                {/if}
              </div>
              <div style="display: flex; flex-wrap: wrap;">
                <div style="width: 50%">
                <p style="font-size: 16px">From:</p>
                  <p style="font-size: 16px">&nbsp;&nbsp;{request.pickupCity}</p>
                </div>
                <div style="width: 50%">
                <p style="font-size: 16px">To:</p>
                  <p style="font-size: 16px">&nbsp;&nbsp;{request.dropoffCity}</p>
                </div>
              </div>
            </div>
          </button>
          {/if}
        {/each}
      </div>


      {:else if currPage === "messages"}
      <div style="display: flex; flex-direction: column; align-items: center;">
        <div style="width: calc(100vw - 40px); max-width: 500px; height: calc(100vh - 190px); margin-top: 20px; padding: 20px; background-color: white">
          <h1 style="text-align: center; margin-bottom: 20px">Messages</h1>

          {#each requests.requests as request}
          {#if request.accepted === "true"}
          <div style="border-bottom: 1px solid black; height: 75px; display: grid; grid-template-columns: 5fr 1fr">


              <div style="display: flex; align-items: center; height 75px">
                <p style="font-size: 20px; margin-left: 20px">{request.dropoffLocation}</p>
              </div>

              {#if request.id === 3}
          <div style="display: flex; justify-content: center; align-items: center">
                <svg height="20" width="20" xmlns="http://www.w3.org/2000/svg">
  <circle r="7" cx="10" cy="10" fill="#166088" />
</svg>
                </div>

                {/if}




          </div>

          {/if}
          {/each}

        </div>
      </div>


      {/if}
  </div>

  <Footer bind:currPage {requestsForUser}/>
</main>

<style>
  @import "./app.css";
</style>
