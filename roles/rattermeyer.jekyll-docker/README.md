Jekyll Docker
=============

This role creates a docker image with Jekyll and an alias to run jekyll from the command line.

Requirements
------------

Docker must be installed. This role does not declare a direct dependency on
a docker role.

Role Variables
--------------

More or less all the listed variables should be treated as mandatory.
Setting these correctly enables running `jekyll` in user home directoy
without mangling with directory ownership.
It ensures that in the docker container jekyll is run with same user and group id
as on the host.
```
# the user name is a mandatory role variable that must be specified
user_name: richard
user_id: 1001
group_name: "{{user_name}}"
group_id: 1001
```

Dependencies
------------

Currently none.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: localhost
      roles:
         - { role: jekyll-docker, user_name: richard, user_id: 1001, group_name: richard, group_id: 1001, become: true, become_user: richard }

License
-------

BSD

Author Information
------------------
Richard Attermeyer

* [Blog](http://www.rattermyer.de)
* [Github](https://github.com/rattermeyer)
* [Twitter](https://twitter.com/rattermeyer)
