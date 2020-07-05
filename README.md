# Httq Developer Documentation 👩‍💻👨‍💻

(Like there is any other kind?)

🛑 Attention - Httq is in heavy development. Use at own risk. 🧪

## What is Httq ⚡🏄‍♀️

Thanks for asking! 😀

Httq (or hook to the queue) is a little glue service that lets you integrate your serverless functions with webhooks, without having to set up a queue. Httq does that for you, in a single API call, saving you time and effort in the process.

Set up a queue with an API call, get a webhook endpoint, and magic happens ✨.

Think Zapier, but just for developers. And just for webhook integrations. For now.

You can find us on the web at [httq.dev](https://httq.dev).

## Usage ⚒️

While in early access you can request your credentials by filling in the form at [httq.dev](https://httq.dev#waitingList).

### Authentication

All requests dealing with webhook management need to be authenticated.
You do this by passing your API key in the `Authorization` header, as such:

```bash
Authorization: Bearer YOUR_API_KEY
```

Webhook invocation requests don't require authentication, so we advise you keep their URLs secret.

### Set up a hook 🔨

#### Request

Send a POST request to `https://dev.api.httq.dev/v1/YOUR_USER_ID/hooks`.
Make sure to pass the authorization header: `Authorization: Bearer YOUR_API_KEY`.


Body is a JSON payload containing the following:

- `name` (string) - your webhook name (can be anything)
- `source` (string) - where your webhook originates, can be anything but we recommend using the domain you're integrating
- `target` (string) - the location of the lambda you're integrating with. Httq will relay all webhook requests to this URL. This needs to work.

```bash
curl -X POST 'https://dev.api.httq.dev/v1/YOUR_USER_ID/hooks' \
--header 'Content-Type:application/json' \
--header 'Authorization: Bearer YOUR_API_KEY' \
--data-raw '{
    "name": "YOUR_WEBHOOK_NAME",
    "source": "SERVICE_YOU_ARE_INTEGRATING",
    "target": "YOUR_LAMBDA_ENDPOINT"
}'
```

#### Response

The response will contain:

- `id` the ID of the hook,
- `url` - the URL to pass your webhook integration.
- `name`, `target`, `source` - what you passed to it earlier

```json
{
  "id": "YOUR_WEBHOOK_ID",
  "name": "YOUR_WEBHOOK_NAME",
  "url": "https://URL_TO_PASS_TO_YOUR_WEBHOOK_INTEGRATION.api.httq.dev/",
  "target": "YOUR_LAMBDA_ENDPOINT",
  "source": "SERVICE_YOU_ARE_INTEGRATING"
}
```

### List hooks 📚

Send a GET request to `https://dev.api.httq.dev/v1/YOUR_USER_ID/hooks`.
Make sure to pass the authorization header: `Authorization: Bearer YOUR_API_KEY`.

The response will be an array of all the webhooks you have set up:

```json
[
  {
    "id": "YOUR_WEBHOOK_ID",
    "name": "YOUR_WEBHOOK_NAME",
    "url": "https://URL_TO_PASS_TO_YOUR_WEBHOOK_INTEGRATION.api.httq.dev/",
    "target": "YOUR_LAMBDA_ENDPOINT",
    "source": "SERVICE_YOU_ARE_INTEGRATINGn"
  },
  {
    "id": "YOUR_WEBHOOK_ID",
    "name": "YOUR_WEBHOOK_NAME",
    "url": "https://URL_TO_PASS_TO_YOUR_WEBHOOK_INTEGRATION.api.httq.dev/",
    "target": "YOUR_LAMBDA_ENDPOINT",
    "source": "SERVICE_YOU_ARE_INTEGRATINGn"
  },
  {
    "id": "YOUR_WEBHOOK_ID",
    "name": "YOUR_WEBHOOK_NAME",
    "url": "https://URL_TO_PASS_TO_YOUR_WEBHOOK_INTEGRATION.api.httq.dev/",
    "target": "YOUR_LAMBDA_ENDPOINT",
    "source": "SERVICE_YOU_ARE_INTEGRATINGn"
  }
]
```

### Delete a hook 🚮

#### Request

Send a DELETE request to `https://dev.api.httq.dev/v1/YOUR_USER_ID/hooks/HOOK_ID_TO_DELETE`.

Make sure to pass the authorization header: `Authorization: Bearer YOUR_API_KEY`.

```bash
curl -X DELETE 'https://dev.api.httq.dev/v1/YOUR_USER_ID/hooks/HOOK_ID_TO_DELETE' \
--header 'Authorization: Bearer YOUR_API_KEY'
```

### Invoke a hook 🎣

Pass the URL you get from creating a webhook to the service you're integrating.
Httq will send it's JSON payload to your target endpoint.

There is no authentication on webhook invocation, so keep that URL safe.

## Pricing 🤑

Httq is free to use while in beta. Hobbyist, business, and professional pricing coming soon.

There will always be a free tier.

## Contact us 🦅

Best way to get in touch is via email - [info@httq.dev](mailto:info@httq.dev).

There will be Twitter at some point.

Made with ❤️ in London.
