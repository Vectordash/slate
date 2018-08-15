# Errors

<!--
<aside class="notice">
This error section is stored in a separate file in <code>includes/_errors.md</code>. Slate allows you to optionally separate out your docs into many files...just save them to the <code>includes</code> folder and add them to the top of your <code>index.md</code>'s frontmatter. Files are included in the order listed.
</aside>

The Kittn API uses the following error codes:
-->

The Vectordash API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API token is wrong.
403 | Forbidden -- The object requested is hidden for administrators only.
404 | Not Found -- The specified object could not be found.
405 | Method Not Allowed -- You tried to access an object with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
407 | Incomplete Profile -- Some part of your profile needs updating to access this resource
410 | Gone -- The object requested has been removed from our servers.
429 | Too Many Requests -- You're requesting too many objects! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
504 | GPU Unavailable -- We don't currently have the GPU you requested available for rent.
