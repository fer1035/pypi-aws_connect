=====================
**aws-authenticator**
=====================

Overview
--------

Login to AWS using CLI named profiles, IAM access key credentials, or SSO.

Prerequisites
-------------

- *Python >= 3.6*
- *aws-ssooidc (https://pypi.org/project/aws-ssooidc/) >= 2021.1.1.1*
- *boto3 (https://pypi.org/project/boto3/) >= 1.17.78*

Conditional Arguments
---------------------

If authenticating with named profiles:

- AWSCLI profile name

If authenticating with IAM acccess key credentials:

- AWS access key id
- AWS secret access key

If authenticating with SSO:

- AWS account ID
- AWS SSO Permission Set (role) name
- AWS SSO login URL

Usage
-----

Installation:

.. code-block:: BASH

   pip3 install aws-authenticator
   # or
   python3 -m pip install aws-authenticator

In Python3 authenticating with named profiles:

.. code-block:: PYTHON

   import aws_authenticator

   auth = aws_authenticator.AWSAuthenticator(
      profile_name="<profile-name>",
   )
   session = auth.profile()
   client = session.client("<client-name>")

In Python3 authenticating with IAM access key credentials:

.. code-block:: PYTHON

   import aws_authenticator

   auth = aws_authenticator.AWSAuthenticator(
      access_key_id="<access-key-id>",
      secret_access_key="<secret-access-key>",
   )
   session = auth.iam()
   client = session.client("<client-name>")

In Python3 authenticating with SSO:

.. code-block:: PYTHON

   import aws_authenticator

   auth = aws_authenticator.AWSAuthenticator(
      sso_url="<sso-url>",
      sso_role_name="<sso-role-name>",
      ssp_account_id="<ssp-account-id>",
   )
   session = auth.sso()
   client = session.client("<client-name>")

Testing profile-based login as a script in BASH:

.. code-block:: BASH

   python [/path/to/]aws_authenticator \
   -m profile \
   -p <profile-name>
