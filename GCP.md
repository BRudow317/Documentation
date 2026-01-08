# Google Cloud Platform (GCP)

## API Keys

#### Standard API keys
Standard API keys provide a way to associate a request with a project for billing and quota purposes. When you use a standard API key (an API key that has not been bound to a service account) to access an API, the API key doesn't identify a principal. Without a principal, the request can't use Identity and Access Management (IAM) to check whether the caller is authorized to perform the requested operation.

#### Service account-bound API keys
API keys bound to a service account provide the identity and authorization of the service account to a request. When you use an API key that has been bound to a service account to access an API, your request is processed as if you used the bound service account to make the request.

##### The only API that supports bound API keys is [aiplatform.googleapis.com](https://aiplatform.googleapis.com).

### API key components
An API key has the following components, which let you manage and use the key:

#### String
The API key string is an encrypted string, for example, AIzaSyDaGmWKa4JsXZ-HjGw7ISLn_3namBGewQe. When you use an API key to access an API, you always use the key's string. API keys don't have an associated JSON file.
#### ID
The API key ID is used by Google Cloud administrative tools to uniquely identify the key. The key ID can't be used to access APIs. The key ID can be found in the URL of the key's edit page in the Google Cloud console. You can also get the key ID by using the Google Cloud CLI to list the keys in your project.
#### Display name
The display name is an optional, descriptive name for the key, which you can set when you create or update the key.

## Google Maps API
To use Google Maps services in your application, you need to enable the appropriate APIs in the Google Cloud Console and obtain an API key. The most commonly used APIs include:
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Simple Marker</title>
    <!-- The callback parameter is required, so we use console.debug as a noop -->
    <script async src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY_HERE&callback=console.debug&libraries=maps,marker&v=beta">
    </script>
    <style>
      /* Always set the map height explicitly to define the size of the div
       * element that contains the map. */
      gmp-map {
        height: 100%;
      }

      /* Optional: Makes the sample page fill the window. */
      html,
      body {
        height: 100%;
        margin: 0;
        padding: 0;
      }
    </style>
  </head>
  <body>
    <gmp-map center="40.12150192260742,-100.45039367675781" zoom="4" map-id="DEMO_MAP_ID">
      <gmp-advanced-marker position="40.12150192260742,-100.45039367675781" title="My location"></gmp-advanced-marker>
    </gmp-map>
  </body>
</html>
```
