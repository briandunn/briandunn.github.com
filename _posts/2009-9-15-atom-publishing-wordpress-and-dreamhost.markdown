---
layout: post
title: Atom Publishing, Wordpress, and Dreamhost
---
I've been working on automating the system my "church":http://tulsachristianfellowship.com uses for publishing "sermons":http://tcf.theophil.us.  When trying to publish podcast entries via WordPress Atom support, I discovered an issue with Dreamhost and http basic auth described "here":http://www.besthostratings.com/articles/http-auth-php-cgi.html.

As you can see, his solution requires both some ModRewrite love and some PHP script changes.  Well those lovely fellas on the Wordpress team already picked up their end of the deal, so all I ended up having to do is add this segment to the <code>.htaccess</code> file in the root of my WordPress installation.

<macro:code lang="apache">
<IfModule mod_rewrite.c>
RewriteEngine on
RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization},L]
</IfModule
</macro:code>

Now I can automagically publish sermons from my command line.  I feel a power trip coming on.
