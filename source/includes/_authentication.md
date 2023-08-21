# Authentication

Sobot employs authentication keys to grant access to its API. To acquire a new Sobot API keys, please follow below instructons to obtain keys from our portal.

Sign In to [app.sobot.in](https://app.sobot.in) -> Settings -> Developers tools - > Generate New Keys

(Only Admin can generate API Keys.)

<aside class="warning">
Every time you will generate the new keys, old keys will be deprecated. 
</aside>

For each API request directed to the server, Sobot requires the API keys to be included in the header. The header should follow this format:

`x-api-key: yourapiaccesskey`

`x-api-secret: yourapisecretkey`

These keys play a crucial role in ensuring the security and validity of API interactions. Please ensure that you incorporate your provided access and secret keys correctly in the headers of your API requests.

<aside class="notice">
You must replace <code>yourapiaccesskey</code> & <code>yourapisecretkey</code> with your personal API keys.
</aside>
