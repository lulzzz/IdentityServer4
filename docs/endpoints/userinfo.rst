UserInfo Endpoint
=================

The UserInfo endpoint can be used to retrieve identity information about a user (see `spec <http://openid.net/specs/openid-connect-core-1_0.html#UserInfo>`_). 

The caller needs to send a valid access token representing the user.
Depending on the granted scopes, the UserInfo endpoint will return the mapped claims (at least the `openid` scope is required).

Example
^^^^^^^

::

    GET /connect/userinfo
    Authorization: Bearer <access_token>

::

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "sub": "248289761001",
        "name": "Bob Smith",
        "given_name": "Bob",
        "family_name": "Smith",
        "role": [
            "user",
            "admin"
        ]
    }

IdentityModel
^^^^^^^^^^^^^
You can programmatically access the userinfo endpoint using the `IdentityModel <https://github.com/IdentityModel/IdentityModel2>`_ library::

    var userInfoClient = new UserInfoClient(doc.UserInfoEndpoint, token);

    var response = await userInfoClient.GetAsync();
    var claims = response.Claims;