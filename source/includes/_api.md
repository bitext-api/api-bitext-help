# API Rest

The Bitext API can be reached by using the following 4 endpoints:

> If your personal token is "abcdefghijklmnopqrstuvwxyz" then, using Curl, you can reach the Bitext API like this.

```shell
curl -X POST \
  --url https://svc02.api.bitext.com/sentiment/ \
  -H "Authorization: bearer abcdefghijklmnopqrstvwxyz"
```
> You must also specify in the headers that you expect a JSON response, and must then instantiate the header Content-Type with the application/json value.

```shell
curl -X POST \
  --url https://svc02.api.bitext.com/sentiment/ \
  -H "Authorization: bearer abcdefghijklmnopqrstvwxyz" \
  -H "Content-Type: application/json"
```

> In Curl, a first request for the analysis of "I have a beautiful house in Madrid" would appear as follows.

```shell
curl -X POST \
  --url https://svc02.api.bitext.com/sentiment/ \
  -H "Authorization: bearer abcdefghijklmnopqrstvwxyz" \
  -H "Content-Type: application/json"  \
  --data \
    '{"language":"eng", "text":"I have a beautiful house in Madrid"}'
```

>To call the "categories" endpoint.

```shell
curl -X POST \
  --url https://svc02.api.bitext.com/categories/ \
  -H "Authorization : bearer abcdefghijklmnopqrstvwxyz", \
  -H "Content-Type : application/json" \
  --data \
    '{"text":"I have a beautiful house in Madrid",”codingplanid”:”123”}'
```

* https://svc02.api.bitext.com/sentiment/
* https://svc02.api.bitext.com/entities/
* https://svc02.api.bitext.com/concepts/
* https://svc02.api.bitext.com/categories/

The endpoints correspond to the subscriptions you have activated on the My Subscriptions page. For example, if you want to perform a sentiment analysis in English, you must first have an active free trial or paid subscription for sentiment analysis in English activated in your account. You would then use the endpoint https://svc02.api.bitext.com/sentiment and specify English as the language parameter for requests.

In order to make the endpoint work, you must connect your credentials to the endpoint, by adding your personal authentication token to all requests. Your authentication token can be found in the My Profile section of the dashboard. Click API Credentials, copy the token and use it in your code. The token must be sent as the value of the Authorization header, and should appear with a bearer.

The Bitext API works asynchronously. You must first request that the API start analyzing a text, after which you can perform additional requests, until the API returns the correct analysis of the text.

The first request is a POST request that sends a JSON with two parameters: language and text. The value of the text parameter corresponds with the text to be analyzed, and the value of the language parameter corresponds with the language of that text. Currently the limit of characters per API call is of 1000. We are working to increase that limit and we will do so promptly.

This request is calling to the endpoint sentiment analysis in English (the parameter language). The action will only be successfully executed if the user currently has an active trial or paid subscription to the sentiment analysis service in English.

To call the "categories" endpoint, you must provide a "codingplanid" parameter. This parameter identifies the coding plan that will be used in order to perform the categorization. The value of the parameter is numeric, and corresponds to the "key" found in your list of coding plans in the Coding Plans screen of the control panel (see: Coding Plans).

The codes for the currently available Bitext languages are as follows:

* **"eng"**: English
* **"cat"**: Catalan
* **"deu"** German
* **"fra"**: French
* **"ita"**: Italian
* **"nld"**: Dutch
* **"por"**: Portuguese
* **"spa"**: Spanish

> This first request would return a JSON that looks like this.

```json
{
  "resultid": "9a23759db4ae46d8bfbbab47ac4dff1f",
  "success": true,
  "message": "Request accepted"
}
```

> The resultid field in this response is crucial. It will be used to build the subsequent requests. These new requests are GET and include the resultid in the URL. To ask the Bitext API to further analyze one of the texts previously sent, you would write the following request with Curl.

```shell
curl -X GET \
  --url https://svc02.api.bitext.com/sentiment/9a23759db4ae46d8bfbbab47ac4dff1f/ \
  -H "Authorization: bearer abcdefghijklmnopqrstvwxyz" \
  -H "Content-Type: application/json"
```

> If the analysis is already available, the response to that request would be the following.

