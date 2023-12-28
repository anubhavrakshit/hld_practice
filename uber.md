# A High Level Design of Uber

## Functional Requirements
1. Allow User to book a trip from her current location to another location.
2. Allow a Driver to get notification for nearby trip requests and select/reject a ride.
3. Show user a geographical map with nearby available cabs.
4. Show user a map with her current location while trip is in progress.

## Non Functional Requirements
1. Platform should be scalable.
2. Platform should be available, reliable, expandable and fault tolerant.
3. Platform should be fast and responsive.

## Back of envelope calculation
1. As the app is globally used we can expect a very large number of users and drivers.
2. Lets assume total number of users for app might be ~50Million.
3. Lets assume 10% are DAU. So we have 5Million DAU. Each user has some static data and
   her location. Lets assume per user data a 1KB. So total data is 50 Million * 1 KB = 50 TB.
4. For each active user the system will continously storing/updating Geographical position data. Lets say its around 100Bytes per second. So the plaform will need to continously store 100Bytes x 5 Million = 500MB/s of position data.

## Core Algorithm and data structure to use
1. The key challenge is to represent geo data in such a way that we can quickly search nearby drivers. Also figure out the shortest path between locations.
2. Lets say we have some location service that can ingest Cab locations and can be queried to find the nearby cabs.
3. Lets also assume we have Shortest Path calculator between locations. Maybe we can use Dijikstra's or A* algos in them.
