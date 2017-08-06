# New York Times Article API: Dataloader

## Requirements

- It is assumed you have **Python 2.7** installed on your machine

## Install
- Unzip the directory and then go into the directory:

## Get Api Key

- Get yourself an api key from the New York Times API
[link for getting an api key](https://developer.nytimes.com/signup)

## Usage

- Start dataloader with the following command:
```
python2 nytbatches.py 5 <your-api-key> -b 20170414 -e 20170415 -q Facebook
```

### Required arguments:
- the **number of batches**, you request (one batch consists of 10 articles)
- **your api key**

### Optional arguments
- date **-b** egin search
- date **-e** nd search
- **-q** ueryterm

## Result

### Batches
- You will receive the requested number of batches
- Or as many batches as needed to serve
all hits from your query.

### Where are the Articles?

- On screen only headers and ids are displayed.

- You find the complete flattend articles in the batch-files in the `json` directory

- The result of the query above would be stored in files with the following names:
```
facebook_20170414_20170415.0.json
facebook_20170414_20170415.1.json
...
```
- Each batch contains 10 or less articles

## Flattend Structure of Articles
- the programm `makeflat.py` flattens the articles or any structure
of python dictionaries and lists recursively

- nested dictionaries are turned into a flat dictonary with a combined key:
```
{'headline': {'main': 'some headline', 'kicker': 'some excitement'}}
```
is turned into:
```
{'headline.main': 'some headline',
'headline.kicker': 'some excitement'}
```
- lists item keys are derived by numbering:
```
{'keywords': [{'value': 'US', rank': 1}, {'value': 'Soccer', rank': 2}]}
```
is turned into:
```
{'keywords.0.value': 'US',
 'keywords.0.rank': 1,
 'keywords.1.value': 'Soccer',
 'keywords.1.rank': 2}
```

## Testing
- `makeflat.py` is tested
you may try the tests with `python2 -m unittest discover`

- The dataloader does not have tests yet.