```json
{
  "resultid": "9a23759db4ae46d8bfbbab47ac4dff1f",
  "sentimentanalysis": [
    {
      "sentence": "I have a beautiful house in Madrid",
      "text_norm": "beautiful",
      "text": "beautiful",
      "score": "3.000000",
      "topic": "house",
      "topic_norm": "house"
    }
  ]
}
```

> If the analysis is not yet available (202 HTTP code), you need to try the same request again.


## Sentiment Analysis

The Bitext sentiment analysis tool analyzes opinions found in texts. It first identifies the topic(s) that are being discussed in a particular text and then evaluates the opinion(s) expressed about the topic(s). The result is a numeric score that is either positive or negative.

For example, for the sentence “I have a beautiful house in Madrid,” Bitext sentiment analysis would identify the topic being discussed as ‘house’ and then establish a relationship between 'house' and 'beautiful’ based on the Bitext engine’s deep knowledge of language. ‘Beautiful' is understood as a positive opinion expressed about the topic ‘house’ and so the numeric score of the sentiment analysis would be positive.

When a text is sent to the sentiment analysis API endpoint, it is divided into different sentences, and analyses are automatically performed on each sentence. If a sentence contains no sentiment expression, it receives a score of ’0’ and the corresponding fields for ‘topics’ and ‘sentiment expressions’ are left blank.

### POST Request

> Sentiment - POST request headers.

```json
{
  "Authorization": "bearer [token]",
  "Content-Type": "application/json"
}
```

> Sentiment - POST request data parameters.

```json
{
  "language": "...",
  "text": "..."
}
```

> Sentiment - POST request successful responses (Code: 201)

```json
{
  "success": true,
  "message": "Request accepted",
  "resultid": "..."
}
```

#### Request

* Endpoint: /sentiment/
* URL: https://svc02.api.bitext.com/sentiment/
* Method: POST
* Headers: _(see code)_
* Data parameters: _(see code)_
* token: Your API credentials (can be copied from the My Profile section of the control panel)
* language: Language of the text you want to analyze (see available languages below)
* text: Text you want to analyze

Available languages:

* **"eng"**: English
* **"cat"**: Catalan
* **"deu"** German
* **"fra"**: French
* **"ita"**: Italian
* **"nld"**: Dutch
* **"por"**: Portuguese
* **"spa"**: Spanish

#### Successful responses

_(see code)_

### GET Request

> Sentiment - GET request Headers.

```json
{
  "Authorization": "bearer [token]",
  "Content-Type": "application/json"
}
```
> Sentiment - GET request successful responses (Code: 201)

```json
{
  "resultid": "..."
}
```
> Sentiment - GET request successful responses (Code: 200)

```json
{
  "success": true,
  "resultid": "...",
  "sentimentanalysis": [
    {
      "topic": "...",
      "topic_norm": "...",
      "text": "...",
      "text_norm": "...",
      "score": "...",
      "sentence": "..."
    }
  ]
}
```

#### Request

* Endpoint: /sentiment/
* URL: https://svc02.api.bitext.com/sentiment/:resultid/
* Method: GET
* Headers: _(see code)_
* token: Your API credentials (can be copied from the My Profile section of the control panel)
* resultid: Identifier of the analysis request (retrieved by the POST transaction)

#### Successful responses

Code 200: The analysis with ID 'resultid' is complete

* resultid: Identifier of the analysis request (retrieved by the POST transaction and sent in the current request)
* topic: Target of an opinion
* topic_norm: Normalized version of the topic
* text: Opinion about the topic
* text_norm: Normalized version of the text
* sentence: Sentence in which a topic/text relation was found


> Sentiment - Example POST Request.

```shell
curl -s -X POST \
  --url https://svc02.api.bitext.com/sentiment/ \
  -H "Authorization: bearer 123451234512345123451234512345ab" \
  -H "Content-Type: application/json" \
  --data '{"language":"eng", "text":"I have a beautiful house in Madrid"}'
```

> Sentiment - Example POST Response.

```json
{
  "success": true,
  "message": "Request accepted",
  "resultid": "123451234512345123451234512345ab"
}
```

> Sentiment - Example GET Request.

```shell
curl -s -X GET \
  --url https://svc02.api.bitext.com/sentiment/123456789abcdefg123456789abcdefg/  \
  -H "Authorization: bearer 123451234512345123451234512345ab" \
  -H "Content-Type: application/json"
```

