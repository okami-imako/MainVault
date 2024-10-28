In order to deploy to a subset of clusters do the following:

1) Click the "Replay" button in a job view in jenkins
2) Add the following entry to the config:

```json
deployProdConfig: [
	customClusterSequence: [
		"apps-us-central1-prod-02",
		"apps-us-central1-prod-03",
	]
],
```

>Note: 
>1) jenkins may not follow the order of clusters that you declared
>2) canary deploy will still happen