## Introduction ##

Uploading to ifile.it via API is very simple process consisting of two steps:
  1. Determine upload url, we discover which upload server (if any) is accepting uploads
  1. We upload the file via HTTP POST request to the upload url fetched in step 1 above

<br><br>
<hr />

<h3>Step1 - Determine upload url</h3>
<b>Request URL</b>
<pre><code>http://ifile.it/api-fetch_upload_url.api<br>
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
<tr><td> server_id             </td><td> int         </td><td>                        </td><td> The unique id of the server,<br>example: i<b>71</b>.ifile.it </td></tr>
<tr><td> upload_url            </td><td> string      </td><td>                        </td><td> The url to which you can upload your file (see step 2 below)<br>example: http://i<b>71</b>.ifile.it/upload </td></tr></tbody></table>

<br><br><br>
<hr />

<h3>Step2 - Upload file</h3>
<b>Request URL</b>
<pre><code>http://i123.ifile.it/upload<br>
</code></pre>
Where the request URL is determined in step 1 above<br>
<br>
<br>
<br>
<b>HTTP GET parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>optional</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>default value</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> response              </td><td> yes             </td><td> string      </td><td> json<br />text         </td><td> json                 </td><td> In what format the API response should be </td></tr></tbody></table>

<br>
<br>
<b>HTTP POST parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>optional</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>default value</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> Filedata              </td><td> no              </td><td> string      </td><td>                        </td><td>                      </td><td> The file to upload </td></tr>
<tr><td> akey                  </td><td> yes             </td><td> string      </td><td>                        </td><td>                      </td><td> apikey of the account to which this file is to be added to (see <a href='FetchApikey.md'>FetchApikey</a>) </td></tr></tbody></table>

Please note: if you do not provide an "akey" as a POST parameter then the file will be uploaded as anonymous user and not attached to an account<br>
<br>
<br>
<br>
<b>API response parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> status                </td><td> string      </td><td> ok<br>error            </td><td> Whether the request was successful, error message parameter shown on error </td></tr>
<tr><td> ukey                  </td><td> string      </td><td>                        </td><td> The unique identifier for a file (what is <a href='Ukey.md'>Ukey</a> ?) </td></tr>
<tr><td> name                  </td><td> string      </td><td>                        </td><td> Name for the file uploaded </td></tr>
<tr><td> size                  </td><td> int         </td><td>                        </td><td> File size in bytes </td></tr>
<tr><td> mime                  </td><td> string      </td><td>                        </td><td> File <a href='http://en.wikipedia.org/wiki/MIME'>mimetype</a> </td></tr>
<tr><td> md5                   </td><td> string      </td><td>                        </td><td> File <a href='http://en.wikipedia.org/wiki/Md5sum'>md5</a> checksum </td></tr></tbody></table>

<br><br><br>
<hr />
<h3>Sample Code in PHP</h3>
Using the official PHP api wrapper, see <a href='http://code.google.com/p/ifileit/downloads/list'>Downloads</a>
<pre><code>&lt;?php<br>
<br>
/**<br>
 * this example code snipppet tries to upload a file<br>
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
//test filepath to the file to upload<br>
$filepath	=	'/PATH/TO/test.file';<br>
<br>
<br>
<br>
<br>
<br>
<br>
try {<br>
	<br>
	$upload = $IfileApi-&gt;upload(<br>
		$filepath<br>
	);<br>
	<br>
	print 'uploaded: http://ifile.it/'.$upload['ukey'].'/'.rawurlencode( $upload['name'] )."\n\n";<br>
	<br>
	//output our response response array to see its structure<br>
	print print_r( $upload,true );<br>
	<br>
}<br>
catch ( IfileApiException $e){<br>
	<br>
	print 'IfileApiException &gt; '.$e-&gt;getMessage();<br>
}<br>
<br>
?&gt;<br>
</code></pre>