> Sentiment - Example POST Response.

```json
{
  "resultid": "1b84e78a8655448db6b1730927fba1a2",
  "sentimentanalysis": [
    {
      "topic": "house",
      "topic_norm": "house",
      "text": "beautiful",
      "text_norm": "beautiful",
      "score": "3.00000",
      "sentence": "I have a beautiful house in Madrid"
    }
  ]
}
```

## Concept Extraction

The Bitext concept extraction service identifies different kinds of phrases in texts, including nominal phrases such as 'room service' and 'technical assistance,’ verbal phrases such as 'like’ and 'prefer,’ adjectival phrases such as 'great' or 'useful' and adverbial phrases, such as 'successfully' and 'unfortunately.’

When a text is sent to the concepts endpoint, a single bag of concepts is retrieved. Each concept found in the text appears both exactly as it does in the text and in a normalized version (usually the lemma of the word). The type of concept is specified with a numeric code.

### POST Request

> Concept - POST request headers.

```json
{
  "Authorization": "bearer [token]",
  "Content-Type": "application/json"
}
```

> Concept - POST request data parameters.

```json
{
  "language": "...",
  "text": "..."
}
```

> Concept - POST request successful responses (Code: 201)

```json
{
  "success": true,
  "message": "Request accepted",
  "resultid": "..."
}
```

#### Request

* Endpoint: /concepts/
* URL: https://svc02.api.bitext.com/concepts/
* Method: POST
* Headers: _(see code)_
* Data parameters: _(see code)_
* token: Your API credentials (can be copied from the My Profile section of the control panel)
* language: Language of the text you want to analyze (see available languages below)
* text: Text you want to analyze

Available languages:

* **"eng"**: English
* **"cat"**: Catalan
* **"deu"** German
* **"fra"**: French
* **"ita"**: Italian
* **"nld"**: Dutch
* **"por"**: Portuguese
* **"spa"**: Spanish

#### Successful responses

_(see code)_

### GET Request

> Concept - GET request Headers.

```json
{
  "Authorization": "bearer [token]",
  "Content-Type": "application/json"
}
```

> Concept - GET request successful responses (Code: 202)

```json
{
  "resultid": "..."
}
```

> Concept - GET request successful responses (Code: 200)

```json
{
  "conceptsanalysis": [
    {
      "type": "...",
      "concept": "...",
      "concept_norm": "..."
    }
  ],
  "resultid": "..."
}
```

#### Request

* Endpoint: /concepts/
* URL: https://svc02.api.bitext.com/concepts/:resultid/
* Method: GET
* Headers: _(see code)_
* token: Your API credentials (can be copied from the My Profile section of the control panel)
* resultid: Identifier of the analysis request (retrieved by the POST transaction)

#### Successful responses:

Code 202: The analysis with ID 'resultid' is not complete and must be called again.

Code 200: The analysis with ID 'resultid' is complete

* resultid: Identifier of the analysis request (retrieved by the POST transaction and sent in the current request)
* type: Type of concept identified (see concept types below)
* concept: Concept found (a concept is a nominal, verbal, adverbial or adjectival phrase)
* concept_norm: Normalized version of the concept

Available concepts types:

* **1001:** nominal
* **1002:** adjectival
* **1003:** adverbial
* **1004:** verbal

> Concept - Example POST Request.

```shell
-s -X POST \
  --url https://svc02.api.bitext.com/concepts/ \
  -H "Authorization: bearer 123451234512345123451234512345ab" \
  -H "Content-Type: application/json" \
  --data '{"language":"eng", "text":"I have a beautiful house in Madrid"}'
```

> Concept - Example POST Response.

```json
{
  "success": true,
  "message": "Request accepted",
  "resultid": "123451234512345123451234512345ab"
}
```

> Concept - Example GET Request.

```shell
curl -s -X GET \
  --url https://svc02.api.bitext.com/concepts/123456789abcdefg123456789abcdefg/  \
  -H "Authorization: bearer 123451234512345123451234512345ab" \
  -H "Content-Type: application/json"
```

> Concept - Example POST Response.

