## Project Description ##

Project page explaining how the [ifile.it](http://ifile.it/) HTTP based API works

With examples and links to other projects and code making use of the ifile.it api (September 2011 api version on)

Using the API is a matter of sending HTTP requests to API endpoint URLs (as linked below) with the correct HTTP [POST](http://en.wikipedia.org/wiki/POST_(HTTP)) and/or [GET](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods) parameters in the request, the response is a [JSON](http://www.json.org/) encoded array of values in all cases, which you can use in your applications and/or subsequent requests to the API.

**please note:** Most of the API calls require you to send your apikey as part of the request in order to authenticate you as a site user, getting the apikey belonging to an account is easy, see [FetchApikey](FetchApikey.md) for more details

<br><br>
<hr />
<h2>Key Downloads</h2>

<ul><li><a href='http://code.google.com/p/ifileit/downloads/detail?name=ifileapi_2011-12-02.zip&can=2&q='>Official PHP5 class and examples (2011-12-02) </a> This sample code contains a Wrapper class written in PHP5 making use of the php curl extension, along with various examples</li></ul>

<br><br>
<hr />
<h2>Available API functionality explained</h2>
API functionality is grouped into the following sections<br>
<br>
<b>account</b>
<ul><li><a href='FetchApikey.md'>FetchApikey</a> - Retrieving your apikey / authenticating subsequent requests<br>
</li><li><a href='FetchAccountInfo.md'>FetchAccountInfo</a> - Retrieve account information and statistics</li></ul>

<b>site</b>
<ul><li><a href='Ping.md'>Ping</a> - Checking whether the API/site is available<br>
</li><li><a href='Uploading.md'>Uploading</a> - Uploading<br>
</li><li><a href='FetchDownloadUrl.md'>FetchDownloadUrl</a> - Requesting download ticket URL (available to premium/tester/vip accounts only)</li></ul>

<b>files</b>
<ul><li><a href='CheckFileStatus.md'>CheckFileStatus</a> - Checking whether a file is downloadable or not (and why)<br>
</li><li><a href='FetchFileInfo.md'>FetchFileInfo</a> - Retrieve detailed information about your file</li></ul>

<b>folders</b>
<i>to do</i>

<b>vouchers</b> (available to reseller accounts only)<br>
<ul><li><a href='CreateVoucher.md'>CreateVoucher</a> - Create a premium voucher using your reseller account balance</li></ul>


<br><br>
<hr />
<h2>Questions?</h2>
Address any enquiries about the API to <a href='http://ifile.it/help-contact.html'>ifile.it admin and support</a>. Please insert API into subject line of any communication in order to get priority!<br>
<br>
<br><br>
<h2>3rd party api usage examples</h2>
<ul><li><a href='http://facundoolano.wordpress.com/category/ifile-it/'>Python </a>
</li><li><a href='http://code.google.com/p/ifileit/downloads/detail?name=ifile.zip&can=2&q='>Bash</a>