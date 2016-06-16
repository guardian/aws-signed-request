# Signed AWS requests

Module to send signed requests to an AWS service.

Heavily inspired by [aws samples](https://github.com/awslabs/amazon-elasticsearch-lambda-samples).

## Install

```
npm install --save aws-signed-request
```

## Usage

### ElasticSearch

```js
var elastic = require('aws-signed-request')({
	endpoint: 'htps://your.elasticsearch.es.amazon.com',
	region: 'eu-west-1',
	service: 'es'
});

elastic.send({
	method: 'GET',
	path: '/domain/index/id'
}, function (err, data) {
	console.log(data);
});
```

### API Gateway

```js
var gateway = require('aws-signed-request')({
	endpoint: 'https://your.api.gateway.amazon.com',
	region: 'eu-west-1',
	service: 'execute-api'
});

gateway.send({
	method: 'POST',
	path: '/action',
	message: {
		json
	}
}, function (err, data) {
	console.log(data);
});
```


### Advanced usage

By default the module expects a JSON response. If you're expecting plain text you can call

```js
elastic.send({
	method: 'GET',
	path: '/_cat/indices',
	json: false
}, function (err, data) {
	console.log(data); // as plain text
});
```

If `json:true` and the response is not a valid JSON, the callback receives an error containing `responseText` for debug purposes.

## Contribute

Clone the repo, write some test, make them pass and pull request your changes.

You can watch your tests by running

```js
npm install -g watch
watch "npm test" . -d
```