```json
{
  "conceptsanalysis": [
    {
      "type": "1004",
      "concept": "have",
      "concept_norm": "have"
    },
    {
      "type": "1001",
      "concept": "beautiful house",
      "concept_norm": "beautiful house"
    },
    {
      "type": "1001",
      "concept": "Madrid",
      "concept_norm": "Madrid"
    }
  ],
  "resultid": "91e950cfe0454043b2cb51cd8b7650a4"
}
```

## Entities Extraction

The Bitext entity extraction service finds entities within texts, such as people’s names, country names and company names. When a text is sent to the entities endpoint, a single bag of entities is retrieved. Each entity found in the text appears both exactly as it does in the text and also as a normalized version. The type of entity is specified with a numeric code.

### POST Request

> Entities - POST request headers.

```json
{
  "Authorization": "bearer [token]",
  "Content-Type": "application/json"
}
```

> Entities - POST request data parameters.

```json
{
  "language": "...",
  "text": "..."
}
```

> Entities - GET request successful responses (Code: 201)

```json
{
  "success": true,
  "message": "Request accepted",
  "resultid": "..."
}
```

> Entities - GET request headers.

```json
{
  "Authorization": "bearer [token]",
  "Content-Type": "application/json"
}
```

> Entities - GET request successful responses (Code: 202)

```json
{
  "resultid": "..."
}
```
> Entities - GET request successful responses (Code: 200)

```json
{
  "entitiesanalysis": [
    {
      "type": "...",
      "concept": "...",
      "concept_norm": "..."
    }
  ],
  "resultid": "..."
}
```

#### Request

* Endpoint: /entities/
* URL: https://svc02.api.bitext.com/entities/
* Method: POST
* Headers: _(see code)_
* Data parameters: _(see code)_
* token: Your API credentials (can be copied from the My Profile section of the control panel)
* language: Language of the text you want to analyze (see available languages below)
* text: Text you want to analyze

Available languages:

* **"eng"**: English
* **"deu"** German
* **"fra"**: French
* **"ita"**: Italian
* **"nld"**: Dutch
* **"por"**: Portuguese
* **"spa"**: Spanish

#### Successful responses

_(see code)_

### GET Request

#### Request

* Endpoint: /entities/
* URL: https://svc02.api.bitext.com/entities/:resultid/
* Method: GET
* Headers: _(see code)_
* token: Your API credentials (can be copied from the My Profile section of the control panel)
* resultid: Identifier of the analysis request (retrieved by the POST transaction)

#### Successful responses:

Code 202: The analysis with ID 'resultid' is not complete and must be called again.

Code 200: The analysis with ID 'resultid' is complete

* resultid: Identifier of the analysis request (retrieved by the POST transaction and sent in the current request)
* type: Type of entity identified (see available entity types below)
* entity: Entity found (person, country, company, etc.)
* entity_norm: Normalized version of the entity

Available entities types:

* **0:** Unknown
* **1:** Name of person
* **2:** Car license plate
* **3:** Place
* **4:** Phone number
* **5:** Email address
* **6:** Company
* **7:** Organization
* **8:** URL
* **9:** IP address
* **10:** Date
* **11:** Hour
* **15:** Money
* **16:** Address
* **17:** Twitter hashtag
* **18:** Twitter user
* **19:** Other alphanumeric


> Entities - Example POST Request.

```shell
-s -X POST --url https://svc02.api.bitext.com/entities/ -H "Authorization: bearer 123451234512345123451234512345ab" -H "Content-Type: application/json" --data '{"language":"eng", "text":"I have a beautiful house in Madrid"}'
```

> Entities - Example POST Response.

```json
{
  "success": true,
  "message": "Request accepted",
  "resultid": "123451234512345123451234512345ab"
}
```

> Entities - Example GET Request.

```shell
curl -s -X GET \
  --url https://svc02.api.bitext.com/entities/123456789abcdefg123456789abcdefg/  \
  -H "Authorization: bearer 123451234512345123451234512345ab" \
  -H "Content-Type: application/json"
```

> Entities - Example POST Response.

```json
{
  "entitiesanalysis": [
    {
      "type": "3",
      "entity": "Madrid",
      "entity_norm": "Madrid"
    }
  ],
  "resultid": "91e950cfe0454043b2cb51cd8b7650a4"
}
```

## Categories Extraction

