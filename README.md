# Stripe-graphql
## Expose Stripe over GraphQL using TailCall

Tailcall DSL builds on your existing GraphQL knowledge by allowing the addition of some custom directives.

## Installation 

### NPM

-  Install Tailcall by running the following command in your terminal:
```
npm i -g @tailcallhq/tailcall
```
- To verify the correct installation of Tailcall, run:
```
tailcall
```

## Launch
```
tailcall start ./schema.graphql
```

If the command succeeds, you should see logs like the following below.

```
INFO Env file: "/Users/apple/Docs/React stuff/Projects/tailcall/Stripe-tailcall/.env" loaded 
 INFO File read: ./schema.graphql ... ok
 INFO File read: ././types/balance.graphql ... ok
 INFO File read: ././types/customer.graphql ... ok
 INFO N + 1 detected: 0
 INFO 🚀 Tailcall launched at [127.0.0.1:8000] over HTTP/1.1
 INFO 🌍 Playground: http://127.0.0.1:8000
 ```

 The server starts with the schema provided and prints out a load of meta information. We will cover those in detail in a bit. For now, open the [playground URL](http://localhost:8000) in a new tab in your browser and try it out for yourself!

 ## Execute
1. Open a web browser and go to http://localhost:8000. This should load the GraphiQL interface.

2. In the query editor of GraphiQL, enter the following query
```
query{
  balance{
    object
    available{
      amount
      currency
      source_types{
        card
      }
    }
    livemode
    pending{
      amount
      currency
      source_types{
        card
      }
    }
  }
}
```

3. After running the query in GraphiQL, expect to see a JSON response structured like this:
```
{
  "data": {
    "balance": {
      "object": "balance",
      "available": [
        {
          "amount": 0,
          "currency": "inr",
          "source_types": {
            "card": 0
          }
        }
      ],
      "livemode": false,
      "pending": [
        {
          "amount": 964600,
          "currency": "inr",
          "source_types": {
            "card": 964600
          }
        }
      ]
    }
  }
}
```

You can now add more fields, and compose more queries together!