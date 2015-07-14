## Introduction ##

Getting an apikey for any API calls which require one is a matter of sending the username and password combination for an account via a SSL.

The apikey only changes when the account holder changes his/her password, and might be a good idea to cache/save the apikey locally if you are confident the account password would not be changed often.


<br><br>
<hr />

<h3>Fetch apikey</h3>
<b>Request URL</b>
<pre><code>https://secure.ifile.it/api-fetch_apikey.api<br>
</code></pre>

<br>
<br>
<b>HTTP GET parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>optional</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>default value</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> response              </td><td> yes             </td><td> string      </td><td> json<br />text         </td><td> json                 </td><td> In what format the API response should be </td></tr></tbody></table>

<br>
<br>
<b>HTTP POST parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>optional</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>default value</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> username              </td><td> no              </td><td> string      </td><td>                        </td><td>                      </td><td> Account username   </td></tr>
<tr><td> password              </td><td> no              </td><td> string      </td><td>                        </td><td>                      </td><td> Account password   </td></tr></tbody></table>

<br>
<br>
<b>API response parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> status                </td><td> string      </td><td> ok<br>error            </td><td> Whether the request was successful, error message parameter shown on error </td></tr>
<tr><td> akey                  </td><td> string      </td><td>                        </td><td> The apikey for this account </td></tr></tbody></table>

<br><br><br>
<hr />
<h3>Sample Code in PHP</h3>
Using the official PHP api wrapper, see <a href='http://code.google.com/p/ifileit/downloads/list'>Downloads</a>
<pre><code>&lt;?php<br>
<br>
/**<br>
 * this example code snipppet gets apikey for an account via ssl using username/pass for that ifile.it account<br>
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
//username and pass for an account for which you wish to get the apikey<br>
$username = 'USERNAME';<br>
$password = 'PASSWORD';<br>
<br>
<br>
<br>
<br>
//get the key<br>
try {<br>
	<br>
	$apikey = $IfileApi-&gt;fetchApiKey($username, $password);<br>
	<br>
	print 'the apikey for @'.$username .' is: '.$apikey."\n\n";<br>
}<br>
catch ( IfileApiException $e){<br>
	<br>
	print 'IfileApiException &gt; '.$e-&gt;getMessage();<br>
}<br>
<br>
<br>
<br>
<br>
<br>
//you can now pass along this apikey in subsequent request, <br>
//to authenticate each request as coming from the user for whom this key belongs<br>
<br>
<br>
?&gt;<br>
</code></pre>