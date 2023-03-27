---
title: Grepper API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - php

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the Grepper API!  Grepper allows you to quickly search, add and edit code snippets & technical answers to all those little coding problems you run into every day (It’s Basically stackoverflow, but tightly integrated into your workflow… and without the overzealous moderators…). 

This API is a work in progress and we are calling on all community members to help build it out. Specifically we need language bindings/client libraries for [Javascript, Python, Java, Go, .NET, Node, Ruby]. We also want feature requests from the community, so we can unlock all the value of Grepper through this API.

Note: You will need a [grepper account](https://www.grepper.com), after creating an account you can find your [api key here](https://www.grepper.com/app/settings-account.php)

You can hit the API endpoints directly or use one of our API client libraries:

Language | Github Repo | Status | Notes
-------- | ----------- | ------ | -------
PHP      |(https://github.com/CodeGrepper/grepper-php)| In Progress  | Authors: [Taylor Hawkes](https://github.com/TaylorHawkes)
Javascript|(https://github.com/CodeGrepper/grepper-javascript)| Need Contributors  | Authors: TBD
Python|(https://github.com/CodeGrepper/grepper-python)| Need Contributors  | Authors: TBD
Node|(https://github.com/CodeGrepper/grepper-node)| Need Contributors  | Authors: TBD
Go|(https://github.com/CodeGrepper/grepper-go)| Need Contributors  | Authors: TBD


<aside class="notice">
To get a feel for how this API works see the example to the right.
</aside>

> Here is an example of doing a grepper search through the api:

```shell
curl https://api.grepper.com/v1/answers/search \
  -u your_grepper_api_key_here: \
  --data-urlencode query="javascript loop array backwords" \
  -G
```


# Authentication
The Grepper API uses API keys to authenticate requests. You can view and manage your API key in your [Grepper Account Settings](https://www.grepper.com/app/settings-account.php).

Authentication to the API is performed via HTTP Basic Auth. Provide your API key as the basic auth username value. You do not need to provide a password.

If you need to authenticate via bearer auth (e.g., for a cross-origin request), use -H "Authorization: Bearer youapikeyhere" instead of -u youapikeyhere.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

# Answers

## Search All Answers

```shell
curl https://api.grepper.com/v1/answers/search \
  -u your_grepper_api_key_here: \
  --data-urlencode query="javascript loop array backwords" \
  -G
```

```php
$grepper = new \Grepper\GrepperClient(
  'your_api_key_here'
);
$grepper->answers->search([
  'query' => 'javascript loop array backwords',
]);
```

> Response:

```json
{
  "object": "list",
  "data": [
    {
      "id": 560676,
      "content": "let arr = [1, 2, 3];\n\narr.slice().reverse().forEach(x => console.log(x))\n Run code snippetHide results",
      "author_name": "Homely Hyena",
      "author_profile_url": "https://www.grepper.com/profile/homely-hyena-qrcy8ksj0gew",
      "title": "javascript loop through array backwords",
      "upvotes": 0,
      "object": "answer",
      "downvotes": 0
    },
    {
      "id": 504956,
      "content": "var arr=[1,2,3];\narr.reverse().forEach(x=> console.log(x))",
      "author_name": "Yanislav Ivanov",
      "author_profile_url": "https://www.grepper.com/profile/yanislav-ivanov-r2lfrl14s6xy",
      "title": "js loop array back",
      "upvotes": 2,
      "object": "answer",
      "downvotes": 2
    }
  ]
}
```

This endpoint searches all answers based on a query.

### HTTP Request

`GET https://api.grepper.com/v1/answers/search`




### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
query | true | false | query to search through answer titles ex: "Javascript loop array backwords"
similarity | false | 60 | How similar the query has to be to the answer title. 1-100 where 1 is really loose matching and 100 is really strict/tight match.

<aside class="success">
Remember — You'll need to swap out your_grepper_api_key_here for you api key.
</aside>

## Retreive an Answer
<aside class="warning">This endpoint is in progress and not yet available.</aside>

```shell
curl https://api.grepper.com/v1/answers/560676 \
  -u your_api_key_here:
```

```php
$grepper = new \Grepper\GrepperClient(
  'your_api_key_here'
);

$answer=$stripe->answers->retrieve(560676);
```

> Response:

```json
    {
      "id": 560676,
      "content": "let arr = [1, 2, 3];\n\narr.slice().reverse().forEach(x => console.log(x))\n Run code snippetHide results",
      "author_name": "Homely Hyena",
      "author_profile_url": "https://www.grepper.com/profile/homely-hyena-qrcy8ksj0gew",
      "title": "javascript loop through array backwords",
      "upvotes": 0,
      "object": "answer",
      "downvotes": 0
    }
```

This endpoint retrieves a specific answer.



### HTTP Request

`GET https://api.grepper.com/v1/answers/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The answer id of the answer to retrieve

## Update a specific answer
<aside class="warning">This endpoint is in progress and not yet available.</aside>

```php
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl https://api.grepper.com/v1/answers/560676 \
  -u your_api_key_here: \
  -d "answer[content]"="new answer content here"
```

```php
$grepper = new \Grepper\GrepperClient(
  'your_api_key_here'
);
$grepper->answers->update(
  '560676',
  ['answer' => ['content' => 'new answer content here']]
);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "success" : "true"
}
```

This endpoint updates a specific answer.

### HTTP Request

`POST https://api.grepper.com/v1/answers/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The answer id of the answer to update

