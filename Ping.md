## Introduction ##

Ping is the the most simple call in the ifile.it API, and it allows you to check whether the service is up.


<br><br>
<hr />

<h3>Fetch apikey</h3>
<b>Request URL</b>
<pre><code>http://ifile.it/api-ping.api<br>
</code></pre>

<br>
<br>
<b>HTTP GET parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>optional</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>default value</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> response              </td><td> yes             </td><td> string      </td><td> json<br />text         </td><td> json                 </td><td> In what format the API response should be </td></tr></tbody></table>

<br>
<br>
<b>HTTP POST parameters</b>

<i>none</i>

<br>
<br>
<b>API response parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> status                </td><td> string      </td><td> ok<br>error            </td><td> Whether the request was successful, error message parameter shown on error </td></tr>
<tr><td> message               </td><td> string      </td><td> "pong"                 </td><td> The api replying to your ping </td></tr></tbody></table>

<br><br><br>
<hr />
<h3>Sample Code in PHP</h3>
Using the official PHP api wrapper, see <a href='http://code.google.com/p/ifileit/downloads/list'>Downloads</a>
<pre><code>&lt;?php<br>
<br>
/**<br>
 * this example code snipppet pings the ifile.it api and checks the response for a "pong" reply<br>
 * usefull for checking if the site/api is up<br>
 */<br>
<br>
//set error reporting and include our api class<br>
error_reporting(E_ALL); ini_set( 'display_errors', 'On' );<br>
require_once( 'IfileApi.php' ); //in same directory as this example script<br>
<br>
<br>
//create api model<br>
$IfileApi = new IfileApi();<br>
<br>
<br>
<br>
<br>
//try pinging<br>
try {<br>
	<br>
	$response = $IfileApi-&gt;post(<br>
		'http://ifile.it/api-ping.api',<br>
		array()<br>
	);<br>
}<br>
catch ( IfileApiException $e){<br>
	<br>
	print 'IfileApiException &gt; '.$e-&gt;getMessage();<br>
}<br>
<br>
<br>
if ( $response['message'] == 'pong' ){<br>
	<br>
	print 'ifile.it api is up'."\n\n";<br>
}<br>
<br>
<br>
//output our response response array to see its structure<br>
print print_r( $response,true );<br>
<br>
<br>
?&gt;<br>
</code></pre>