The Bitext categorization service categorizes the sentences of a text according to a specific set of categories or a “coding plan.” A coding plan is a set of categories and words (or terms) that relate to the information you want Bitext to extract from your data. When you call the categories endpoint you must provide a coding plan identifier in the 'codingplanid' parameter. The identifier of the coding plan is its ‘key' attribute in the control panel.

When a text is sent to the categories endpoint, it is divided into different sentences. One or more categories is assigned to each sentence. In addition to the category assigned to the sentence, the service retrieves a list of terms that appear in the sentence that caused the sentence to be assigned to that particular category. For example, if the coding plan has the category ’House’ then all sentences that contain the word “house” are assigned to that category.

The category extraction service would therefore assign the sentence “I have a beautiful house in Madrid” to the category ‘House.’ If a sentences contains no words that trigger categorization, it is assigned to the default category ’None’ and the list of terms remains empty.

### POST Request

> Categories - POST request headers

```json
{
  "Authorization": "bearer [token]",
  "Content-Type": "application/json"
}
```

> Categories - POST request data parameters

```json
{
  "language": "...",
  "text": "...",
  "codingplanid": "..."
}
```

> Categories -  POST request successful responses (Code: 201)

```json
{
  "success": true,
  "message": "Request accepted",
  "resultid": "..."
}
```

> Categories - GET request headers

```json
{
  "Authorization": "bearer [token]",
  "Content-Type": "application/json"
}
```

> Categories - GET request successful responses (Code: 202)

```json
{
  "resultid": "..."
}
```

> Categories - GET request successful responses (Code: 200)

```json
{
  "categoriesanalysis": [
    {
      "category": "...",
      "terms": [
        "..."
      ],
      "sentence": "..."
    }
  ],
  "resultid": "..."
}
```

#### Request

* Endpoint: /categories/
* URL: https://svc02.api.bitext.com/categories/
* Method: POST
* Headers: _(see code)_
* Data parameters: _(see code)_
* token: Your API credentials (can be copied from the My Profile section of the control panel)
* language: Language of the text you want to analyze (see available languages below)
* text: Text you want to analyze
* codingplanid: Identifier of the coding plan you want to use to categorize (the ‘key' attribute of the coding plan found in the control panel)

Available languages:

* **"eng"**: English
* **"deu"** German
* **"cat":** Catalan
* **"fra"**: French
* **"ita"**: Italian
* **"nld"**: Dutch
* **"por"**: Portuguese
* **"spa"**: Spanish

#### Successful responses

_(see code)_


### GET Request

#### Request

* Endpoint: /categories/
* URL: https://svc02.api.bitext.com/categories/:resultid/
* Method: GET
* Headers: _(see code)_
* token: Your API credentials (can be copied from the My Profile section of the control panel)
* resultid: Identifier of the analysis request (retrieved by the POST transaction)

#### Successful responses:

Code 202: The analysis with ID 'resultid' is not complete and must be called again.

Code 200: The analysis with ID 'resultid' is complete

* resultid: Identifier of the analysis request (retrieved by the POST transaction and sent in the current request)
* category: Category assigned to the current sentence
* terms: Words that triggered the categorization of the sentence
* sentence: Sentence in which the category was found

Available categories types:

* **1001:** nominal
* **1002:** adjectival
* **1003:** adverbial
* **1004:** verbal


> Categories - Example POST Request.

```shell
-s -X POST \
  --url https://svc02.api.bitext.com/categories/ \
  -H "Authorization: bearer 123451234512345123451234512345ab" \
  -H "Content-Type: application/json" \
  --data '{"language":"eng", "text":"I have a beautiful house in Madrid", "codingplanid":"hotels_ENG_0"}'
```

> Categories - Example POST Response.

```json
{
  "success": true,
  "message": "Request accepted",
  "resultid": "123451234512345123451234512345ab"
}
```

> Categories - Example GET Request.

```shell
curl -s -X GET \
  --url https://svc02.api.bitext.com/categories/123456789abcdefg123456789abcdefg/  \
  -H "Authorization: bearer 123451234512345123451234512345ab" \
  -H "Content-Type: application/json"
```

> Categories - Example GET Response.

```json
{
  "categoriesanalysis": [
    {
      "category": "room",
      "terms": [
        "room"
      ],
      "sentence": "I have a beautiful room in Madrid"
    }
  ],
  "resultid": "1c20ccf9c0f24598a5ed09d23dfa460a"
}
```
