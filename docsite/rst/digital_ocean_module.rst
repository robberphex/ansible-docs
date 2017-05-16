.. _digital_ocean:


digital_ocean - Create/delete a droplet/SSH_key in DigitalOcean
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. versionadded:: 1.3


.. contents::
   :local:
   :depth: 1


Synopsis
--------

Create/delete a droplet in DigitalOcean and optionally wait for it to be 'running', or deploy an SSH key.


Requirements (on host that executes module)
-------------------------------------------

  * python >= 2.6
  * dopy


Options
-------

.. raw:: html

    <table border=1 cellpadding=4>
    <tr>
    <th class="head">parameter</th>
    <th class="head">required</th>
    <th class="head">default</th>
    <th class="head">choices</th>
    <th class="head">comments</th>
    </tr>
            <tr>
    <td>api_token<br/><div style="font-size: small;"> (added in 1.9.5)</div></td>
    <td>no</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>DigitalOcean api token.</div></td></tr>
            <tr>
    <td>backups_enabled<br/><div style="font-size: small;"> (added in 1.6)</div></td>
    <td>no</td>
    <td>no</td>
        <td><ul><li>yes</li><li>no</li></ul></td>
        <td><div>Optional, Boolean, enables backups for your droplet.</div></td></tr>
            <tr>
    <td>command<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td>droplet</td>
        <td><ul><li>droplet</li><li>ssh</li></ul></td>
        <td><div>Which target you want to operate on.</div></td></tr>
            <tr>
    <td>id<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>Numeric, the droplet id you want to operate on.</div></td></tr>
            <tr>
    <td>image_id<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>This is the slug of the image you would like the droplet created with.</div></td></tr>
            <tr>
    <td>ipv6<br/><div style="font-size: small;"> (added in 2.2)</div></td>
    <td>no</td>
    <td>no</td>
        <td><ul><li>yes</li><li>no</li></ul></td>
        <td><div>Optional, Boolean, enable IPv6 for your droplet.</div></td></tr>
            <tr>
    <td>name<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>String, this is the name of the droplet - must be formatted by hostname rules, or the name of a SSH key.</div></td></tr>
            <tr>
    <td>private_networking<br/><div style="font-size: small;"> (added in 1.4)</div></td>
    <td>no</td>
    <td>no</td>
        <td><ul><li>yes</li><li>no</li></ul></td>
        <td><div>Bool, add an additional, private network interface to droplet for inter-droplet communication.</div></td></tr>
            <tr>
    <td>region_id<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>This is the slug of the region you would like your server to be created in.</div></td></tr>
            <tr>
    <td>size_id<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>This is the slug of the size you would like the droplet created with.</div></td></tr>
            <tr>
    <td>ssh_key_ids<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>Optional, array of of SSH key (numeric) ID that you would like to be added to the server.</div></td></tr>
            <tr>
    <td>ssh_pub_key<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>The public SSH key you want to add to your account.</div></td></tr>
            <tr>
    <td>state<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td>present</td>
        <td><ul><li>present</li><li>active</li><li>absent</li><li>deleted</li></ul></td>
        <td><div>Indicate desired state of the target.</div></td></tr>
            <tr>
    <td>unique_name<br/><div style="font-size: small;"> (added in 1.4)</div></td>
    <td>no</td>
    <td>no</td>
        <td><ul><li>yes</li><li>no</li></ul></td>
        <td><div>Bool, require unique hostnames.  By default, DigitalOcean allows multiple hosts with the same name.  Setting this to "yes" allows only one host per name.  Useful for idempotence.</div></td></tr>
            <tr>
    <td>user_data<br/><div style="font-size: small;"> (added in 2.0)</div></td>
    <td>no</td>
    <td>None</td>
        <td><ul></ul></td>
        <td><div>opaque blob of data which is made available to the droplet</div></td></tr>
            <tr>
    <td>virtio<br/><div style="font-size: small;"> (added in 1.4)</div></td>
    <td>no</td>
    <td>yes</td>
        <td><ul><li>yes</li><li>no</li></ul></td>
        <td><div>Bool, turn on virtio driver in droplet for improved network and storage I/O.</div></td></tr>
            <tr>
    <td>wait<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td>yes</td>
        <td><ul><li>yes</li><li>no</li></ul></td>
        <td><div>Wait for the droplet to be in state 'running' before returning.  If wait is "no" an ip_address may not be returned.</div></td></tr>
            <tr>
    <td>wait_timeout<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td>300</td>
        <td><ul></ul></td>
        <td><div>How long before wait gives up, in seconds.</div></td></tr>
        </table>
    </br>



Examples
--------

 ::

    # Ensure a SSH key is present
    # If a key matches this name, will return the ssh key id and changed = False
    # If no existing key matches this name, a new key is created, the ssh key id is returned and changed = False
    
    - digital_ocean:
        state: present
        command: ssh
        name: my_ssh_key
        ssh_pub_key: 'ssh-rsa AAAA...'
        api_token: XXX
    
    # Create a new Droplet
    # Will return the droplet details including the droplet id (used for idempotence)
    
    - digital_ocean:
        state: present
        command: droplet
        name: mydroplet
        api_token: XXX
        size_id: 2gb
        region_id: ams2
        image_id: fedora-19-x64
        wait_timeout: 500
    
      register: my_droplet
    
    - debug: msg="ID is {{ my_droplet.droplet.id }}"
    - debug: msg="IP is {{ my_droplet.droplet.ip_address }}"
    
    # Ensure a droplet is present
    # If droplet id already exist, will return the droplet details and changed = False
    # If no droplet matches the id, a new droplet will be created and the droplet details (including the new id) are returned, changed = True.
    
    - digital_ocean:
        state: present
        command: droplet
        id: 123
        name: mydroplet
        api_token: XXX
        size_id: 2gb
        region_id: ams2
        image_id: fedora-19-x64
        wait_timeout: 500
    
    # Create a droplet with ssh key
    # The ssh key id can be passed as argument at the creation of a droplet (see ssh_key_ids).
    # Several keys can be added to ssh_key_ids as id1,id2,id3
    # The keys are used to connect as root to the droplet.
    
    - digital_ocean:
        state: present
        ssh_key_ids: 123,456
        name: mydroplet
        api_token: XXX
        size_id: 2gb
        region_id: ams2
        image_id: fedora-19-x64
    


Notes
-----

.. note:: Two environment variables can be used, DO_API_KEY and DO_API_TOKEN. They both refer to the v2 token.
.. note:: As of Ansible 1.9.5 and 2.0, Version 2 of the DigitalOcean API is used, this removes ``client_id`` and ``api_key`` options in favor of ``api_token``.
.. note:: If you are running Ansible 1.9.4 or earlier you might not be able to use the included version of this module as the API version used has been retired. Upgrade Ansible or, if unable to, try downloading the latest version of this module from github and putting it into a 'library' directory.


    
This is a Core Module
---------------------

For more information on what this means please read :doc:`modules_core`

    
For help in developing on modules, should you be so inclined, please read :doc:`community`, :doc:`developing_test_pr` and :doc:`developing_modules`.
