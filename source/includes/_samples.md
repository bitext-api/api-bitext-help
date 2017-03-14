# Code Samples

You can see in the right side some examples in Perl, Phyton, Ruby and Java.

> **CODE SAMPLES**

```perl
use Mojo::UserAgent;
use Mojo::JSON qw(encode_json);
my $ua = Mojo::UserAgent->new;
my $oauth_token = '';
my $endpoint = "https://svc02.api.bitext.com/sentiment/";
my $headers = { Authorization => "bearer $oauth_token", 'Content-Type' => 'application/json' };
my $params = {"language" => "eng","text" => "I have a beautiful house in Madrid"};
$tx = $ua->post($endpoint, $headers, json => $params);
my $action_id = $tx->res->json->{resultid};
my $analysis;

until ($analysis)
{
     $tx = $ua->get($endpoint.$action_id.'/', $headers);
     eval { $analysis = $tx->res->json };
}

print encode_json $analysis;
```

```python
import requests, json

oauth_token = 'MY TOKEN HERE'
endpoint = "https://svc02.api.bitext.com/sentiment/"
headers = { "Authorization" : "bearer " + oauth_token, "Content-Type" : "application/json" }
params = {"language" : "eng","text" : "I have a beautiful house in Madrid"}

res = requests.post(endpoint, headers=headers, data=json.dumps(params))
resultid = json.loads(res.text).get('resultid')

analysis = None

while analysis == None:

    res = requests.get(endpoint + resultid + '/', headers=headers)
    if res.status_code == 200 :
        analysis = res.text

print(analysis)
```

```ruby
require 'httpclient'
require 'json'

oauth_token = ''
endpoint = "https://svc02.api.bitext.com/sentiment/"
headers = { "Authorization" => "bearer " + oauth_token, "Content-Type" => "application/json"}
params = {"language" => "eng","text" => "I have a beautiful house in Madrid"}.to_json

clnt = HTTPClient.new
res = clnt.post(endpoint,params,headers)

puts res.status
content = JSON.parse(res.content)
resultid = content["resultid"]

analysis = ""

while analysis == ""  do

  res = clnt.get(endpoint + resultid + "/",{},headers)
  if res.status == 200
    analysis = res.content
  end

end

puts analysis
```

```java
import java.net.HttpURLConnection;
import java.net.URL;
import java.io.*;
import org.json.JSONObject;

public class Client {

    public static String oauth_token = "";
    public static String endpoint = "https://svc02.api.bitext.com/sentiment/";
    public static String textdata =
    "{\"language\":\"eng\",\"text\":\"I have a beautiful house in Madrid\"}";

    public static void main(String[] args)throws Exception {

        // Send text to analyze
        URL url1 = new URL(endpoint);
        HttpURLConnection conn1 = createAPIConnection("POST",url1);
        DataOutputStream outStream = new DataOutputStream(conn1.getOutputStream());
        outStream.write(textdata.getBytes("UTF8"));
        outStream.flush();
        outStream.close();

        // Get the id of the analysis launched
        String sResponse1 = getAPIResponse(conn1);
        JSONObject jResponse1 = new JSONObject(sResponse1);
        String resultid = jResponse1.getString("resultid");

        // Ask for the result of the analysis launched before
        // Try until the analysis is ready and the API returns it
        URL url2 = new URL(endpoint + resultid + "/");
        String sResponse2 = "";

        while (sResponse2 == "")
        {
           HttpURLConnection conn2 = createAPIConnection("GET",url2);
           if (conn2.getResponseCode() == 200)
	   {
		sResponse2 = getAPIResponse(conn2);
	   }
        }
         public static HttpURLConnection createAPIConnection(String method, URL url)
    throws Exception {

        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setRequestMethod(method);
        conn.setRequestProperty("Content-Type", "application/json");
        conn.setRequestProperty("Authorization", "bearer " + oauth_token);

        if (method == "POST")
        {
            conn.setDoOutput(true);
            conn.setDoInput(true);
        }
        return conn;
    }

    public static String getAPIResponse(HttpURLConnection conn) throws Exception {

        String sResponse = "";
        BufferedReader in = new BufferedReader(new InputStreamReader(conn.getInputStream()));
        String decodedString;

        while ((decodedString = in.readLine()) != null)
        {
            sResponse = sResponse+"\n"+decodedString;
        }
        sResponse = sResponse.trim();
        in.close();
        return sResponse;
    }

}
```
