---
title: Gists API v3 | developer.github.com
---

# Gists API

The Gist API v3 has been unified into the core GitHub API and can be
accessed via the domain api.github.com. SSL is required so the base url
for all API calls should be: `https://api.github.com`.
Please see the [summary](/v3/) for a complete description of the API
including information about data format and authentication.

## List a user's gists

    GET /users/:user/gists.json

### Response

<%= headers 200, :pagination => true %>
<%= json(:gist) { |h| [h] } %>

## Get a single gist

   GET /gists/:id.json

### Response

<%= headers 200 %>
<%= json :full_gist %>

## Create a new gist

    POST /users/:user/gists.json

### Input

<%= json \
  :description => "the description for this gist",
  :public      => true,
  :files => {
    "file1.txt" => {"content" => "String file contents"}
  } %>

### Response

<%= headers 201,
      :Location => "https://api.github.com/users/:user/gists/1.json" %>
<%= json :full_gist %>

## Edit a gist

    PATCH /gists/:id.json

<%= json \
  :description => "the description for this gist",
  :files => {
    "file1.txt" => {"content" => "String file contents"}
  } %>

### Response

<%= headers 200 %>
<%= json :full_gist %>

## Star a gist

    POST /gists/:id/star

### Response

<%= headers 201 %>
<%= json({}) %>

## Unstar a gist

    DELETE /gists/:id/star

### Response

<%= headers 200 %>
<%= json({}) %>

## Check if a gist is starred

    GET /gists/:id/star

### Response if gist is starred

<%= headers 204 %>

### Response if gist is not starred

<%= headers 404 %>
<%= json({}) %>

## Fork a gist

    POST /gists/:id/fork.json

### Response

<%= headers 201 %>
<%= json(:gist) %>

## Delete a gist

   DELETE /gists/:id.json

### Response

<%= headers 204 %>