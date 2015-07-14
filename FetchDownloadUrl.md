## Introduction ##

Users with premium/tester/vip accounts can request download tickets via this API calls, one can the download from the download ticket URL.

This call will be available to users with premium accounts when the premium account system is done, in the meantime it is only available to beta/vip account holders.

<br><br>
<hr />

<h3>Get download ticket url</h3>
<b>Request URL</b>
<pre><code>http://ifile.it/api-fetch_download_url.api<br>
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
<tr><td> download_url          </td><td> string      </td><td>                        </td><td> Download ticket URL </td></tr></tbody></table>


One can then download from the download ticket URL.<br>
<br>
You could use wget or curl or whatever method you wish to download files available on your platform and/or programming language of choice<br>
<br>
Please note:<br>
<ul><li>Download ticket URLs are only valid for 24 hours from time of issue<br>
</li><li>Download ticket URLs are restricted to the network from which the ticket was requested.