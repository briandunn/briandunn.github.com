---
layout: post
title: writing an HTTP response to a file as it is read (in ruby)
---
You have yourself a URI.

<macro:code lang="ruby">URI.parse("http://theophil.us")</macro:code>

You probably know how to grab a file via GET with ruby:

<macro:code lang="ruby">Net::HTTP.get(target)</macro:code>

But what if the result is HUGE, like say, 300mb of xml? you probably want to flush the response to disk as it is handed to you, like this: (not immediately obvious to me from the "docs":http://www.ruby-doc.org/core/classes/Net/HTTP.html)

<macro:code lang="ruby">
  def write_to_file(target, file_name)
    Net::HTTP.start(target.host, target.port) do |http|
      File.open( file_name, 'w') do |file|
        http.request_get(target.request_uri) do |response|
          response.read_body do |body|
            file.write(body)
          end
        end
      end
    end
  end
</macro:code>
