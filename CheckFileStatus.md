# Introduction #

This API call lets you check whether the file is downloadable from ifile.it. You can use this to check any file whether it belongs to you or not.

<br><br>
<hr />


<h3>Get file status</h3>
<b>Request URL</b>
<pre><code>http://ifile.it/api-check_file_status.api<br>
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
<tr><td> ukey                  </td><td> no              </td><td> string      </td><td>                        </td><td>                      </td><td> The unique key for a file (see <a href='Ukey.md'>Ukey</a>) </td></tr></tbody></table>


<br>
<br>
<b>API response parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> status                </td><td> string      </td><td> ok<br>error            </td><td> Whether the request was successful, error message parameter shown on error </td></tr>
<tr><td> file_status           </td><td> int         </td><td> 1                      </td><td> File status of 1 means the file is all ok, anything else means an error </td></tr>
<tr><td> message               </td><td> string      </td><td>                        </td><td> More verbose message telling you whether the file is ok, or not (and why its missing) in error cases </td></tr>
<tr><td> ukey                  </td><td> string      </td><td>                        </td><td> The unique key for a file (see <a href='Ukey.md'>Ukey</a>) </td></tr>
<tr><td> name                  </td><td> string      </td><td>                        </td><td> File name          </td></tr>
<tr><td> size                  </td><td> int         </td><td>                        </td><td> File size in bytes </td></tr>
<tr><td> mime                  </td><td> string      </td><td>                        </td><td> File <a href='http://en.wikipedia.org/wiki/MIME'>mimetype</a> </td></tr></tbody></table>

<br><br><br>
<hr />
<h3>Sample Code in PHP</h3>
Using the official PHP api wrapper, see <a href='http://code.google.com/p/ifileit/downloads/list'>Downloads</a>
<pre><code>&lt;?php<br>
<br>
/**<br>
 * this example code snippet checks the status of a file<br>
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
//ukey for test file, see http://code.google.com/p/ifileit/wiki/Ukey   for more details<br>
$ukey = '6phxv2z'; //  http://ifile.it/6phxv2z/Internet_map_1024.jpg<br>
<br>
<br>
<br>
<br>
<br>
//get account info<br>
try {<br>
	<br>
	$response = $IfileApi-&gt;post(<br>
		'http://ifile.it/api-check_file_status.api',<br>
		array(<br>
			'ukey'	=&gt;	$ukey<br>
		)<br>
	);<br>
	<br>
	if ( $response['file_status'] == 1 ){<br>
		<br>
		print_r( 'file is downloadable');<br>
	}<br>
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