# teamseer-node-client

A simple Node client for the teamseer.com API.

## Api coverage

Only `getActiveUsers` and `getRecordsByUser` are implemented.

## Documentation

### Creating a client

	var teamseer = require('teamseer-node-client');

	var client = new teamseer.Client({
		companyId: '12345',
		companyKey: 'abc123fghi456',
		apiVersion: '1_0_1'
	}, new teamseer.adapters.Soap('https://www.teamseer.com/services/soap/coreapi/1_0_1/teamseer_core_api.wsdl'));


### `client.getRecordsByUser` Get records as array for one person

	/**
	 * Return all recorded days for a user within a given range
	 * @param {string} userIdentifier Typically the users email
	 * @param {string} fromDate The start date as YYYY-MM-DD
	 * @param {string} toDate The end date as YYYY-MM-DD
	 * @returns {Promise}
	 */
	client.getRecordsByUser('anna.miller@example.com', '2015-12-01', '2015-12-31').then(function(records) {
		console.log(records);
	});

	Example output:

	[ '2015-12-21',
	  '2015-12-22',
	  '2015-12-23',
	  '2015-12-24',
	  '2015-12-25',
	  '2015-12-26',
	  '2015-12-28',
	  '2015-12-29',
	  '2015-12-30',
	  '2015-12-31' ]


### `client.getRecordsByUser` Get a list of all active users

	/**
	 * Returns active users as an array
	 * @returns {Promise}
	 */
	client.getActiveUsers().then(function(records) {
		console.log(records);
	});

	Example output:

	[ 'anna.miller@example.com',
	  'clemens.doe@example.com',
	  'tanja.jackson@example.com',
	  'timo.foo@example.com',
	  'anne.bar@example.com',
	  'linda.baz@example.com' ]

## Full Example

	var teamseer = require('teamseer-node-client');

	var client = new teamseer.Client({
		companyId: '12345',
		companyKey: 'abc123fghi456',
		apiVersion: '1_0_1'
	}, new teamseer.adapters.Soap('https://www.teamseer.com/services/soap/coreapi/1_0_1/teamseer_core_api.wsdl'));

	client.getRecordsByUser('youremail@test.com', '2015-12-01', '2015-12-31').then(function(records) {
		console.log("success");
		console.log(records);
	}, function(err) {
		console.log("error");
		console.log(err);
	});

## Tests

In order to run the tests, make sure that the `.env` file within the root directory is set up correctly. (see
.env.example as reference)

## Note

Note: This project has been developed for personal needs and therefore has no demand to be feature-complete.
I used RxJs because I wanted to play with - it´ my first project with this library, so if I´m doing something stupid,
please let me know.