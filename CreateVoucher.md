# Introduction #

This call (ONLY WORKS FOR RESELLER ACCOUNTS!) lets your creates a premium voucher using your reseller balance. Your account balance needs to be higher than the value of the voucher you are issuing.


<br><br>
<hr />

<h3>Create Voucher</h3>
<b>Request URL</b>
<pre><code>http://ifile.it/api-create_voucher.api<br>
</code></pre>

<br>
<br>
<b>HTTP GET parameters</b>
none<br>
<br>
<br>
<br>
<b>HTTP POST parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>optional</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>default value</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> akey                  </td><td> no              </td><td> string      </td><td>                        </td><td>                      </td><td> apikey for a users account (see <a href='FetchApikey.md'>FetchApikey</a>) </td></tr>
<tr><td> duration              </td><td> no              </td><td> int         </td><td> 30<br>60<br>90<br>180  </td><td> none                 </td><td> Duration of the premium voucher </td></tr></tbody></table>

<br>
<br>
<b>API response parameters</b>
<table><thead><th> <b>parameter name</b> </th><th> <b>type</b> </th><th> <b>possible values</b> </th><th> <b>description</b> </th></thead><tbody>
<tr><td> status                </td><td> string      </td><td> ok<br>error            </td><td> Whether the request was successful, error message parameter shown on error </td></tr>
<tr><td> voucher_code          </td><td> string      </td><td>                        </td><td> premium voucher code </td></tr></tbody></table>



<br><br><br>
<hr />
<h3>Sample Code in PHP</h3>
Using the official PHP api wrapper, see <a href='http://code.google.com/p/ifileit/downloads/list'>Downloads</a><?php

/**
 * this example code snipppet creates a voucher (reseller accounts only!)
 */

//set error reporting and include our api class
error_reporting(E_ALL); ini_set( 'display_errors', 'On' );
require_once( 'IfileApi.php' ); //in same directory as this example script


//create api model
$IfileApi = new IfileApi();


$duration = 30; //voucher duration, 30,60,90,180 days



//username and pass for an account for which you wish to get the apikey
$username = 'USERNAME';
$password = 'PASSWORD';





//login and get api key
try {
	
	$apikey = $IfileApi->fetchApiKey($username, $password);
	
	print 'the apikey for @'.$username .' is: '.$apikey."\n\n";
}
catch ( IfileApiException $e){
	
	print 'IfileApiException > '.$e->getMessage();
}



//issue voucher
try {
	
	$response = $IfileApi->post(
		'http://ifile.it/api-create_voucher.api',
		array(
			'akey'		=>	$apikey,
			'duration'	=>	$duration
		)
	);
	
	$voucherCode = $response['voucher_code'];
	
	print 'voucher code: '. $voucherCode;
}
catch ( IfileApiException $e){
	
	print 'IfileApiException > '.$e->getMessage();
}







//output our response response array to see its structure
print print_r( $response,true );



?>}}}</code></pre>