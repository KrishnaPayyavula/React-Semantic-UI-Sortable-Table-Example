# React-Semantic-UI-Sortable-Table-Example
An example for React Semantic UI sortable table.

[![build status](https://img.shields.io/travis/gges5110/React-Semantic-UI-Sortable-Table-Example/master.svg)](https://travis-ci.org/gges5110/React-Semantic-UI-Sortable-Table-Example)
[![Coverage Status](https://coveralls.io/repos/github/gges5110/React-Semantic-UI-Sortable-Table-Example/badge.svg?branch=master&service=github)](https://coveralls.io/github/gges5110/React-Semantic-UI-Sortable-Table-Example?branch=master)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/a5f2bc2a9a8944549c95a17de5d863e9)](https://www.codacy.com/app/gges5110/React-Semantic-UI-Sortable-Table-Example?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=gges5110/React-Semantic-UI-Sortable-Table-Example&amp;utm_campaign=Badge_Grade)

## Prerequisite
Node.js runtime environment.

## Quick Start
```bash
# Install dependencies
npm ci

# Start JSON Server at port 3000.
npm start

# Compile and watch changes to React component. This will open localhost:8000
npm run build:watch
```

## All Available Custom Script
```bash
npm run
```

## Compile for Production
To compile the React component in production mode, type
```
npm run build
```
This command will build app.bundle.js, vendor.bundle.js and their corresponding source maps.
I compile it separately into two files, app.bundle.js is for our react front end code and vendor.bundle.js is for the other front end libraries. Find out more in the ```webpack.config.js```.

## Deployment
I deploy the application with docker, and is configured by `now.json`

## Docker
```bash
# Build the image
docker build -t {SOME_TAG} .
# Run the container with exposing port 5000
docker run -p 5000:3000 {SOME_TAG}
```


## Server APIs

| Operation         | HTTP Method   | Example           | Remarks       |
| ----------------- | ------------- | ----------------- | ------------- |
| Get Vehicle List  | Get           | /api/v1/vehicles?q=&_page=0&_limit=10&_order=asc&_sort=package  | Available query params: q, _offset, _limit, _order, _sort. |
| Toggle Favorite   | Put           | /api/v1/vehicles/:id | Requires to send the JSON formatted vehicle in the body.  |

## Sorting data on front-end v.s. back-end
Depending on the data set size and the connectivity, we can sort the vehicle data either on front-end or the back-end. When the data set size is small it is easier to send the whole data set to the client size and do all the sorting and filtering in the browser. But this will not scale well as the data size grows, especially it could have millons of rows. To limit the data being sent over to the front-end, I only allow 100 records per request.

## Input Validation
Each time a character changes in filter input, it will check two things. 1) If the input contains invalid character, and 2) there is no result being found after applying the filter. For the first case, the input UI will turn red and a popup will show a message warning the user. If the filter will cause the result to be empty, the popup will inform the user about this. On the server side, it will also check if the input only contains alphanumerics, and will send a 422 response along with an error message.
