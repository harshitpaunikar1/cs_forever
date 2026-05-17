Title: RFC 9110: HTTP Semantics
Mapped Topic: HTTP semantics
Source URL: https://www.rfc-editor.org/rfc/rfc9110.html
Source Type: official_standard
Trust Score: 99
Fetched At: 2026-04-17T07:08:09+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

###
[6.4. ](https://www.rfc-editor.org#section-6.4)[Content](https://www.rfc-editor.org#name-content)

HTTP messages often transfer a complete or partial representation as the
message "content": a stream of octets sent after the header
section, as delineated by the message framing.[¶](https://www.rfc-editor.org#section-6.4-1)

This abstract definition of content reflects the data after it has been
extracted from the message framing. For example, an HTTP/1.1 message body
([Section 6](https://www.rfc-editor.org/rfc/rfc9112#section-6) of [[HTTP/1.1](https://www.rfc-editor.org#HTTP11)]) might consist of a stream of data encoded
with the chunked transfer coding -- a sequence of data chunks, one
zero-length chunk, and a trailer section -- whereas
the content of that same message
includes only the data stream after the transfer coding has been decoded;
it does not include the chunk lengths, chunked framing syntax, nor the
trailer fields ([Section 6.5](https://www.rfc-editor.org#trailer.fields)).[¶](https://www.rfc-editor.org#section-6.4-2)

####
[6.4.1. ](https://www.rfc-editor.org#section-6.4.1)[Content Semantics](https://www.rfc-editor.org#name-content-semantics)

The purpose of content in a request is defined by the method semantics
([Section 9](https://www.rfc-editor.org#methods)).[¶](https://www.rfc-editor.org#section-6.4.1-1)

For example, a representation in the content of a PUT request
([Section 9.3.4](https://www.rfc-editor.org#PUT)) represents the desired state of the
[target resource](https://www.rfc-editor.org#target.resource) after the request is successfully applied,
whereas a representation in the content of a POST request
([Section 9.3.3](https://www.rfc-editor.org#POST)) represents information to be processed by the
target resource.[¶](https://www.rfc-editor.org#section-6.4.1-2)

In a response, the content's purpose is defined by the request method,
response status code ([Section 15](https://www.rfc-editor.org#status.codes)), and response
fields describing that content.
For example, the content of a [200 (OK)](https://www.rfc-editor.org#status.200) response to GET
([Section 9.3.1](https://www.rfc-editor.org#GET)) represents the current state of the
[target resource](https://www.rfc-editor.org#target.resource), as observed at the time of the message
origination date ([Section 6.6.1](https://www.rfc-editor.org#field.date)), whereas the content of
the same status code in a response to POST might represent either the
processing result or the new state of the target resource after applying
the processing.[¶](https://www.rfc-editor.org#section-6.4.1-3)

The content of a [206 (Partial Content)](https://www.rfc-editor.org#status.206) response to GET
contains either a single part of the selected representation or a
multipart message body containing multiple parts of that representation,
as described in [Section 15.3.7](https://www.rfc-editor.org#status.206).[¶](https://www.rfc-editor.org#section-6.4.1-4)

Response messages with an error status code usually contain content that
represents the error condition, such that the content describes the
error state and what steps are suggested for resolving it.[¶](https://www.rfc-editor.org#section-6.4.1-5)

Responses to the HEAD request method ([Section 9.3.2](https://www.rfc-editor.org#HEAD)) never include
content; the associated response header fields indicate only
what their values would have been if the request method had been GET
([Section 9.3.1](https://www.rfc-editor.org#GET)).[¶](https://www.rfc-editor.org#section-6.4.1-6)

[2xx (Successful)](https://www.rfc-editor.org#status.2xx) responses to a CONNECT request method
([Section 9.3.6](https://www.rfc-editor.org#CONNECT)) switch the connection to tunnel mode instead of
having content.[¶](https://www.rfc-editor.org#section-6.4.1-7)

All [1xx (Informational)](https://www.rfc-editor.org#status.1xx), [204 (No Content)](https://www.rfc-editor.org#status.204), and
[304 (Not Modified)](https://www.rfc-editor.org#status.304) responses do not include content.[¶](https://www.rfc-editor.org#section-6.4.1-8)

All other responses do include content, although that content
might be of zero length.[¶](https://www.rfc-editor.org#section-6.4.1-9)

####
[6.4.2. ](https://www.rfc-editor.org#section-6.4.2)[Identifying Content](https://www.rfc-editor.org#name-identifying-content)

When a complete or partial representation is transferred as message
content, it is often desirable for the sender to supply, or the recipient
to determine, an identifier for a resource corresponding to that specific
representation. For example, a client making a GET request on a resource
for "the current weather report" might want an identifier specific to the
content returned (e.g., "weather report for Laguna Beach at 20210720T1711").
This can be useful for sharing or bookmarking content from resources that
are expected to have changing representations over time.[¶](https://www.rfc-editor.org#section-6.4.2-1)

For a request message:[¶](https://www.rfc-editor.org#section-6.4.2-2)

- If the request has a
[Content-Location](https://www.rfc-editor.org#field.content-location)header field, then the sender asserts that the content is a representation of the resource identified by the Content-Location field value. However, such an assertion cannot be trusted unless it can be verified by other means (not defined by this specification). The information might still be useful for revision history links.[¶](https://www.rfc-editor.org#section-6.4.2-3.1) - Otherwise, the content is unidentified by HTTP, but a more specific
identifier might be supplied within the content itself.
[¶](https://www.rfc-editor.org#section-6.4.2-3.2)

For a response message, the following rules are applied in order until a
match is found:[¶](https://www.rfc-editor.org#section-6.4.2-4)

- If the request method is HEAD or the response status code is
[204 (No Content)](https://www.rfc-editor.org#status.204)or[304 (Not Modified)](https://www.rfc-editor.org#status.304), there is no content in the response.[¶](https://www.rfc-editor.org#section-6.4.2-5.1) - If the request method is GET and the response status code is
[200 (OK)](https://www.rfc-editor.org#status.200), the content is a representation of the[target resource](https://www.rfc-editor.org#target.resource)([Section 7.1](https://www.rfc-editor.org#target.resource)).[¶](https://www.rfc-editor.org#section-6.4.2-5.2) - If the request method is GET and the response status code is
[203 (Non-Authoritative Information)](https://www.rfc-editor.org#status.203), the content is a potentially modified or enhanced representation of the[target resource](https://www.rfc-editor.org#target.resource)as provided by an intermediary.[¶](https://www.rfc-editor.org#section-6.4.2-5.3) - If the request method is GET and the response status code is
[206 (Partial Content)](https://www.rfc-editor.org#status.206), the content is one or more parts of a representation of the target resource.[¶](https://www.rfc-editor.org#section-6.4.2-5.4) - If the response has a
[Content-Location](https://www.rfc-editor.org#field.content-location)header field and its field value is a reference to the same URI as the target URI, the content is a representation of the target resource.[¶](https://www.rfc-editor.org#section-6.4.2-5.5) - If the response has a
[Content-Location](https://www.rfc-editor.org#field.content-location)header field and its field value is a reference to a URI different from the target URI, then the sender asserts that the content is a representation of the resource identified by the Content-Location field value. However, such an assertion cannot be trusted unless it can be verified by other means (not defined by this specification).[¶](https://www.rfc-editor.org#section-6.4.2-5.6) - Otherwise, the content is unidentified by HTTP, but a more specific
identifier might be supplied within the content itself.
[¶](https://www.rfc-editor.org#section-6.4.2-5.7)

## 5.6.5. Comments

Comments can be included in some HTTP fields by surrounding the comment text with parentheses. Comments are only allowed in fields containing "comment" as part of their field value definition.¶
