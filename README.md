# Insight Data Science Coding Challenge Solution
by Jiyoung Park on 7/11/16

## Introduction
I used Python 2.7 or 3.0 for this challenge, because it is great for getting things working quickly. It also helps that it is widely popular for data engineering / science industry.
I also used the Python graph library ```networkx``` to implement the graph data structure. It is best to use popular and proven libraries rather than reinventing the wheel.

## Requirements
* Python  		(Language of choice)
* networkx 		(external Python library, so you need to install by ```pip install networkx```)

## Discussion
I created a ```ProcessPayment``` class to parse input data, build graph, calculate median degree, and persist result to a file.

There is a check performed at the data parsing stage 
* ```check_input``` method handles rejection of bad/incorrectly formatted data. ```try/except``` clause is used to catch and ignores it.

	
Once the input data passes, it can be used to update the graph:
* ```process_payment``` method updates maximum running time and process payment if the payment is within the time window.
* ```prune_payments``` method visits every edge and deletes it if stale (fallen out of time window). It also removes any orphaned nodes as a result.
* ```get_median_degree``` method calculates the median degree by sorting all the degrees of the nodes and extracting the median.
	
The result is written sequentially in the output file by ```save_to_file``` method.

For massive scalability in practice, I would look into hosting a distributed graph database (e.g. Neo4j) in the cloud (AWS EC2). I thought this was beyond the scope of this assignment.

## Test cases
Here is a list of tests I have created in addition to the provided ```test-1-venmo-trans```:
* ```test-2-insight-readme-example``` tests the sample walkthrough in README.md
* ```test-3-invalid-inputs``` tests invalid input data (missing, incorrect/broken format, etc) in between first and last valid data.