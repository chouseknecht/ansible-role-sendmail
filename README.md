Role Name
=========

Quick and easy way to send an email message from a Tower, Jenkins or any job stream.

Requirements
------------
Requirs v2 of the mail module. If you are not running v2 of ansible, you can install v2 of the mail module. Create a `library` directory in the path where you run playbooks, and download a copy of the [latest mail module](https://github.com/ansible/ansible-modules-extras/tree/devel/notification) to `library/mail.py`. 

Role Variables
--------------

All of the mail module parameters have been turned into variables.

SMTP server connection.

    sendmail_host: smtp.google.com
    sendmail_port: 587
    sendmail_username: "email_address@gmail.com"
    sendmail_password: "password1!"

Construct the email message.

    sendmail_to: "foo@companydomain.com"
    sendmail_cc: "bar@companydomain.com, baz@companydomain.com"
    sendmail_from: "admin@companydomain.com"
    sendmail_subject: "The upgrade process complete!"
    sendmail_body: {{ lookup('file','/tmp/email_body.txt') }} 

Provide a path to a temporary file space the user running the playbook can write to. Defaults to '/tmp'.

    sendmail_tmp: "/home/username"

Add any optional special headers

    sendmail_headers: "Reply-To=john@example.com|X-Special='Something or other'"

Set the character set. Defaults to 'utf8'.    

    sendmail_charset: 'us-ascii'

Set the type of message - text or html. Defaults to html.

    sendmail_subtype: html

Provide an optional space separated list of file attachments.

    sendmail_attachments: "/etc/group /tmp/pavatar2.png"


Dependencies
------------
None.

Example Playbook
----------------
A simple playbook to send an email:

    # sendmail.yml
    ---
    - name: Sending email
      hosts: local
      roles:
      - { role: sendmail }

Run the playbook with something like:

    ansible-playbook sendmail.yml -i inventory.txt -e "@vars.yml"

License
-------

MIT

Author Information
------------------

Thanks for checking out ansible-role-sendmail. Hopefully it makes sending email messages from your job streams super easy.

For questions, comments suggestions please open an issue here or add a review at [Ansible Galaxy](http://galaxy.ansible.com).
