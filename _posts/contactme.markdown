---
layout: post
title: 'Rails 5.2.0 FINAL: Active Storage, Redis Cache Store, HTTP/2 Early Hints, CSP, Credentials'
categories: releases
author: dhh
published: true
date: 2018-04-09 12:00:00 -09:00
---
Nearly 14 years since [the first public version of Rails](http://blade.nagaokaut.ac.jp/cgi-bin/scat.rb/ruby/ruby-talk/107370), it's our pleasure to release yet another major upgrade to the framework in the form of 5.2.0 final. We've been diligently polishing Active Storage and the other big new components for stable release, and it's great to see so many applications already running the release candidates in production. [Basecamp](https://basecamp.com) and [Shopify](https://shopify.com) have both been running Rails 5.2.0 for quite a while.

This release comes just in time for [RailsConf](https://railsconf.com/), which features sessions on the new [encrypted credentials](https://railsconf.com/program/sessions#session-627), [a code review of Active Storage](https://railsconf.com/program/sessions#session-562), [advice on how to upgrade to a new Rails version](https://railsconf.com/program/sessions#session-588), and a [lot](https://railsconf.com/program/sessions#session-552) [of](https://railsconf.com/program/sessions#session-568) [Webpack](https://railsconf.com/program/sessions#session-549) talks.

You can read in even more detail about everything that's [new in Rails 5.2 in the newly finished release notes](http://edgeguides.rubyonrails.org/5_2_release_notes.html).

Note that [rails/master](https://github.com/rails/rails) development is now targeting Rails 6.0.

Many thanks to Rails core, Rails contributors, and everyone else who've helped with code, documentation, bug reports, and whatever else to get Rails 5.2.0 out the door. It's amazing to have [over 400 code contributors](http://contributors.rubyonrails.org/releases/5-2-0/contributors) with fingerprints on this release.

## Feature highlights

It’s been too hard to deal with file uploads in Rails for too long. Sure, there’s been a lot of fine plugins available,
but it was overdue that we incorporated something right into the framework. So now we have!

With the new [Active Storage](https://github.com/rails/rails/blob/d3893ec38ec61282c2598b01a298124356d6b35a/activestorage/README.md)
framework in Rails 5.2, we’ve solved for the modern approach of uploading files straight to the cloud. Out of the box,
there’s support for Amazon’s S3, Google’s Cloud Storage, and Microsoft Azure Cloud File Storage.

If you’re dealing with images, you can create variants on the fly. If you’re dealing with videos or PDFs, you can create
previews on the fly. And regardless of the type, you can analyze uploads for metadata extraction asynchronously.

Active Storage was extracted from Basecamp 3 by George Claghorn and yours truly. So not only is the framework already
used in production, it was born from production. There’s that Extraction Design guarantee stamp alright!


Speaking of extractions, Jeremy Daer has untangled the long jungle twine of hacks we were using at Basecamp to employ
Redis for general partial, fragment, and other Rails caching jobs. There’s a sparkling new [Redis Cache Store](https://github.com/rails/rails/pull/31134)
that incorporates all those years of veteran hacks into a cohesive unit that anyone can use.

This new Redis Cache Store supports Redis::Distributed, for Memcached-like sharding across Redises. It’s fault tolerant,
so will treat failures like misses, rather than kill the request with an exception. It even supports distributed MGETs
for that full partial collection caching goodness.

This comes together with a massive leap forward for cache efficiency with [key recycling](https://github.com/rails/rails/pull/29092)
and [compression](https://github.com/rails/rails/pull/31147) both available by default. For Basecamp, it meant improving
the cache lifetime by two orders of magnitude! We went from having caches trashed in as little as a day to having
caches last for months. If you’re using partial caching and the nesting doll strategy, your cache lifetime will improve
dramatically between these two changes.


We’ve also embraced the cherry of HTTP/2 with [early hints](https://github.com/rails/rails/pull/30744) through the work
of Aaron Patterson and Eileen Uchitelle. This means we can automatically instruct the web server to send required style
sheet and JavaScript assets early. Which means faster full page delivery, as who wouldn’t want that?


On the topic of performance, Rails now ships with [Bootsnap](https://github.com/Shopify/bootsnap) in the default `Gemfile`, created by our friends at Shopify. It generally reduces application boot times by over 50%.


Rails has always been in the forefront of making your web applications more secure, leading the way with built-in CSRF
and XSS protection and we've enhanced that further in Rails 5.2 with [the addition of a new DSL](https://github.com/rails/rails/pull/31162)
that allows you to configure a [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)
for your application. You can configure a global default policy and then override it on a per-resource basis and even
use lambdas to inject per-request values into the header such as account subdomains in a multi-tenant application.


But it’s not all just new starry-eyed wonders. In Rails 5.1, we added [encrypted secrets](https://github.com/rails/rails/pull/28038).
These secrets were like the old secrets but, uhm, more secret, because, you know, ENCRYPTION! Confusing? Yes. Why would
you want secrets that weren’t really secret? Well, you don’t.

In Rails 5.2, we’ve rectified the mess by deprecating the two different kinds of secrets and introduced a new shared
concept called [Credentials](https://github.com/rails/rails/pull/30067). Credentials, like AWS access keys and other forms of logins and passwords, were the dominant
use case for secrets, so why not just call a spade a spade. So spade it is!

Credentials are always encrypted. This means they’re safe to check into revision control, as long as you keep the key
out of it. That means atomic deploys, no need to mess with a flurry of environment variables, and other benefits of having all
credentials that the app needs in one place, safe and secure.

In addition, we’ve opened up the API underlying Credentials, so you can easily deal with other encrypted configurations,
keys, and files.

Since Rails 5.1, we’ve also made great strides with [Webpacker](https://github.com/rails/webpacker). So Rails 5.2 is
meant to pair beautifully with the new Webpacker 3.0 release. Rails has fully embraced modern JavaScript with a
pre-configured build pipeline run by Webpack. We keep strengthening that relationship.
