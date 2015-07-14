# Introduction #

This call lets your retrieve detailed file information for any file in your account.


<br><br>
<hr />

<h3>Fetch apikey</h3>
<b>Request URL</b>
<pre><code>http://ifile.it/api-fetch_file_info.api<br>
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
<tr><td> akey                  </td><td> no              </td><td> string      </td><td>                        </td><td>                      </td><td> apikey for a users account (see <a href='FetchApikey.md'>FetchApikey</a>) </td></tr>
<tr><td> ukey                  </td><td> no              </td><td> string      </td><td>                        </td><td>                      </td><td> The unique key for a file (see <a href='Ukey.md'>Ukey</a>) </td></tr></tbody></table>

<br>
<br>
<b>API response parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> status                </td><td> string      </td><td> ok<br>error            </td><td> Whether the request was successful, error message parameter shown on error </td></tr>
<tr><td> file_status           </td><td> int         </td><td> 1                      </td><td> File status of 1 means the file is all ok, anything else means an error with file </td></tr>
<tr><td> ukey                  </td><td> string      </td><td>                        </td><td> The unique key for a file (see <a href='Ukey.md'>Ukey</a>) </td></tr>
<tr><td> name                  </td><td> string      </td><td>                        </td><td> File name          </td></tr>
<tr><td> size                  </td><td> int         </td><td>                        </td><td> File size in bytes </td></tr>
<tr><td> md5                   </td><td> string      </td><td>                        </td><td> File <a href='http://en.wikipedia.org/wiki/Md5sum'>md5</a> checksum </td></tr></tbody></table>


<br><br><br>
<hr />
<h3>Sample Code in PHP</h3>
Using the official PHP api wrapper, see <a href='http://code.google.com/p/ifileit/downloads/list'>Downloads</a>
<pre><code>&lt;?php<br>
<br>
/**<br>
 * this example code snippet retrieves various file information for a file in your account<br>
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
//file for which we want info for<br>
$ukey = 'UKEY'; // see for more info http://code.google.com/p/ifileit/wiki/Ukey<br>
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
//get file info<br>
try {<br>
	<br>
	$response = $IfileApi-&gt;post(<br>
		'http://ifile.it/api-fetch_file_info.api',<br>
		array(<br>
			'akey'	=&gt;	$apikey,<br>
			'ukey'	=&gt;	$ukey<br>
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