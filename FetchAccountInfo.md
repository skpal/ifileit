## Introduction ##

Once you have an apikey for an ifile.it account you can use it to fetch certain account information and statistics which you may incorporate in your application/code.


<br><br>
<hr />

<h3>Fetch apikey</h3>
<b>Request URL</b>
<pre><code>http://ifile.it/api-fetch_account_info.api<br>
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
<tr><td> akey                  </td><td> no              </td><td> string      </td><td>                        </td><td>                      </td><td> apikey of the account to fetch information/stats for (see <a href='FetchApikey.md'>FetchApikey</a>) </td></tr></tbody></table>

<br>
<br>
<b>API response parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> status                </td><td> string      </td><td> ok<br>error            </td><td> Whether the request was successful, error message parameter shown on error </td></tr>
<tr><td> num_files             </td><td> int         </td><td>                        </td><td> Number of working files attached to account </td></tr>
<tr><td> num_folders           </td><td> int         </td><td>                        </td><td> Number of folders belonging to this account </td></tr>
<tr><td> storage_used          </td><td> int         </td><td>                        </td><td> Sum total of bytes (storage) taken by all your files </td></tr>
<tr><td> bw_used_24hrs         </td><td> int         </td><td>                        </td><td> Sum total of bytes downloaded (in all downloads partial or full) by your account in the last 24 hours </td></tr>
<tr><td> user_id               </td><td> int         </td><td>                        </td><td> Unique account number </td></tr>
<tr><td> user_name             </td><td> string      </td><td>                        </td><td> Account username   </td></tr>
<tr><td> user_group            </td><td> string      </td><td> normal<br>premium<br>vip </td><td> User group this account belongs to </td></tr></tbody></table>

<br><br><br>
<hr />
<h3>Sample Code in PHP</h3>
Using the official PHP api wrapper, see <a href='http://code.google.com/p/ifileit/downloads/list'>Downloads</a>
<pre><code>&lt;?php<br>
<br>
/**<br>
 * this example code snippet retrieves various user account information such as number of files and so on<br>
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
//get account info<br>
try {<br>
	<br>
	$response = $IfileApi-&gt;post(<br>
		'http://ifile.it/api-fetch_account_info.api',<br>
		array(<br>
			'akey'	=&gt;	$apikey<br>
		)<br>
	);<br>
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
//output our response response array to see its structure<br>
print print_r( $response,true );<br>
<br>
<br>
?&gt;<br>
</code></pre>