# cppweb

## Using Docker

```
# create docker container
docker build -t cppbox .

# use a volume with the container
docker run -v <host directory>:<container directory> -ti <image> bash

# run container and map ports
docker run -v <host directory>:<container directory> -p <host port>:<container port> -e PORT=8081 <image> <app to run>
```
To run our server from a Docker container and access it from the host, we need to open a port, by defalut they're closed. For that we use `-p` to open a port and map it to the host machine and `-e` to create an environmental variable, we use it to tell the server  which port it should use.

## Databases
* Use MongoDB Atlas.
  * Create a Cluster. Note that the name cannot be changed later.
  * Setup which IPs can access the cluster (for this example all of them)
  * Configure an user and a password. Provide `Atlas Admin` privileges.
  * Connect to the cluster using `mongodb shell`. Follow instructions in Atlas site.

* Install mongodb in your host machine.
```
brew update
brew install mongodb
# this may also be required for mongoimport
brew install mongodb/brew/mongodb-database-tools
```

* You can import a JSON to your database in MongoDB Atlas.

I couldn't make the `mongoimport --host` command work, and the uri version was not working either. To make this work I created the collection and the database maually using the Atlas interface. Then, I needed the uri, I found it on the `connection` section of the cluster. I noticed that the string for the host was different from the uri because the uri one needed to have my user and password embedded on the string. After that this command worked.

```
mongoimport --uri "mongodb+srv://<user>:<password>@<cluster>/<database>"  -c <collection> --drop --file <file>.json --jsonArray
```

## Resources
* [MongoDB Atlas mongoimport issues cannot decode array into a D](https://stackoverflow.com/questions/58150528/mongodb-atlas-mongoimport-issues-cannot-decode-array-into-a-d)
* [Load File with mongoimport](https://docs.atlas.mongodb.com/import/mongoimport)