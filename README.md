# Dice Vue Game
A simple dice game built with Vue.js.

### Prerequisites
Node.js v14 or later
Installation
Clone the repository:

```
git clone https://github.com/mastashake08/dice-vue-game.git
```
Change into the project directory:

```
cd dice-vue-game
```
Install the dependencies:

```
npm install
```
Usage
To run the application in development mode:

```
npm run serve
```
This will start a development server at http://localhost:8080, where you 
can access the application in your web browser.

To build the application for production:

```
npm run build
```
This will create a dist directory containing the built files that can be 
deployed to a web server.

Docker
You can also run the application using Docker. First, build the Docker 
image:

```
docker build -t dice-vue-game .
Then, start a Docker container:
```

```
docker run -p 8080:8080 dice-vue-game
This will start a Docker container running the application at 
http://localhost:8080.
```
License
This project is licensed under the MIT License. See the LICENSE file for 
details.
